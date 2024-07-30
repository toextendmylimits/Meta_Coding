# System design for chat
## Requirements
### Functional requirements
- one on one chat
- send media file
- group chat
- chat storage
- push notification

----------out of scope----------
- audio/video calling
- registration/profile management
- interactions with business

### Non-functional requirements
- Consistency order of message should be maintained
- high availability
- Low latency
- Scalability
- Fault tolerance

----------out of scope----------
- security
- prevent against bad content

### Capacity analysis
TPS:1B * 100 /10^5 seconds = 1m /s  
Storage: 1B * 100 * 100byte = 10 TB  

## Core Entities & API
### Core Entities
User
Group
Chat

### APIs
- send one on one message  
  sendMessage(receiverId,senderId,timestamp,text,link to media file)
- send group message
  sendMessageGroup(groupId,senderId,timestamp,text,link to media file)

- get message
  GET /messages
- upload file
  POST /files
- download file
  GET /files/{fileId}

## Data Models
- Message
