# Leaderboard Documentation

## Functional Requirements
    Write an API that would power the leaderboard Screen above (REST)
    ● All users start with 0 points.
    ● As you click +/-, the leaderboard updates and users are re-ordered based on score.
    ● You are able to add users (+) and delete users (x)
    ● When the name is clicked on, UI would show details of this user.
      ○ Name
      ○ Age
      ○ Points
      ○ Address
    ● Create a model factory to fill the db with initial users with random values.
    ● Create an endpoint that returns the users info grouped by score and include the average age of the users in json format.
    ● Create a scheduled job that identifies the user with the highest points at a given moment and stores a new record in a winners table. This table must maintain a relationship with the original users table and store the timestamp when the user was declared a winner and their corresponding points at that time. The job should run every 5 minutes. In cases where there's a tie for the highest points, no winner should be declared, and no record should be created in the winners table.

## Non-Functional Requirements
  1. High availability
  2. Low latency
  3. Scalability
  4. Reliability

## High Level Design
![image](https://github.com/vivekdbit/leaderboard-doc/assets/44405152/e4d30ca7-34c2-421e-a2a2-b9fd57b11ca7)

## Traffic Estimations
1. Number of users: 50 million
2. Daily active users: 10 million
    ```QPS = 10*10^6 / 24*60*60 
    QPS = 10*10^6 / 84600  ( Assume, 86400 ≈ 100000 Sec ) 
    QPS = 10*10^6*10^-5
    QPS ≈ 100
3. At peak considering 10x QPS ≈ 1000
4. Home page leaderboard read queries 1000 RQPS


## Tech Stack
1. Redis Sorted Sets for caching
2. AWS Lambda used for scheduled job
3. React for frontend
4. Python Flask for backend APIs
5. MongoDB for storage

## API Documentation
https://documenter.getpostman.com/view/30759648/2sA3QsAs2E#0b82d441-98f7-4a62-ae85-7ad7d10055f3

## Low Level Design
1. Frontend Repository - https://github.com/vivekdbit/leaderboard_react
2. Backend Repository - https://github.com/vivekdbit/leaderboard

## Deployment
1. Docker container
2. GitHub Actions
3. ECR
4. ECS
5. Route53
