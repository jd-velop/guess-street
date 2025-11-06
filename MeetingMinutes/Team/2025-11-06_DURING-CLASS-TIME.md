# Week of 11/03/2025 - 11/09/2025

## Meeting Start Time
2025/11/06 11:05 AM

## Meeting End Time
2025/11/06 11:55 AM

## Location/Medium
Bracken Rm 409 and over Discord

## Present
JD, Elaine, Braxton (In Person) - Ryan (Online)

## Minute Recorder
Elaine

## Topics Discussed
- Two things that need to be done urgently: Dockerizing the code/updating the development.md and making the cloud database always accessible regardless of IP address.
- We need to make sure that GitHub actions works with our unittests in Python.
- We need to implement modularity -- how are we going to do that? Still unsure.

## Things Clarified
- Our code is relatively clean, but we need to go through and make sure that it is.
- Thinking that UserPredictions should be a superclass and the parent class of ValidatedPredictions so that there aren't overlapping/repeated methods.
- 

## Progress Made
- Cloud database is closer to being able to be accessed without your specific IP address being the same every single time.
  - We're all creating Google Cloud accounts and then sending our emails to Ryan so that we can get this rolling.
- UserPredictions is now a superclass and ValidatedPredictions is now a child class -- still making sure it works (lives in
