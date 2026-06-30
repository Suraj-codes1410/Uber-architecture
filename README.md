# 🚖 Uber Architecture - Microservices Backend

A production-inspired Uber backend built using **Java, Spring Boot, Kafka, MySQL, Redis, and Spring Cloud** following a **Microservices Architecture**.

This project demonstrates how large-scale ride-hailing platforms handle ride requests, driver matching, real-time location updates, and event-driven communication between independent services.

---

# ✨ Features

- Microservices Architecture
- Event-Driven Communication using Apache Kafka
- REST APIs
- Driver Matching Algorithm
- Real-time Driver Location Tracking
- MySQL Persistence
- Redis Geospatial Search
- Spring Cloud OpenFeign
- Spring Data JPA
- DTO Layer
- Kafka Producers & Consumers
- Clean Layered Architecture

---

# 🏗 Architecture

```
                   Client
                      │
                      ▼
              Ride Service
                      │
          RideRequestedEvent
                      │
                      ▼
                Apache Kafka
                      │
                      ▼
            Matching Service
                      │
      Fetch Nearby Drivers (Feign)
                      │
                      ▼
            Location Service
                      │
        Redis GEO Search Engine
                      │
                      ▼
            Matching Service
                      │
          RideMatchedEvent
                      │
                      ▼
                Apache Kafka
                      │
                      ▼
              Ride Service
                      │
                      ▼
            Ride Updated Successfully
```

---

# 📦 Microservices

## 🚖 Ride Service

Responsible for

- Creating rides
- Managing ride lifecycle
- Fare estimation
- Publishing RideRequestedEvent
- Consuming RideMatchedEvent
- Updating ride status

### APIs

```
POST   /api/v1/rides/request

GET    /api/v1/rides/{rideId}

GET    /api/v1/rides/rider/{riderId}

PUT    /api/v1/rides/{rideId}/start

PUT    /api/v1/rides/{rideId}/complete

PUT    /api/v1/rides/{rideId}/cancel
```

---

## 🚗 Matching Service

Responsible for

- Consuming RideRequestedEvent
- Finding nearby drivers
- Driver scoring algorithm
- Selecting the best driver
- Publishing RideMatchedEvent

### Driver Selection

Drivers are ranked using:

```
Score =
(1 / Distance) × 70%
+
Driver Rating × 30%
```

Closest driver with highest score is assigned.

---

## 📍 Location Service

Responsible for

- Driver location updates
- Nearby driver search
- Redis GEO indexing
- Geospatial radius queries

### APIs

```
POST /api/v1/locations/update

GET  /api/v1/locations/drivers/nearby
```

---

# 📡 Event Flow

## Ride Requested

```
Client

↓

Ride Service

↓

Save Ride

↓

Publish RideRequestedEvent

↓

Kafka

↓

Matching Service

↓

Find Drivers

↓

Publish RideMatchedEvent

↓

Kafka

↓

Ride Service

↓

Ride Assigned
```

---

# 🛠 Tech Stack

### Backend

- Java 21
- Spring Boot
- Spring Data JPA
- Spring Web
- Spring Validation
- Spring Cloud OpenFeign

### Messaging

- Apache Kafka

### Database

- MySQL

### Cache / Geo Search

- Redis

### Build Tool

- Maven

### Utilities

- Lombok

---

# 📂 Project Structure

```
uber-architecture/

│

├── ride-service/

│     ├── controller

│     ├── service

│     ├── repository

│     ├── dto

│     ├── event

│     ├── model

│     └── config

│

├── matching-service/

│     ├── consumer

│     ├── service

│     ├── client

│     ├── dto

│     ├── event

│     └── config

│

├── location-service/

│     ├── controller

│     ├── service

│     ├── repository

│     ├── model

│     └── config

│

└── docker-compose.yml
```

---

# 🚀 Getting Started

## Clone

```bash
git clone https://github.com/yourusername/uber-architecture.git
```

```
cd uber-architecture
```

---

## Start Infrastructure

Start

- Kafka
- Zookeeper (if required)
- MySQL
- Redis

using Docker.

```bash
docker compose up -d
```

---

## Run Services

### Ride Service

```bash
cd ride-service
mvn spring-boot:run
```

Runs on

```
localhost:8083
```

---

### Matching Service

```bash
cd matching-service
mvn spring-boot:run
```

Runs on

```
localhost:8084
```

---

### Location Service

```bash
cd location-service
mvn spring-boot:run
```

Runs on

```
localhost:8082
```

---

# 📬 Sample Ride Request

```json
{
  "riderId": "RIDER001",
  "pickupLatitude": 28.6139,
  "pickupLongitude": 77.2090,
  "pickupAddress": "Connaught Place",

  "dropLatitude": 28.5355,
  "dropLongitude": 77.3910,
  "dropAddress": "Noida"
}
```

---

# 🔄 Ride Lifecycle

```
REQUESTED

↓

MATCHING

↓

ACCEPTED

↓

RIDE_STARTED

↓

COMPLETED
```

or

```
REQUESTED

↓

CANCELLED
```

---

# 📈 Future Enhancements

- API Gateway
- Service Discovery (Eureka)
- Authentication & Authorization (JWT)
- Driver Service
- Payment Service
- Notification Service
- Surge Pricing Engine
- Trip History Service
- Kubernetes Deployment
- Prometheus & Grafana Monitoring
- Distributed Tracing (Zipkin)

---

# 🎯 Learning Outcomes

This project demonstrates:

- Microservices Design
- Event-Driven Architecture
- Kafka Messaging
- Distributed Systems
- Inter-Service Communication
- REST API Design
- Redis GEO Search
- Database Modeling
- Clean Code Principles
- Layered Architecture
- Spring Boot Best Practices

---

# 👨‍💻 Author

**Suraj Samanta**

- LinkedIn: https://linkedin.com/in/suraj-samanta1410
- GitHub: https://github.com/Suraj-codes1410

---

## ⭐ If you found this project helpful, consider giving it a star!
