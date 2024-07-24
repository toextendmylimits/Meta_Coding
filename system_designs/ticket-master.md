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
    - Response body: {bookingId, ticketIds:[]}

  2.pay ticket
    - PUT /booking/:bookingId/confirm
    - Request header: JWT | SessionToken
    - Response: success/failure, {ticketIds:[],paymentDetais:""}
- search events
- GET /events/search?keyword={keyword}&start={start}&end={end} -> Partial Events[]
