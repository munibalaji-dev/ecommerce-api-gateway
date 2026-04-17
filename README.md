# API Gateway - E-Commerce Microservices

##  Overview
This project is an API Gateway built using **Spring Cloud Gateway** for an E-Commerce Microservices system.

It acts as a **single entry point** for all client requests and routes them to respective microservices:
- Customer Service
- Product Service
- Order Service

---

##  Features
- Centralized entry point for all microservices
- Request routing based on URL patterns
- Microservice abstraction (client does not access services directly)
- Easy scalability and maintainability
- Built using Spring Cloud Gateway

---

##  Architecture

Client → API Gateway → Microservices

- Customer Service (3001)
- Product Service (3002)
- Order Service (3003)

---

##  Tech Stack
- Java 21
- Spring Boot
- Spring Cloud Gateway
- Maven

---

##  Gateway Port
http://localhost:9000

---

##  Route Configuration

| Service | Route | Target |
|--------|------|--------|
| Customer Service | /api/v1/customers/** | http://localhost:3001 |
| Product Service | /api/v2/products/** | http://localhost:3002 |
| Order Service | /api/v3/orders/** | http://localhost:3003 |

---

##  application.yml

```yaml id="gwyaml1"
server:
  port: 8080

spring:
  application:
    name: API-GATEWAY

  cloud:
    gateway:
      server:
        webmvc:
          routes:
            - id: customer-service
              uri: http://localhost:3001
              predicates:
                - Path=/api/v1/customers/**

            - id: product-service
              uri: http://localhost:3002
              predicates:
                - Path=/api/v2/products/**

            - id: order-service
              uri: http://localhost:3003
              predicates:
              - Path=/api/v3/orders/**
---------------------------
##  How to Run

### 1. Start microservices first
- Customer Service (3001)
- Product Service (3002)
- Order Service (3003)

### 2. Start API Gateway
- Run Spring Boot application

### 3. Access APIs through Gateway
--------------------------
##  API Testing Examples

### Customer Service
GET http://localhost:8080/api/v1/customers/1

### Product Service
GET http://localhost:8080/api/v2/products/1

### Order Service (Aggregation)
GET http://localhost:8080/api/v3/orders/1/details
--------------------------
## Key Concepts Used

- Spring Cloud Gateway for routing
- Microservice architecture
- REST API design
- Service decoupling
- Centralized entry point pattern
--------------------------
##  Future Enhancements

- Eureka Service Discovery
- JWT Authentication & Authorization
- Rate Limiting
- Circuit Breaker (Resilience4j)
- Centralized Logging
