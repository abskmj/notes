---
title: "YouTube HLS Server"
date: 2024-02-21T00:00:00+05:30
tags: ["Project","Youtube","IPTV","M3U","Playlist", "HLS"]
---

The server provides a set of APIs.
1. HLS Link
2. JSON Metadata

### HLS Link
The link has a `.m3u8` extension, a popular extension for a live stream. Most IPTV players are compatible with this format. It redirects to the [HLS](https://en.wikipedia.org/wiki/HTTP_Live_Streaming) streaming feed of the YouTube video. When successful, it responds with a [`302 Found`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/302) status code.

#### Youtube Channel
It picks up the live feed of a YouTube channel. It works when a YouTube channel has a single live feed or goes live frequently. It might not work when a channel has multiple live feeds simultaneously. Please use the video link for this case.

```bash
# format of the link
https://ythls-v2.onrender.com/channel/$youtube_channel_id.m3u8

# example
https://ythls-v2.onrender.com/channel/UCt4t-jeY85JegMlZ-E5UWtA.m3u8
```
#### Youtube Video
It picks up the live feed of a YouTube video. It works when the video is live.

```bash
# format of the link
https://ythls-v2.onrender.com/video/$youtube_video_id.m3u8

# example
https://ythls-v2.onrender.com/video/Nq2wYlWFucg.m3u8
```

### JSON Metadata
The API provides information about the YouTube channel or video in JSON format. 

#### Youtube Channel
```bash
# format of the link
https://ythls-v2.onrender.com/channel/$youtube_channel_id.json

# example
https://ythls-v2.onrender.com/channel/UCt4t-jeY85JegMlZ-E5UWtA.json

# response
{
  "name": "<string>", # name of youtube channel
  "logo": "<url>", # logo of youtube channel
  "stream": "<url>/index.m3u8", # hls of youtube video
  "status":  <http_code> # response code from youtube
}
```
#### Youtube Video
```bash
# format of the link
https://ythls-v2.onrender.com/video/$youtube_video_id.json

# example
https://ythls-v2.onrender.com/video/Nq2wYlWFucg.json

# response
{
  "name": "<string>", # name of youtube channel
  "logo": "<url>", # logo of youtube channel
  "stream": "<url>/index.m3u8", # hls of youtube video
  "status":  <http_code> # response code from youtube
}
```

### API Errors
### How to get the YouTube channel ID