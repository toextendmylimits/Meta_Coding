# System design for Uber
## Requirements
### Functional requirements
1. Users can enter location and destination, and get fare estimate
2. Users can request a ride
3. Drivers can accept trade and navigate to pick up/drop off

-----------out of scope----------------  
1. Rating
2. Multiple car types
3. Schedule in advance

### Non-functional requirements
1. Low latency for matching < 1 min or failure
2. Consistency matching ride to drive, 1 : 1
3. highl availability
4. High throughput, handle surge in peak hours or special events

----------out of scope------------------  
- protect user privacy
- monitoring, alerting

## Core Entities and APIs
### Core Entities
- Rider
- Ride
- Driver
- Location

### APIs
1. Estimate fare  
   POST /fare-estimate  -> Partial<Ride> {rideId, price, eta}
    { location, destination}
2. Request a ride  
   PATCH /rides/request -> success/failure  
   { rideId }
3. Update driver location -> success  
   POST /drivers/location/update  
   Request: JWT | SessionToken  
   {latitude,longtitude}  
4. Accept ride
   POST /rides/accept  
   Request: {rideId:}  
   Response: {status,latitude,longtitude}  
5. Ride status update
   PATCH /rides/status/update  
   Request: { rideId, status:pickedup | completed}     
