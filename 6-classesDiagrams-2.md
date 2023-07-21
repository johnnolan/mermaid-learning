# Section 6

```mermaid
---
title: Classes Diagram 2
---
classDiagram
    class UserController {
        -ICreateUserService _createUserService
        +UserController(CreateUserService createUserService)
        +Create(string email, string username) User
    }

    class CreateUserRequest {
        +string Email
        +string Username

        +Validate() bool
    }

    class ICreateUserService {
        <<Interface>>
        +Call(CreateUserRequest createUserRequest) User
    }

    class CreateUserService {
        -UserModel _userModel
        -SendWelcomeEmailService _sendWelcomeEmailService
        -Kafka _kafka
        +CreateUserService(UserModel um, SendWElcomeEmailService es, Kafka k)
        +Call(ICreateUserService createUserRequest) User
        -CheckActiveUsers(List-User- users) bool
    }

    class UserModel {
        +FindUsersByEmail(string email) List-User-
        +CreateUser(CreateUserRequest createUserRequest) User
    }

    class User {
        +int UserId
        +string Username
        +string Email
    }

    class SendWelcomeEmailService {
        +Call(User user) bool
    }

    class Kafka {
        +PublishUserCreatedEvent(User user) bool
    }

    UserController ..> ICreateUserService: depends on
    UserController ..> CreateUserRequest: depends on
    CreateUserService ..> ICreateUserService: implements
    CreateUserService ..> UserModel: depends on
    UserModel ..> User: depends on
    CreateUserService ..> SendWelcomeEmailService: depends on
    CreateUserService ..> Kafka: depends on

```
