# Expansion Wiki generator

This page contains a simple generator for creating a new entry for the [Placeholders Wiki Page][placeholders] of PlaceholderAPI.

## Before you start...

Please make sure of the following:

1. You forked the [PlaceholderAPI repository][papi-repo]
2. You switched to the `wiki` branch of your fork.
3. Your wiki branch (Or any branch you made from it) is up-to-date. [[How to update][update-branch]]

To use this generator, input text into the different text fields.  
The [output field](#output) will automatically update once you fill out the required fields.

## Additional notes

- Remember to also add a new entry to the list of expansions at the top of the placeholders page.
- Add `----` before and/or after your entry if there are other expansions listed before/after you. [[Example][entries-example]]
- If your expansion requires a plugin, make sure to also add this plugin to the [`Plugins using PlaceholderAPI` page][plugins-page]

## Generator

Below is the generator that you can use to create the markdown required for the Placeholders Wiki Page.

<span style="color: var(--md-form-fg-color--required)">*</span> = Required

<label for="expansionName" class="md-form-required">Name:</label>
<input id="expansionName" class="md-input md-input--stretch" type="text" placeholder="MyExpansion" onchange="updateOutput()" onkeyup="updateOutput()" required>

<label for="expansionLink">Link:</label>
<input id="expansionLink" class="md-input md-input--stretch" type="text" placeholder="https://www.spigotmc.org/resources/6245" onchange="updateOutput()" onkeyup="updateOutput()">

<label for="expansioneCloud">eCloud name:</label>
<input id="expansioneCloud" class="md-input md-input--stretch" type="text" placeholder="myexpansion" onchange="updateOutput()" onkeyup="updateOutput()">

<label for="expansionDescription">Description:</label>
<input id="expansionDescription" class="md-input md-input--stretch" type="text" placeholder="For more info visit &lbrack;the docs&rbrack;(https://github.com/PlaceholderAPI/PlaceholderAPI/wiki)" onchange="updateOutput()" onkeyup="updateOutput()">

<label for="expansionPlaceholders" class="md-form-required">Placeholders:</label>
<textarea id="expansionPlaceholders" class="md-textarea md-textarea--stretch" type="text" placeholder="%myexpansion_placeholder%" onchange="updateOutput()" onkeyup="updateOutput()"></textarea>

<label for="output">Output:</label>
<textarea id="output" class="md-textarea md-textarea--stretch" type="text" placeholder="Fill the above fields to get an output..." readonly></textarea>
<button id="copy" data-clipboard-target="#output">Copy</button>

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
  function updateOutput() {
    const expansionName = document.getElementById("expansionName").value;
    const expansionLink = document.getElementById("expansionLink").value;
    const expansioneCloud = document.getElementById("expansioneCloud").value;
    const expansionDescription = document.getElementById("expansionDescription").value;
    const expansionPlaceholders = document.getElementById("expansionPlaceholders").value;
    if (!expansionName || !expansionPlaceholders) {
        return;
    }
    const spigot_link_regex = /https:\/\/www\.spigotmc\.org\/resources\/.+\.(\d+)/;
    const matchResults = expansionLink.match(spigot_link_regex);
    const link = matchResults ? "https://www.spigotmc.org/resources/" + matchResults[1] : expansionLink;
    const expansionOutputField = document.getElementById("output");
    const result = `- ### **${link ? `[${expansionName}](${link})` : `${expansionName}`}**
${expansioneCloud ? `  > /papi ecloud download ${expansioneCloud}` : `  > NO DOWNLOAD COMMAND`}
${expansionDescription ? `\n  ${expansionDescription}\n` : ``}
  \`\`\`
  ${expansionPlaceholders.replace(/\n/g, '\n  ')}
  \`\`\``;
    expansionOutputField.value = result;
  }
</script>

[placeholders]: https://github.com/PlaceholderAPI/PlaceholderAPI/wiki/Placeholders
[papi-repo]: https://github.com/PlaceholderAPI/PlaceholderAPI
[update-branch]: https://github.com/PlaceholderAPI/PlaceholderAPI/tree/wiki#fetch-changes-from-upstream
[entries-example]: https://github.com/PlaceholderAPI/PlaceholderAPI/tree/wiki#example
[plugins-page]: https://github.com/PlaceholderAPI/PlaceholderAPI/blob/wiki/Plugins-using-PlaceholderAPI.md