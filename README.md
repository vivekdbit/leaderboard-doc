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
  1. High Availability
  2. Low Latency
  3. Scalability
  4. Reliability

## High Level Design
![image](https://github.com/vivekdbit/leaderboard-doc/assets/44405152/5075fc1c-b350-4e05-b4ac-9946814358d0)


## Traffic Estimations
1. Number of users: 50 million
2. Daily active users: 10 million
3. Read Query Per Second (RQPS)
    ```QPS = 10*10^6 / 24*60*60 
    QPS = 10*10^6 / 84600  ( Assume, 86400 ≈ 100000 Sec ) 
    QPS = 10*10^6*10^-5
    QPS ≈ 100
   At peak considering 10x QPS ≈ 1000
   Home page leaderboard read queries 1000 RQPS
    ```
4. Write Query Per Second (WQPS)
    Average 1 customer votes for 5 users
    ```
    QPS = 5 * 10*10^6 / 84600  ( Assume, 86400 ≈ 100000 Sec ) 
    QPS = 5* 10*10^6*10^-5
    QPS ≈ 500
    At peak considering 10x QPS ≈ 5000
    WQPS ≈ 5000
    ```
5. Read:Write = 1:5

## Data Model (Schema)
![image](https://github.com/vivekdbit/leaderboard-doc/assets/44405152/452957c2-e2b4-4b82-be2e-bbec77fb5f42)

## Tech Stack
1. React for frontend
2. Python Flask for backend APIs
3. MongoDB for storage
4. AWS Lambda is used for scheduled job

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
