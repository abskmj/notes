---
title: "External Players in Kodi"
date: 2022-08-27T00:00:00+05:30
tags: ["AndroidTV", "Kodi", "JustPlayer", "MXPlayer"]
---

Setup video players like Just Player and MX Player to use on Kodi

# Video Players
- Install the player of your choice
- Use the package name of the player as `filename` in the configuration file

I use the below players on my Android TV
- [Just Player](https://play.google.com/store/apps/details?id=com.brouken.player)
  - I use it as the default player on Kodi.
  - It plays most video and audio formats.
  - It is open source and available at [github.com](https://github.com/moneytoo/Player)
- [MX Player](https://play.google.com/store/apps/details?id=com.mxtech.videoplayer.ad)
  - I use it as an alternative to play any files that are not supported by the other player.
  - To use in Kodi, long click on the item to play, and select the `Play using` menu option.

# Configuration
Create a `playercorefactory.xml` configure file at `Android/data/org.xbmc.kodi/files/.kodi/userdata/`

```xml
<playercorefactory>
    <!-- players -->
    <players>
        <player name="JustPlayer" type="ExternalPlayer" audio="false" video="true">
          <filename>com.brouken.player</filename>
          <hidexbmc>true</hidexbmc>
          <playcountminimumtime>120</playcountminimumtime>
        </player>
        <player name="MXPlayer" type="ExternalPlayer" audio="false" video="true">
          <filename>com.mxtech.videoplayer.ad</filename>
          <hidexbmc>true</hidexbmc>
          <playcountminimumtime>120</playcountminimumtime>
        </player>
    </players>
    <!-- rules -->
    <rules action="prepend">
      <rule protocols="smb" player="JustPlayer" />
      <rule dvdimage="true" player="JustPlayer"/>
      <rule protocols="rtmp" player="JustPlayer"/>
      <rule protocols="rtsp" player="JustPlayer" />
      <rule protocols="sop" player="JustPlayer" />
      <rule internetstream="true" player="JustPlayer" />
      <rule video="true" player="JustPlayer"/> <!-- Default for anything else not listed -->
    </rules>
</playercorefactory>
```

# References
- External Players at [kodi.wiki](https://kodi.wiki/view/External_players)