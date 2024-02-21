---
title: "YouTube HLS Server"
date: 2024-02-21T00:00:00+05:30
tags: ["Project","Youtube","IPTV","M3U","Playlist", "HLS"]
---

The server provides the HLS (live streaming) link for a YouTube channel or video. Any video or IPTV player can play a YouTube live video using this link.

## How to get it?
1. An executable of the server is available for purchase at [buymeacoffee.com](https://www.buymeacoffee.com/abskmj/e/223409).
2. You will receive an email with a link to download.
3. Extract the downloaded zip file.

## How to use it?
- Upload the executable to your machine
- Assign the executable the permission to run 
```bash
chmod +x ./youtube-hls-server
```

- Start the server
```bash
./youtube-hls-server

# output
server listening on port: 3333
```

- Open the URL on the browser
```bash
$server/

# IP with port
<ip>:3333/

# Domain without port
<domain>/
```

- (optional) Change the port of the server
```bash
PORT=8080 ./youtube-hls-server

# output
server listening on port: 8080
``` 

## Before you buy?
1. The executable supports Linux machines with `amd64` architecture only. Most of the cloud providers provision machines with this architecture by default.
2. The server connects to youtube.com for each request. If you send many requests in a short time, YouTube will impose a rate limit on your server. Requests over the rate limit will fail with the [`429 Too Many Requests`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/429) error status code. To avoid this, consider adding a cache before the server. If you are planning to use the server for you and your family, there is a low chance of hitting the rate limit.

## Server
### HLS Link
The link has a `.m3u8` extension, a popular extension for a live stream. Most IPTV players are compatible with this format. It redirects to the [HLS](https://en.wikipedia.org/wiki/HTTP_Live_Streaming) streaming feed of the YouTube video. When successful, it responds with a [`302 Found`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/302) status code.

#### Youtube Channel
It picks up the live feed of a YouTube channel. It works when a YouTube channel has a single live feed or goes live frequently. It might not work when a channel has multiple live feeds simultaneously. Please use the video link for this case.

```bash
# format of the link
$server/channel/$youtube_channel_id.m3u8

# example
$server/channel/UCt4t-jeY85JegMlZ-E5UWtA.m3u8
```
#### Youtube Video
It picks up the live feed of a YouTube video. It works when the video is live.

```bash
# format of the link
$server/video/$youtube_video_id.m3u8

# example
$server/video/Nq2wYlWFucg.m3u8
```

### JSON Metadata
The API provides information about the YouTube channel or video in JSON format. 

#### Youtube Channel
```bash
# format of the link
$server/channel/$youtube_channel_id.json

# example
$server/channel/UCt4t-jeY85JegMlZ-E5UWtA.json

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
$server/video/$youtube_video_id.json

# example
$server/video/Nq2wYlWFucg.json

# response
{
  "name": "<string>", # name of youtube channel
  "logo": "<url>", # logo of youtube channel
  "stream": "<url>/index.m3u8", # hls of youtube video
  "status":  <http_code> # response code from youtube
}
```
