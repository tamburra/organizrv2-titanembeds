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
<li>Add this code to your Custom Javascript in Organizr (Settings --> Customize --> Appearance --> Custom Javascript) and change the variables under the "// Modify these variables only" section ONLY.

```
// Modify these variables only
var titanServer = "123456789";        // Discord Server ID
var titanCSS = "100";                 // Titan CSS ID
var titanDefaultChannel = "";         // Default Discord Channel ID to be opened
var titanFixedSideNav = "true";       // Displays side navigation of channels
var titanNoScroll = "false";          // Prevents the embed from scrolling down on first load

// Don't change any this
var userMenuElement = $("li[data-url^='https://titanembeds.com']");
var orgTabName = userMenuElement.attr('id').split('-')[1];
var plexUsername = activeInfo.user.username;
var discordUsername = plexUsername.replace(/@[^@]+$/, '').replace(/\./g,"_").replace(/ /g,"%20").replace(/[^\w\s]/gi, '');
var discordURL = "https://titanembeds.com/embed/" + titanServer + 
                 "?css=" + titanCSS + 
                 "&defaultchannel=" + titanDefaultChannel + 
                 "&fixedsidenav=" + titanFixedSideNav + 
                 "&noscroll=" + titanNoScroll + 
                 "&username=" + discordUsername;
$("#menu-" + orgTabName).attr("data-url",discordURL);
$("#container-" + orgTabName).attr("data-url",discordURL);
```
</li>
<li>Create a new tab in Ogranzir with tab url: "https://titanembeds.com/embed/[DISCORD-SERVER-ID/[CSS-ID]".<br>
Change [DISCORD-SERVER-ID] with your discord server id and [CSS-ID] to your Titan css id.  This is helpful when some decides to refresh the tab.
</li>
<li>PROFIT</li>
</ul>
