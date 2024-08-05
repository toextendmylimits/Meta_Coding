# Design ticket master
## Requirements
### Functional requirements
- View upcoming events
- Book tickets to upcoming events
- Search for upcoming events

------------out of scope--------
- view booked events
- dynamic pricing for popular events
- admin add/update/delete events

### Non-functional requirements
- High availability for searching and viewing events
- High consitency for booking tickets(no double booking)
- Low latency search
- Scalibility to 10m users, read heavy, read/write ratio 100
- Scalibility to handle surge of popular events

---------------out of scope-----------
- protect user data
- provide secure transcations for payment
- fault tolerant
- 
## Core Entities & API
### Core Entities
- Event
- Venue
- Perfomer
- Ticket
- Booking
### API
- view events GET /events/:eventId -> Event,Venue,Performer,Ticket[]
- book events  
  1.select seat 
    - POST /booking/reserve 
    - Request header: JWT | SessionToken, body: { eventId, seatNo }
    - Response body: {ticketId}

  2.pay ticket
    - PUT /booking/:ticketId/confirm
    - Request header: JWT | SessionToken
    - Response: success/failure, {ticketId,paymentDetais:""}
- search events
- GET /events/search?keyword={keyword}&start={start}&end={end} -> Partial Events[]

## High-level designs

## Design deep dive
- How to avoid double booking?
- How to scale?
- How to handle hot event like Tylor Swift? SSE for seat update, virtual queue for popular event
- How to implement Search? Elastic search
- How to speed up repeated search queries? Cache CDN
