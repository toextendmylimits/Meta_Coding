# Systemd design for facebook status search
## Requirements
### Functional requirements
- User can post status & only has one status
- Search facebook posts by status of multiple words  

---------------out of scope------------
- search friends posts only
- Rank posts
- search image

### Non-functional requirements
- High availability, eventual consistency 10s
- Low latency for search 200ms
- Scalability   
   write: 10B status, 5 words/status, TPS: 10^5/s, storage 500GB per day  
   read: TPS: 10^6/s,   
   index size: 20k english word and status ids, 1B * 50byte = 50G   
   document size: 1Bpost * 200byte= 200G

------------out of scope --------------------
- protect against bad content

## APIs
- search
  GET /search/keyword, User & Status,
- post status  
  POST /statues

## High-level design
