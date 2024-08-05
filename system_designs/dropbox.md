# System design for dropbox
## Requirements
### Functional requirements
- upload file
- download file
- share file  
------------out of scope----------
- edit file
- view files without downloading

### Non-functional requirements
- availability > consistency
- low latency make upload or download as fast as possible
- secure & reliable
- support large file 50GB

---------out of scope----------
- storage limit per user
- file versioning
- scan files for virus and malware

## Core Entities and API/System Interface
### Core Entities
- File
- File metadata
- User

### APIs
- upload file    
  POST /files,     
  Request: {File, Filemeata}  
- download file  
  GET /files/{fileId} -> File, File Metadata
- share file  
  POST /files/{fileId}/share  
  Reqeust: {users:[]}

## Design deep dive
- support large files? progress indicator/resume download, chunk files on client side
- How can we make uploads and downloads as fast as possible? compress files
- How can you ensure file security? HTTPS,encrypt file on transmission; Encrypt file on rest; presigned url to control permission
