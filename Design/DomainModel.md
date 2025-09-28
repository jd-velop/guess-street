# Domain Model

This document describes the domain model of Guess Street. It shows the classes in the system along with their attributes and their relationships, made with Mermaid syntax.

## Class Diagram

```mermaid 
classDiagram

class RegularUser {
    +userId : UUID
}

class AuthenticatedUser {
    +email : String
    +username : String
    +passwordHash : String
    +isEmailVerified : Boolean
    +createdAt : DateTime
    +lastLoginAt : DateTime
}

class Predictor {
    +credibilityScore : Float
    +totalPredictions : Int
    +correctPredictions : Int
    +updateCredibilityScore() : void
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
    +userId : UUID
    +minValue : Float
    +maxValue : Float
    +createdAt : DateTime
    +targetDate : DateTime
    resolvedAt : DateTime
    +status : String
    +actualValue : Float
    +isCorrect : Boolean
    +checkIfCorrect() : Boolean
    +resolve(actualValue : float) : void
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
    +createdAt : DateTime
}

class FeedItem {
    +feedId : UUID
    +userId : UUID
    +timestamp : DateTime
    +actionType : ActionType
    +relatedEntityId : UUID
    +description : String
}

%% relatedEntityId is a UUID field that references the object that the feed item ActionType is related to
    %% PREDICTION_CREATED & PREDICTION_RESOLVED for example would contain the predictionId of the prediction
    %% User-related ActionTypes contain the userId

class ActionType {
    <<enumeration>>
    PREDICTION_CREATED
    PREDICTION_RESOLVED
    USER_FOLLOWED
    USER_UNFOLLOWED
    ACCOUNT_CREATED
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
AuthenticatedUser "1" --> "*" FeedItem : creates
FeedItem "*" --> "1" ActionType : has
```

