# Project Description

## Summary
On the internet, there are countless youtubers, self-proclaimed economists making random guesses that cannot be verified for correctness. Their predictions often disappear into the noise, with no way to track whether they were right or wrong. GuessStreet changes that by offering a platform where users can make non-changeable predictions on stocks, crypto, or other markets for a specific date. Every guess is locked in and timestamped, ensuring fairness and accountability.

By creating a transparent record of forecasts, GuessStreet aims to bring trust to the economy predictions space. Whether you’re a casual market watcher or a seasoned trader, you can test your intuition against others, build credibility by proving your accuracy over time, and engage with a community that values verifiable insights over empty claims. On GuessStreet, the market isn’t just about price — it’s about prediction, competition, and trust.

## High-level Features
* Auth-Service
  - Account creation with email & password
  - Email verification with 6 digit code
  - Login with token-based authentication (JWT)
  - Password management:
      - Change password (requires current password)
      - Reset password with 6-digit code
* Prediction-Service
    - Create predictions:
        - Range of values [min, max]
        - Asset ID (stock ticket as seen in **Yahoo Finance**)
        - Target date (<= 2 years)
    - View predictions:
        - User's own predictions (paginated)
        - Another user's predictions (paginated)
        - All predictions for a given asset (paginated)
* Relationship-Service
    - Follow another user
    - Unfollow another user
* Feed-Service
    - Show a **personalized feed** of user + followed predictors' actions
* Guess-Checker-Service features
    - Daily at **3 PM PST**: update predictions ending that day with the actual asset value.
  
## Non-Functional Requirements
* Security
    - JWT for authorization
    - Least-privilege model in AWS Cognito
    - Minimize API/information exposure to external users
* Reliability
    - Exponential backoff on login errors
    - Password reset and recovery mechanisms
* Transparency
    - Predictions are timestamped, immutable, and verifiable
* Scalability
    - Services run as AWS Lambda functions
    - Each service containerized with Docker
* Maintainability
    - Code stored in GitHub
    - Clear role distinction (customers = least privileged, maintainers = highly privileged)

## Constraints
* Must use **AWS** as cloud provider
* Each service must be an **AWS Lambda function**
* Each service must be packaged in a **Docker container**
* Predictions target date must not exceed 2 years
* Users must be authenticated & email verified to make predictions
* All customer roles restriced to least privilege in AWS Cognito
* Tech stack programming language is **not restricted**
