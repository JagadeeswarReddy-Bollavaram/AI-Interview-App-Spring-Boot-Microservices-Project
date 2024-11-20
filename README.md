# AI Interview App - Spring Boot Microservices Project

## Overview
This project demonstrates a microservices-based architecture using Spring Boot. It includes the following services:
- **Eureka Server**: A service registry for managing microservice discovery.
- **API Gateway**: Acts as a single entry point for routing requests to backend microservices.
- **User Service**: Handles user authentication and registration using MySQL.
- **Interview Service**: Manages interview sessions and user-specific interview data using MongoDB.

## Project Structure
A Spring Boot multi-module backend application that powers an AI-based interview platform. This backend is designed to manage user accounts, interview sessions, and other related services, with data stored in MySQL and MongoDB. User Service: Manages user authentication, profile information, and account data using MySQL.
Interview Service: Handles interview session data, including tracking, managing, and storing interviews, using MongoDB.
Microservices Architecture: Built with Spring Boot, with modules for user management and interview management.


├── eureka-server # Service Registry ├── gateway # API Gateway for routing ├── user-service # Handles user authentication and registration ├── interview-service # Manages interview sessions and user-related data


## Setup and Configuration

### Prerequisites
- **Java 17** (or compatible version)
- **MySQL** (Ensure MySQL is running)
- **MongoDB** (Ensure MongoDB is running)
- **Maven** (For building the project)

### Clone the Repository
```bash
git clone <repository_url>
cd <project_directory>
```

## Configuration Files


### Gateway (application.properties)
```
spring.application.name=Gateway
server.port=8080

spring.cloud.gateway.discovery.locator.enabled=true
```

### Eureka Server (application.properties)

```
spring.application.name=EurekaServer
server.port=8761
eureka.client.fetchRegistry=false
eureka.client.registerWithEureka=false
```

### User Service (application.properties)

```
spring.application.name=user service 
server.port=8081

spring.datasource.url=jdbc:mysql://localhost:3306/AiInterviewApp?createDatabaseIfNotExist=true
spring.datasource.username=root
spring.datasource.password=*******
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver
spring.jpa.hibernate.ddl-auto=update
spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.MySQL8Dialect
spring.jpa.show-sql=true
server.error.include-message=always

eureka.client.serviceUrl.defaultZone=http://localhost:8761/eureka
eureka.client.fetchRegistry=true
eureka.client.registerWithEureka=true
eureka.instance.hostname=localhost

```

### Interview Service (application.properties)

```
spring.application.name=interview service 
server.port=8082

server.error.include-message=always
spring.data.mongodb.uri=mongodb://localhost:27017/aiInterview

eureka.client.serviceUrl.defaultZone=http://localhost:8761/eureka
eureka.client.fetchRegistry=true
eureka.client.registerWithEureka=true
eureka.instance.hostname=localhost

```
##Service Details and Endpoints

### Endpoints

#### User Service
| HTTP Method | URL           | Description               |
|-------------|---------------|---------------------------|
| POST        | `/api/v1/register` | Register a new user.      |
| POST        | `/api/v1/login`    | Login and generate JWT token. |

#### Interview Service
| HTTP Method | URL                                | Description                          |
|-------------|------------------------------------|--------------------------------------|
| POST        | `/api/v2/register`                | Register a new user.                |
| GET         | `/api/v2/interview/userDetails`   | Retrieve user details.              |
| POST        | `/api/v2/interview/saveSession`   | Save a new interview session.       |
| GET         | `/api/v2/interview/sessions`      | Retrieve all interview sessions.    |
| GET         | `/api/v2/interview/session/{id}`  | Retrieve a specific interview session. |
| DELETE      | `/api/v2/interview/deleteSession/{id}` | Delete a specific interview session. |


## Steps to Run the Application

### Start Eureka Server
```bash
cd eureka-server
mvn spring-boot:run
```

### Start Gateway
```bash
cd gateway
mvn spring-boot:run

```

### Start User Service
```bash
cd user-service
mvn spring-boot:run

```

### Start Interview Service
```bash
cd interview-service
mvn spring-boot:run

```
##Future Enhancements
- Add API documentation using Swagger.
- Implement role-based access control.
- Introduce monitoring and logging using Spring Boot Actuator and ELK Stack.
- Containerize the application using Docker.
