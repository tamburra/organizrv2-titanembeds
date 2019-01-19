# organizrv2-titanembeds
Embeds Titan chat and forces Org username as Bot guest username w/ Plex Theme

<ul>
  <li>First make a user defined css slot on https://titanembeds.com and paste the above css code into the field.  Make note of the ID as you will need to call it in the URL to the Titan Embed later.<li>
<li>Add this code to your Custom HTML Homepage Item in Organizer and make sure the minimum authentication matches that of the authentication of your Discord TAB.

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
"#menu-Discord" and "#container-Discord" need to change according to what you name your tab in Org.  Mine is "Discord". When making the Tab in Org you can specify any url as the script above will be changing the url anyways.</li>
</ul>
