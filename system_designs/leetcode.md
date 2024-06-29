System design of leetcode/hackerank code contest platform

# Requirements
## Func
1. User can solve question, submit solution, run test cases
2. User can take contests
3. Users are ranked by problems solved and time it took
4. Realtime leaderboard show top users

## Scalability requirements
10k concucurrent users
1 contest a day, last 2 hours
User submit 20 times for solution
Each problem has 20 test cases
User-submitted code retained for one month

## Non-func
1. Low latency: The leaderboard should be updated live
2. High availability: Code submission should be avaiable at all times
3. Security: user-submitted code should not pose a thread to the service

# Resource estimation
Storage for code: 1k, Read: Write, 100: 1,
QPS: 10k users * 20 times * 20 test / 2 hours = 4 million / 7600 = 500 QPS
Storage: User submission: 10k users * 20 submissions * 100kB = 20 G a day, a month 600G  
        Test data: 200k submssions * 20 test * 10kB = 40 GB day, a month: 1.2T  

# API
1. POST /problems/{problemId}/sumbit, reqeust: userId, code, lanuage response: status, test_case: 
2. GET /contests/{contestId}/leaderboard, response: ranking

# High-level design

    
 ![Screen Shot 2024-06-29 at 10 54 04 pm](https://github.com/toextendmylimits/Meta_Coding/assets/10056698/bfa7f765-6050-4ae3-b527-8a268947d572)
 
   
