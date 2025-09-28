# Domain Model

This document describes the domain model of Guess Street. It shows the classes in the system along with their attributes and their relationships, made with Mermaid syntax.

## Class Diagram

```mermaid 
classDiagram

class RegularUser {
    +userID : UUID
}

class AuthenticatedUser {
    +email : String
    +username : String
    +passwordHash : String
    +isVerified : Boolean
}

class Predictor {
    +credibilityScore : Float
}

class Admin {
    +adminId : UUID
    +permissions : String[]
}

class VerificationCode {
    +code : String
    +expiry : DateTime
}

class Prediction {
    +predictionId : UUID
    +assetId : String
    +minValue : Float
    +maxValue : Float
    +targetDate : Date
    +status : String
    +actualValue : Float
}

class Asset {
    +assetId : String
    +name : String
    +type : String
}

class Relationship {
    +relationshipId : UUID
    +followerId : UUID
    +followedId : UUID
}

class FeedItem {
    +feedId : UUID
    +timestamp : DateTime
    +actionType
}

%% Inheritance (IS-A)
RegularUser <|-- AuthenticatedUser
AuthenticatedUser <|-- Predictor
RegularUser <|-- Admin

%% Relationships
AuthenticatedUser "1" --> "*" VerificationCode : recieves
Predictor "1" --> "*" Prediction : makes
Prediction "*" --> "1" Asset : about
AuthenticatedUser "1" --> "*" Relationship : follows
Relationship "*" --> "1" Predictor : followed
  %% 1 appears behind class
Predictor "1" --> "*" FeedItem : creates
```