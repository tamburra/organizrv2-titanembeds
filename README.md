# organizrv2-titanembeds
Embeds Titan chat and forces Org username as Bot guest username w/ Plex Theme

<ul>
  <li>First make a user defined css slot on https://titanembeds.com and paste the above css code into the field.  Make note of the ID on Titan as you will need to call it in the URL to the Titan Embed later.</li>
  <li>Make sure your settings on Titan site are as is:<br>
    "Unauthenticated (Guest) Users" - ENABLED (REQUIRED)<br>
    "Toggle Visitor Mode" - DISABLED (OPTIONAL)<br>
    "Toggle Webhooks Messages" - ENABLED (REQUIRED if you want Plex usernames to display in chat. Bot needs Manage Webhooks permissions from within your Discord server settings for this to work.)<br>
    "Chat Links" - ENABLED (OPTIONAL)<br>
    "Render Links as an Embed" - ENABLED (OPTIONAL)<br>
    "Toggle File Attachments" - ENABLED (OPTIONAL)</li>
<li>Add this code to your Custom Javascript in Organizr (Settings --> Customize --> Appearance --> Custom Javascript) and change the variabled under the "// Modify these variables only" section ONLY.

```
// Override function tabActions()
function tabActions(event, name, type) {
    //
    // Intercepts links to Discord tab in Organizr and redirects to TitanEmbed URL
    // with specified URL queries.
    //

    // Modify these variables only (leave values blank ("") if you do not want to use)
    var orgTabName = "Discord"; 			// Name of Organizr tab for Discord
    var titanServer = "470309961864577025";		// Discord Server ID
    var titanCSS = "420";				// Titan CSS ID
    var titanDefaultChannel = "";			// Default Discord Channel ID to be opened
    var titanFixedSideNav = "true";			// Displays side navigation of channels (blank defaults to false)
    var titanNoScroll = "false";			// Prevents the embed from scrolling down on first load (blank defaults to false)

    // Don't change any this
    if (name === 'Discord') {
        var plexUsername = activeInfo.user.username;
        var discordUsername = plexUsername.replace(/@[^@]+$/, '').replace(/\./g,"_").replace(/ /g,"%20").replace(/[^\w\s]/gi, '');
        var discordURL = "https://titanembeds.com/embed/" + titanServer + 
            "?css=" + titanCSS + 
            "&defaultchannel=" + titanDefaultChannel + 
            "&fixedsidenav=" + titanFixedSideNav + 
            "&noscroll=" + titanNoScroll + 
            "&username=" + discordUsername;
        var orgDiscordTabName = orgTabName.replace(/\s+/g, '-');
        $("#menu-" + orgDiscordTabName).attr("data-url",discordURL);
        $("#container-" + orgDiscordTabName).attr("data-url",discordURL);
        document.getElementById("frame-" + orgDiscordTabName).src = discordURL;
    }
}
```
</li>
</ul>
