---
title: "How Live Streaming Works?"
published: "Coming soon"
wallpaper: "https://raw.githubusercontent.com/akbarjorayev/blogs/refs/heads/main/blogs/how-live-streaming-works/assets/blog-wallpaper.light.webp"
---

## Input
It all starts with a camera or microphone capturing raw video and audio. These are the *inputs* of a live stream. But raw media is huge, and if it’s 4k video, you would probably need NASA-speed internet. That’s where our hero, **compression**, comes in.  

## Compression
A codec compresses the video so it can travel more efficiently through servers. Imagine a sped-up sunrise video, where only the sun's position changes throughout the stream. Compression tells the system, 'hey, only render that part.'  

Videos are not sent in mp4 format because it takes too much space. Instead, they are converted to H.265 (HEVC) or H.264 (AVC) format and sent to CDNs in chunks. A chunk is a part of a video, maybe 2 seconds of the live stream. That is exactly why, even if your internet lags, you will still see 2–3 seconds of the live stream, because that chunk is already loaded.  

## CDN
CDNs (Content Delivery Networks) are used to reduce the load on the main server. Users get media from the CDN nearest to them, not from the main server. This helps deliver live streaming more smoothly and faster.  

## Protocol
### UDP
UDP (User Datagram Protocol) is used to send messages and packets over the internet. As I said, we send the media in chunks, and for live streaming, we don’t actually need every single chunk. What we really need is **delivering media** to users. UDP sends chunks even if some are lost.  

```txt
chunk1
chunk2
chunk3
MISSING
chunk5
...
```

### RTP over UDP
### HLS/DASH
