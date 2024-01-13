# Plugin List

This Generator is made for the [Plugins using PlaceholderAPI](https://wiki.placeholderapi.com/users/plugins-using-placeholderapi) page of the PlaceholderAPI wiki.

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

<label for="pluginName" class="md-form-required">Plugin name:</label>
<input id="pluginName" class="md-input md-input--stretch" type="text" placeholder="MyPlugin" required>

<label for="pluginLink">Link:</label>
<input id="pluginLink" class="md-input md-input--stretch" type="text" placeholder="https://www.spigotmc.org/resources/6245">

<input id="pluginSupportsPlaceholders" type="checkbox">
<label for="pluginSupportsPlaceholders">Plugin supports other placeholders.</label>

<label for="pluginExpansion">Expansion name:</label>
<input id="pluginExpansion" class="md-input md-input--stretch" type="text" placeholder="myexpansion">

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
  document.addEventListener('input', function() {
    updateOutput();
  });
  function updateOutput() {
    const pluginName = document.getElementById("pluginName").value;
    const pluginLink = document.getElementById("pluginLink").value;
    const pluginSupportsPlaceholders = document.getElementById("pluginSupportsPlaceholders").checked;
    const pluginExpansion = document.getElementById("pluginExpansion").value;
    const expansionOutputField = document.getElementById("output");
    if (!pluginName) {
        expansionOutputField.value = `Field "Plugin name" needs to be filled out!`;
        return;
    }
    const spigot_link_regex = /https:\/\/www\.spigotmc\.org\/resources\/.+\.(\d+)/;
    const matchResults = pluginLink.match(spigot_link_regex);
    const link = matchResults ? "https://www.spigotmc.org/resources/" + matchResults[1] : pluginLink;
    const result = `- ${link ? `[${pluginName}](${link})` : `${pluginName}`}
    - [${pluginSupportsPlaceholders ? `x` : ` `}] Supports placeholders.
    - [${pluginExpansion ? `x` : ` `}] Provides own placeholders. [${pluginExpansion ? `[**Link**](placeholder-list.md#${pluginExpansion.toLowerCase().replace(/\s/g, '-')})` : `Link`}]`;
    expansionOutputField.value = result;
  }
</script>

[placeholders]: https://github.com/PlaceholderAPI/PlaceholderAPI/wiki/Placeholders
[papi-repo]: https://github.com/PlaceholderAPI/PlaceholderAPI
[update-branch]: https://github.com/PlaceholderAPI/PlaceholderAPI/tree/wiki#fetch-changes-from-upstream
[entries-example]: https://github.com/PlaceholderAPI/PlaceholderAPI/tree/wiki#example
[plugins-page]: https://github.com/PlaceholderAPI/PlaceholderAPI/blob/wiki/Plugins-using-PlaceholderAPI.md