# HBnB – Technical Documentation  

## TASK 0 - High-Level Package Diagram  

---

## Overview  
This document presents a high-level package diagram of the HBnB Evolution application. It describes a three-layer architecture and illustrates how these layers communicate using the Facade design pattern.  

The purpose of this documentation is to provide a clear understanding of the system structure, its components, and how different parts interact with each other.

---

## Architecture Overview  
The HBnB application is designed using a layered architecture consisting of three main layers:  

1. Presentation Layer  
2. Business Logic Layer  
3. Persistence Layer  

Each layer has a specific responsibility and interacts with other layers in a structured and controlled manner.

---

## Layer Descriptions  

### 1. Presentation Layer  
This layer represents the interface between the user and the system. It includes API endpoints and services that handle incoming user requests.  

When a user performs an action, the request is received in this layer and passed through the Facade.

---

### 2. Business Logic Layer  
This layer contains the core logic of the application. It includes the main entities:  

- User  
- Place  
- Review  
- Amenity  

Responsibilities include applying business rules, validating data, and controlling application behavior.

---

### 3. Persistence Layer  
This layer is responsible for storing and retrieving data from the database.  

It includes:  
- UserRepository  
- PlaceRepository  
- ReviewRepository  
- AmenityRepository  

---

## Facade Pattern  

The Facade acts as an intermediary between layers and provides a unified interface.

### Benefits:  
- Single entry point  
- Reduced complexity  
- Improved maintainability  

---

## Package Diagram  

```mermaid
classDiagram

class PresentationLayer {
    +API Endpoints
    +Services
}

class Facade {
    +createUser()
    +getPlaces()
    +createReview()
    +createAmenity()
}

class BusinessLogicLayer {
    +User
    +Place
    +Review
    +Amenity
}

class PersistenceLayer {
    +UserRepository
    +PlaceRepository
    +ReviewRepository
    +AmenityRepository
}

PresentationLayer --> Facade : Sends requests
Facade --> BusinessLogicLayer : Processes logic
BusinessLogicLayer --> PersistenceLayer : Performs data operations

# TASK 1 - Business Logic Layer

## Objective  
Design a detailed class diagram for the Business Logic layer of the HBnB application.  
The diagram should clearly represent the main entities, their attributes, methods, and relationships.

---

## Overview  

This section describes the **Business Logic Layer** of the HBnB application. It provides a UML class diagram that models the core entities of the system and their interactions.  

The goal is to present a clear and structured representation of how the business logic operates and how entities relate to each other.

---

## Business Logic Layer  

The Business Logic Layer contains the core entities of the application:  

- User  
- Place  
- Review  
- Amenity  

These entities are responsible for implementing business rules, managing data validation, and defining system behavior.

Each entity includes:  
- A unique identifier (UUID)  
- Creation and update timestamps  
- Methods that define its behavior  

---

## Class Diagram  

```mermaid
classDiagram
    class BaseModel {
        +UUID id
        +DateTime created_at
        +DateTime updated_at
        +save()
        +update(data)
    }

    class User {
        +String first_name
        +String last_name
        +String email
        +String password
        +Boolean is_admin
        +register()
        +update_profile()
        +delete()
    }

    class Place {
        +String title
        +String description
        +Float price
        +Float latitude
        +Float longitude
        +UUID owner_id
        +create()
        +update()
        +delete()
    }

    class Review {
        +Int rating
        +String comment
        +UUID place_id
        +UUID user_id
        +create()
        +update()
        +delete()
    }

    class Amenity {
        +String name
        +String description
        +create()
        +update()
        +delete()
    }

    %% Inheritance
    User --|> BaseModel
    Place --|> BaseModel
    Review --|> BaseModel
    Amenity --|> BaseModel

    %% Relationships
    User "1" --> "0..*" Place : owns
    Place "1" --> "0..*" Review : has
    User "1" --> "0..*" Review : writes
    Place "0..*" -- "0..*" Amenity : includes