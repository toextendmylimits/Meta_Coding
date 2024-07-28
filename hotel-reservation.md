# Design hotel reservation system
## Requirements
### Functional Requirements
- Admin add/remove/update hotels or rooms
- View hotels and rooms
- Book a room

---------------out of scope------------------
- dynamic pricing
- search rooms by filter

### Scale
1m rooms

### Non-functional requirments
- strong consitency for booking
- high availability for view
- Low latency
- Scalability

----------------out of scope-----------------
- data privacy

## Core Entities and APIs
### Core Entities
- User
- Admin
- Hotel
- Room
- Booking

### APIs
- Admin
- View
- Booking 
  POST /reservations
## High-level design

## Deep dive
- no double booking
- data sharding and replication
