# System design for youbute
## Requirements
### Functional requirements
- upload video
- watch(stream) video

-----------------out of scope ----------
- make coments
- like/dislikes
- search videos
- view video information like view count

### Scale
10m users

### Non-functional requirements
- high availability, evenual consistency
- Low latency streaming
- Scalability
- support large video
- resumable upload

-----------out of scope ---------
- protect against bad content
- protect against bots or fake accounts uploading/consuming videos

## Core Entities and APIs
### Core Entities
- User
- Video
- Video meata

### APIs
- upload  
  POST /videos  
  Request: {video, vide metadata}     
  Response: videoId
- stream  
  GET /vidoes/{videoId}  -> Video, Video Metadaa

## High-level deigns

## Deep dive
- How video processing works
- How to improve latency
- How to support resumable uploads
- How can we handle processing a video to support adaptive bitrate streaming?
- How do we scale to a large number of videos uploaded / watched a day?
  1. User cache for metadata, CDN
  2. Queue for video processing service
