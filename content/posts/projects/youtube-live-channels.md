---
title: "YouTube Live Channels on any IPTV Client"
date: 2024-02-18T00:00:00+05:30
tags: ["Project","Youtube","IPTV","M3U","Playlist"]
---

Many public broadcasts and free-to-air channels are now available on YouTube as live videos. Many smart TVs and streaming boxes support digital channels by adding a playlist. These stream over the internet rather than satellite or cable.

## Live Channels
The [GitHub project](https://github.com/abskmj/iptv-youtube-live) provides playlists in M3U8 format of all live channels categorized by their content and language. The playlists can be added to any IPTV player or client on any device to view the live channels. They update automatically at intervals to add any newly discovered channels or remove any video that is not live anymore (using [GitHub Actions](https://github.com/features/actions)). A list of channels is available at [GitHub](https://github.com/abskmj/iptv-youtube-live/blob/main/channels.csv).

> [abskmj/iptv-youtube-live](https://github.com/abskmj/iptv-youtube-live) - M3U Playlists of Youtube live channels that add to any IPTV client 

## API Service
The project uses an API service to get a live stream of a YouTube video in  HLS or M3U format.

### YouTube Channel
It picks up the live feed of a YouTube channel. It works when a YouTube channel has a single live feed or goes live frequently. It might not work when a channel has multiple live feeds simultaneously. Please use the video link for this case.
```
# format of the link
https://ythls-v2.onrender.com/channel/$youtube_channel_id.m3u8

# example
https://ythls-v2.onrender.com/channel/UCt4t-jeY85JegMlZ-E5UWtA.m3u8
```
### Youtube Video
It picks up the live feed of a YouTube video. It works when the video is live.
```
# format of the link
https://ythls-v2.onrender.com/video/$youtube_video_id.m3u8

# example
https://ythls-v2.onrender.com/video/Nq2wYlWFucg.m3u8
```

> Although I have taken great care to keep the service stable, please note that the service is hosted on a basic tier of a cloud provider to minimize the cost. It might not have sufficient resources to handle numerous requests at a time. If you need a stable service, I would suggest you deploy this service with your cloud provider. An executable of this service is available for download.

## Setup IPTV
The playlists are compatible with any IPTV player or client on any device. As an example, I have added the steps for an Android-based device.

### Get Playlist
#### Master Playlist 
It has all the live channels. It categorizes the channels into multiple groups based on their content and language. You would see a list of these groups and a `Ungrouped` section on the IPTV player.
```
https://abskmj.github.io/iptv-youtube-live/index.m3u8
``` 

#### Group Playlist 
It has channels for a specific group. For example, if you like watching Cartoons in English, add the below playlist.
```
https://abskmj.github.io/iptv-youtube-live/kids-english.m3u8
```

All group playlists are available at [Github](https://github.com/abskmj/iptv-youtube-live/tree/gh-pages). Add `https://abskmj.github.io/iptv-youtube-live/` before the name of a playlist to get its link.

### Add Playlist
I have tried many IPTV apps on my Android mobile and TV, but I recommend the [Televizo](https://televizo.net/) app. It provides a simple and easy-to-use experience on an Android mobile / TV. It has a free and a paid version.

1. Open Televizo app
2. Click on the gear icon on the top right to open the settings screen
3. Click on `Playlists` menu item
4. Click on the plus icon on the top right
5. Click on the `New M3U Playlist` menu item
6. Type `abskmj` as the playlist name
7. Paste the playlist link

You can repeat the above steps to add more playlists.
