---
title: 'How Live Streaming Works?'
published: 'Coming soon'
wallpaper: 'https://raw.githubusercontent.com/akbarjorayev/blogs/refs/heads/main/blogs/how-live-streaming-works/assets/blog-thumbnail.webp'
---

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/akbarjorayev/blogs/refs/heads/main/blogs/how-live-streaming-works/assets/blog-thumbnail.webp">
  <source media="(prefers-color-scheme: light)" srcset="https://raw.githubusercontent.com/akbarjorayev/blogs/refs/heads/main/blogs/how-live-streaming-works/assets/blog-thumbnail.webp">
  <img src="https://raw.githubusercontent.com/akbarjorayev/blogs/refs/heads/main/blogs/how-live-streaming-works/assets/blog-thumbnail.webp" alt="How Live Streaming Works thumbnail" width="1024" height="576">
</picture>

## Input

It all starts with a camera capturing raw video. That is the _input_ of a live stream. But raw media is huge, and if it's 4k video, you would probably need NASA-speed internet. That's where our hero, **compression**, comes in.

## Compression

A codec compresses the video so it can travel more efficiently through servers. Imagine a sped-up sunrise video, where only the sun's position changes throughout the stream. Compression tells the system, 'hey, only render what changed.'

Videos are not sent as a single MP4 file. Instead, they are encoded using H.265 (HEVC) or H.264 (AVC) and split into small chunks that are delivered to CDNs. A chunk is a part of a video, maybe 2 seconds of the live stream. That is exactly why, even if your internet lags or completely turns off, you will still see 2–3 seconds of the live stream, because that chunk is already loaded.

## CDN

CDNs (Content Delivery Networks) cache and distribute content across geographically distributed servers, reducing both the load on the origin server and latency for end users. Users receive media from the nearest edge server, which improves streaming performance and reduces buffering.

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/akbarjorayev/blogs/refs/heads/main/blogs/how-live-streaming-works/assets/cdn-dark.webp">
  <source media="(prefers-color-scheme: light)" srcset="https://raw.githubusercontent.com/akbarjorayev/blogs/refs/heads/main/blogs/how-live-streaming-works/assets/cdn-light.webp">
  <img src="https://raw.githubusercontent.com/akbarjorayev/blogs/refs/heads/main/blogs/how-live-streaming-works/assets/cdn-light.webp" alt="CDNs (Content Delivery Networks)" width="1472" height="704">
</picture>

## Protocols

### UDP

UDP (User Datagram Protocol) is used to send messages and packets over the internet. As I said, we send the media in chunks, and for live streaming, we don't actually need every single chunk. What we really need is **delivering media** to users. UDP sends chunks even if some are lost.

```txt
chunk1
chunk2
chunk3
MISSING
chunk5
...
```

### RTP

RTP (Real-time Transport Protocol) works on top of UDP and adds metadata like timestamps and sequence numbers. This helps the player understand the correct order of packets and synchronize audio with video. Even if some packets are lost, playback can continue.

## Latency

Live streams are never truly "live" due to the steps we discussed earlier. The time it takes for the media to be captured, compressed, sent to the CDN, and delivered to the user is called **latency**. For most live streams, latency is around 10 seconds.

However, with WebRTC we can achieve ultra-low latency of under 1 second, because WebRTC doesn't rely on servers, it's peer-to-peer. That means the media is sent directly from the broadcaster to the viewer without going through servers, which significantly reduces latency.
