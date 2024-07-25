# System design for web crawler

## Requirements
### Functional requirements
- crawl the full web starting froms seed urls
- extract the text data and store  
--------------out of scope-------------  
- handle non-text data(image,video)
- handle dynmaic content

### Scale
- 10B web pages
- 2MB per page
- 5 days to finish

### Non-functional requirements
- Fault tolerant
- Politeness
- Scale to 10B pages
- Efficient  
-----------out of scope------------
- compliance to adhere to legal requirements and privacy regulations
- cost to operatet the system within budget constraints

## Core Entities, API & Interfaces
### Core Entities
- Text data
- URL metadata
- Domain metadata
### Interface
- input: seed urls
- output: text data

## Data workflow
1. Take seed urls from frontier and request DNS for IP address
2. Download HTML
3. Extract text from HTML
4. Save text data in database
5. Extract URLs from the text and add to frontier
6. Repeat steps 1-5 until all URLs have been crawled
