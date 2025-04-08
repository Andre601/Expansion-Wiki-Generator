# Placeholder List

This Generator is made for the [Placeholders List](https://wiki.placeholderapi.com/users/placeholder-list) page of the PlaceholderAPI wiki.

--8<-- "note.md"

## Additional notes

- Remember to also add a new entry to the list of expansions at the top of the placeholders page.
- Add `----` before and/or after your entry if there are other expansions listed before/after you. [[Example][entries-example]]
- If your expansion requires a plugin, make sure to also add this plugin to the [`Plugins using PlaceholderAPI` page][plugins-page]

## Generator

Below is the generator that you can use to create the markdown required for the Placeholders Wiki Page.

<span style="color: var(--md-form-fg-color--required)">*</span> = Required

/// html | label.md-form-required[for="expansionName"]
Name:
///
/// html | input.md-input.md-input--stretch#expansionName[type="text" placeholder="MyExpansion" required]
///

/// html | p
///

/// html | label[for="expansionLink"]
Plugin Link:
///
/// html | input.md-input.md-input--stretch#expansionLink[type="text" placeholder="https://www.spigotmc.org/resources/6245"]
///

/// html | p
///

/// html | label[for="expansioneCloud"]
eCloud Name / Download Link:
///
/// html | input.md-input.md-input--stretch#expansioneCloud[type="text" placeholder="myexpansion"]
///

/// html | p
///

/// html | label[for="expansionDescription"]
Description:
///
/// html | input.md-input.md-input--stretch#expansionDescription[type="text" placeholder="For more info visit [the docs](https://wiki.placeholderapi)"]
///

/// html | p
///

/// html | input#expansionHasPrevious[type="checkbox"]
///
/// html | label[for="expansionHasPrevious"]
Has entries before itself.
///

/// html | p
///

/// html | input#expansionHasAfter[type="checkbox"]
///
/// html | label[for="expansionHasAfter"]
Has entries after itself.
///

/// html | p
///

/// html | label.md-form-required[for="expansionPlaceholders"]
Placeholders:
///
/// html | textarea.md-textarea.md-textarea--stretch#expansionPlaceholders[type="text" placeholder="%myexpansion_placeholder%"]
///

/// html | p
///

/// html | label[for="output"]
Output:
///
/// html | textarea.md-textarea.md-textarea--stretch#output[type="text" placeholder="Fill the above fields to get an output..." readonly]
///
/// html | button#copy[data-clipboard-target="#output"]
Copy
///

<script>
  if ('addEventListener' in window) {
    window.addEventListener('load', function() { document.body.className = document.body.className.replace(/\bis-preload\b/, ''); });
    document.body.className += (navigator.userAgent.match(/(MSIE|rv:11\.0)/) ? ' is-ie' : '');
  }
</script>
<script src="https://cdn.jsdelivr.net/npm/clipboard@2/dist/clipboard.min.js"></script>
<script type="application/javascript">
  new ClipboardJS("#copy");
  document.getElementById("copy").onclick = function() {
    document.getElementById("copy").innerText = "Copied!";
  };
  document.addEventListener('input', function() {
    updateOutput();
  });
  function updateOutput() {
    const expansionName = document.getElementById("expansionName").value;
    const expansionLink = document.getElementById("expansionLink").value;
    const expansionCloud = document.getElementById("expansioneCloud").value;
    const expansionDescription = document.getElementById("expansionDescription").value;
    const expansionCheckBefore = document.getElementById("expansionHasPrevious").checked;
    const expansionCheckAfter = document.getElementById("expansionHasAfter").checked;
    const expansionPlaceholders = document.getElementById("expansionPlaceholders").value;
    const expansionOutputField = document.getElementById("output");
    if (!expansionName || !expansionPlaceholders) {
        expansionOutputField.value = `Fields "Name" and "Placeholders" need to be filled out!`;
        expansionOutputField.style.borderColor = `#ff5252`;
        expansionOutputField.style.backgroundColor = `#ff52521a`;
        return;
    }
    expansionOutputField.style.borderColor = `#00c853`;
    expansionOutputField.style.backgroundColor = `#00c8531a`;
    const spigot_link_regex = /https:\/\/www\.spigotmc\.org\/resources\/.+\.(\d+)/;
    const matchResults = expansionLink.match(spigot_link_regex);
    const link = matchResults ? "https://www.spigotmc.org/resources/" + matchResults[1] : expansionLink;
    const result = `${expansionCheckBefore ? `----\n\n` : ``}### **${link ? `[${expansionName}](${link.replace(/\s/g, '%20')})` : `${expansionName}`}**
/// ${expansionCloud ? `${expansionCloud.startsWith('https://') ? `download | ${expansionCloud.replace(/\s/g, '%20')}` : `command | papi ecloud download ${expansionCloud.replace(/\s/g, '-')}`}` : `integrated | Built into Plugin`}
///
${expansionDescription ? `\n${expansionDescription}\n` : ``}
\`\`\`
${expansionPlaceholders}
\`\`\`${expansionCheckAfter ? `\n\n----` : ``}`;
    expansionOutputField.value = result;
  }
</script>

[placeholders]: https://github.com/PlaceholderAPI/PlaceholderAPI/wiki/Placeholders
[papi-repo]: https://github.com/PlaceholderAPI/PlaceholderAPI
[update-branch]: https://github.com/PlaceholderAPI/PlaceholderAPI/tree/wiki#fetch-changes-from-upstream
[entries-example]: https://github.com/PlaceholderAPI/PlaceholderAPI/tree/wiki#example
[plugins-page]: https://github.com/PlaceholderAPI/PlaceholderAPI/blob/wiki/Plugins-using-PlaceholderAPI.md
