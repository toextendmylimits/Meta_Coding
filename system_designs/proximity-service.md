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

## Design deep dive
geohash vs quad tree
- Geohash
  1. Easy to implement
  1. Supports returning businesses within a specified radius.
  1. When the precision (level) of geohash is fixed, the size of the grid is fixed as well. It cannot dynamically adjust the grid size, based on population density. More complex logic is needed to support this.
  1. Updating the index is easy.
- QuadTree
  1. Slightly harder to implement because it needs to build the tree.
  2. Supports fetching k-nearest businesses.
  3. It can dynamically adjust the grid size based on population density
  4. Updating the index is more complicated than geohash
