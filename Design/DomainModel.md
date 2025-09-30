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

## Class Descriptions

### RegularUser
Represents the default user in the system with only the essential user ID. Serves as the parent class for all user types.

### AuthenticatedUser
Represents a user who has completed the authentication process and can log into the system. Contains credentials, email verification status, and timestamps for creation and last login.

### Predictor
A specialized authenticated user who has made at least one prediction. Tracks performance metrics including credibility score, total predictions made, and accuracy statistics to build reputation on the platform over time.

### Admin
System administrator with permissions to manage the platform. Can perform system-level operations beyond regular user capabilities. 

### VerificationCode
Temporary codes used for email verification and password reset processes. Each code has an expiration time.

### Prediction
Rrepresents a user's prediciton for a specific asset. Contains the prediction range, target date, resolution status, and actual outcome when the prediction period ends.

### Asset
Represents tradeable financial assets (stocks, crypto, commodities) that users can make predictions about. Uses Yahoo Finance ticker symbols.

### Relationship
Represents the social following connections between users. Tracks who follows whom and when the relationship was made.

### FeedItem
Entries in a user's feed showing actions performed by the user, or people they follow. Contains metadata about the action type and references to the related entities that triggered the feed entry.

### ActionType
Enumeration defining the different types of activities that can generate feed items. Includes prediction creation/resolution, user following/unfollowing, and account creation.

