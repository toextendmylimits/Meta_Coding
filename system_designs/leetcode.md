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
 1. User service  
    Responsible for user sign-up, updating, and retrieving user information to be displayed on the user profile page, backed by the user database.
 3. Code evaluation service
    1. The service accepts user-submitted code
    2. enqueues them as messages into a message queue
    3. The workers fetch from the queue, extract the user code and run them against the test cases inside docker containers
    4. The outputs are compared with the expected outputs and the results are sent back to the client. User scores and rankings are also updated based on output comparisons. If user code passes all test cases for a problem, the problem is marked as a success and its corresponding score is added to the user’s total.
    5. User scores and rankings are stored in an in-memory data store, such as Redis. Redis has a built-in data structure called sorted set that is tailored for the leaderboard purpose. We can use (contest_id, user_id) as the key and scores as the value and Redis sorted set will automatically ranks the users by their scores.
 5. Contest service  
    responsible for retrieving contest related information such as questions, date of contest etc from the contest database.

 # Detailed design
 Detailed Design Q&A
Q1: How to prevent users from submitting malicious code that messes up our service internals?

A: Run each test case inside sandboxes like Docker containers and only allow the containers to access temporary storage (e.g., Linux's /tmp folder). We'd use docker containers while limiting network access, setting CPU and memory bounds, and enforcing a timeout on the code execution

Q2: In what format should the test cases be stored and how should they be used?

A: Each test case has an input file and an expected output file. Each problem has a driver code for each language that parses the input file. When user submitted code is executed by the docker container, an output file is created in a temporary folder mounted on the container. The output file can be compared to the expected output file for correctness.

# Reference
1. https://www.hellointerview.com/learn/system-design/answer-keys/leetcode
2. https://systemdesignschool.io/problems/leetcode/solution
