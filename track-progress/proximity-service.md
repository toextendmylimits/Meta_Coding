# Design proximity service
## Requirements
### Functional requirements
- search based on location, radius, and points of interest
- view the business
- business owners add/update/delete business

--------------out of scope----------
- review/ratings
- fuzzy search

### Scale
10m users, 200m business

### Non-functional requirements
- high availability, eventual consistency
- low latency for search/view
- scalability

---------------out of scope---------------
- data privacy

## Core Entities & APIs
### Core Entities
- Clients/Users
- Buisness Owners
- Location

### APIs
- search  
  GET /search/nearby?keyword,latitude,longtitude,radius  
  a list of business  
- view
  GET /businesses/{id}
- business owners  
  POST /businesses  
  PUT /businesses/{id}  
  DELTE /businesses/{id}   

## High-level designs
