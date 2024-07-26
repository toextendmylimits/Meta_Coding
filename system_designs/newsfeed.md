# System design for news feed
## Requirements
### Functional requirements
- create posts
- follow people
- view feed
---------out of scope--------
- like or comment posts
- post can be private

### Non-functional requirements
- High availability, eventual consistency
- Low latency for posting and viewing
- Scalability 1B users
- Unlimited followers

## Core Entities, APIs/System Interface
### Core Entities
- User
- Post
- Follow

### APIs
- create posts
- POST /posts  
  Request: header: JWT | SessionToken  
  body: { post: }  
  Response: {postId}  
- view post  
  GET /feed -> Post[]
- follow people  
  PUT /users/{id}/follow    

## High-level design
