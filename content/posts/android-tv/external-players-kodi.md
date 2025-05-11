---
title: "External Players in Kodi"
date: 2025-05-11T00:00:00+05:30
tags: ["AndroidTV", "Kodi", "JustPlayer", "NextPlayer"]
---

Setup video players like Just Player and Next Player as external players on Kodi

## Video Players
I use the below players on my Android TV
- [Just Player](https://play.google.com/store/apps/details?id=com.brouken.player)
  - I use it as the default player on Kodi.
  - It plays most video and audio formats.
  - It is open source and available at [github.com](https://github.com/moneytoo/Player)
- [Next Player](https://play.google.com/store/apps/details?id=dev.anilbeesetti.nextplayer)
  - I use it as an alternative.
  - It is open source and available at [github.com](https://github.com/anilbeesetti/NextPlayer)
  - To use in Kodi, long click on the item to play, and select the `Play using` menu option.

## Configuration
- Install the player of your choice
- Use the package name of the player as `filename` in the configuration file
- Create a `playercorefactory.xml` configuration file at `Android/data/org.xbmc.kodi/files/.kodi/userdata/`

Configuration file to use Just Player as the default player and Next Player as alternative
```xml
<<playercorefactory>
    <!-- players -->
    <players>
        <player name="JustPlayer" type="ExternalPlayer" audio="false" video="true">
          <filename>com.brouken.player</filename>
          <hidexbmc>true</hidexbmc>
          <playcountminimumtime>120</playcountminimumtime>
        </player>
        <player name="NextPlayer" type="ExternalPlayer" audio="false" video="true">
          <filename>dev.anilbeesetti.nextplayer</filename>
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

## References
- External Players at [kodi.wiki](https://kodi.wiki/view/External_players)