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
  
