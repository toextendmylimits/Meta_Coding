# system design for instagram
## Requirements
### Functional requirements
- upload photo
- follow people
- view feed of images

-------------out of scope--------
- remove duplicate
- moderate content
- search
- make comments
- likes

### Non-functional requirements
- High availability, eventual consistency
- Low latency
- Scalability
- Fault Tolerence

---------out of scope ----------
- privacy
- protect against bad content

### Capacity Analysis
- write TPS: 5m /10^5 seconds = 50/s
- read TPS: 500/s
- storage: photos 5m*2MB = 10TB, metadata 5m*1KB=5GB

## API
- upload photo  
  POST /posts  
  {description, file}
- follow people  
  POST /follow
- view feed  
  GET /feeds?cursor=,pageSize=  
  thumbnail,  

## Data models
Metadata:
postId,
description,
size,
mime type,
link to blob storage,
uploadedBy,
timestamp

## High-level design

## Design deep dive
- celebrity issue fan out hyrbid pull/push
- inactive users pull
- CDN cache popular content
- How to upload large video/photo? MultiPartFile
- Data partition by postId
- Data replication 3 copies, 2 copy in data center, 1 copy in different data center
- avoid duplicate both client side and server side
- moderate content machine learning

