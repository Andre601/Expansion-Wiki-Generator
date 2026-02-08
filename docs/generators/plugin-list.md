# Plugin List

This Generator is made for the [Plugins using PlaceholderAPI](https://wiki.placeholderapi.com/users/plugins-using-placeholderapi) page of the PlaceholderAPI wiki.

--8<-- "note.md"

## Generator

Below is the generator that you can use to create the markdown required for the Plugins using PlaceholderAPI Wiki Page.

<span style="color: var(--md-form-fg-color--required)">*</span> = Required

/// html | label.md-form-required[for="pluginName"]
Plugin Name:
///
/// html | input.md-input.md-input--stretch#pluginName[type="text" placeholder="MyPlugin" required]
///

/// html | p
///

/// html | label[for="pluginLink"]
Plugin Link:
///
/// html | input.md-input.md-input--stretch#pluginLink[type="text" placeholder="https://www.spigotmc.org/resources/6245"]
///

/// html | p
///

/// html | input#isHytaleMod[type="checkbox"]
///
/// html | label[for="isHytaleMod"]
Is Hytale Mod
///

/// html | p
///

/// html | input#pluginSupportsPlaceholders[type="checkbox"]
///
/// html | label[for="pluginSupportsPlaceholders"]
Plugin supports other placeholders.
///

/// html | p
///

/// html | label[for="pluginExpansion"]
Plugin Expansion Name:
///
/// html | input.md-input.md-input--stretch#pluginExpansion[type="text" placeholder="myexpansion"]
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
    const pluginName = document.getElementById("pluginName").value;
    const pluginLink = document.getElementById("pluginLink").value;
    const isHytaleMod = document.getElementById("isHytaleMod").checked;
    const pluginSupportsPlaceholders = document.getElementById("pluginSupportsPlaceholders").checked;
    const pluginExpansion = document.getElementById("pluginExpansion").value;
    const expansionOutputField = document.getElementById("output");
    if (!pluginName) {
        expansionOutputField.value = `Field "Plugin name" needs to be filled out!`;
        expansionOutputField.style.borderColor = `#ff5252`;
        expansionOutputField.style.backgroundColor = `#ff52521a`;
        return;
    }
    expansionOutputField.style.borderColor = `#00c853`;
    expansionOutputField.style.backgroundColor = `#00c8531a`;
    const spigot_link_regex = /https:\/\/www\.spigotmc\.org\/resources\/.+\.(\d+)/;
    const matchResults = pluginLink.match(spigot_link_regex);
    const link = matchResults ? "https://www.spigotmc.org/resources/" + matchResults[1] : pluginLink;
    const result = `- ${link ? `[${pluginName}](${link})` : `${pluginName}`}
    - [${pluginSupportsPlaceholders ? `x` : ` `}] Supports placeholders.
    - [${pluginExpansion ? `x` : ` `}] Provides own placeholders. [${pluginExpansion ? `[**Link**](../placeholder-list/${isHytaleMod ? `hytale` : `minecraft`}.md#${pluginExpansion.toLowerCase().replace(/\s/g, '-')})` : `Link`}]`;
    expansionOutputField.value = result;
  }
</script>

[placeholders]: https://github.com/PlaceholderAPI/PlaceholderAPI/wiki/Placeholders
[papi-repo]: https://github.com/PlaceholderAPI/PlaceholderAPI
[update-branch]: https://github.com/PlaceholderAPI/PlaceholderAPI/tree/wiki#fetch-changes-from-upstream
[entries-example]: https://github.com/PlaceholderAPI/PlaceholderAPI/tree/wiki#example
[plugins-page]: https://github.com/PlaceholderAPI/PlaceholderAPI/blob/wiki/Plugins-using-PlaceholderAPI.md
