# Sysem design for leaderboard
## Requirements
### Functional requirements
- Display top 10 users on the leaderboard
- Show a user's specific rank
- Display users who are a few places above and below the desired user(bonus)

### Scale
5m DAU, 10 matches, check top 10 once a day

### Non-functional requirements
- real time update for scores and ranking
- scalability
- high availability
- eventual consistency

## APIs
- get top 10    
  GET /scores  
- get own score  
  GET /scoresById  
  Reqeust: JWT | SessionToken that has userId  
- add a score  
  POST /scores
## High-level design

## Data models  
userId,  
score  

SQL databases are not performant when we have to process large amounts of continuously changing information.   
Attempting to do a rank operation over millions of rows is going to take 10s of seconds, which is not   
acceptable for the desired real-time approach. Since the data is constantly changing, it is also not feasible to consider a cache.

Redis solution  
Sorted set

## Deep dive
