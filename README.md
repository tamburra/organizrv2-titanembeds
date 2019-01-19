# organizrv2-titanembeds
Embeds Titan chat and forces Org username as Bot guest username w/ Plex Theme

First make a user defined css slot on https://titanembeds.com and make note of the ID.

<h2>Auto Plex Username as Guest Username on Titan Bot</h2>

Add this code to your Custom HTML Homepage Item in Organizer and make sure the minimum authentication matches that of the authentication of your Discord TAB.

```
<script>
var plexUsername = document.querySelector('.profile-pic .hidden-xs').innerHTML;
var discordUsername = plexUsername.replace(/@[^@]+$/, '').replace(/\./g,"_").replace(/ /g,"%20");
var discordURL = "https://titanembeds.com/embed/SERVERID?css=CSSID&fixedsidenav=true&username=" + discordUsername;
$("#menu-Discord").attr("data-url",discordURL);
$("#container-Discord").attr("data-url",discordURL);
</script>
```

Change the Discord URL's SERVERID and CSSID accordingly.
"#menu-Discord" and "#container-Discord" need to change according to what you name your tab.  Mine is "Discord". 
