# Financial Transaction Management System

This repository contains a microservices-based application for managing transactions using Spring Boot and Kafka. The system consists of two microservices:

1. **Transaction Service**: Handles CRUD operations for transactions and publishes transaction events to Kafka.

## Technologies Used

- **Spring Boot**: For building the microservices.
- **Spring Kafka**: For integrating with Apache Kafka.
- **Spring Data JPA**: For data persistence with H2 Database.
- **JUnit 5**: For unit testing.
- **H2 Database**: In-memory database for storing transaction data.

## Setup Instructions

### Prerequisites

- Java 8 or higher installed.
- Apache Kafka installed and running locally on default port `9092`.
- Maven installed to build and run the applications.

### Running the Applications

1. **Start Apache Kafka**: Start Zookeeper and Kafka server.

   ```bash
   # Start Zookeeper
   bin/zookeeper-server-start.sh config/zookeeper.properties

   # Start Kafka server
   bin/kafka-server-start.sh config/server.properties
   ```

2. **Create Kafka Topic**: Create a Kafka topic named `transaction-topic`.

   ```bash
   bin/kafka-topics.sh --create --topic transaction-topic --bootstrap-server localhost:9092 --partitions 1 --replication-factor 1
   ```


### Usage

- **Transaction Service** exposes REST APIs for CRUD operations on transactions:
  - POST `/transactions/create`: Create a new transaction.
  - GET `/transactions/{id}`: Retrieve a transaction by ID.
  - PUT `/transactions/{id}`: Update an existing transaction.
  - DELETE `/transactions/{id}`: Delete a transaction by ID.

- **Notification Service** listens to Kafka topic `transaction-topic` and processes transaction events for notifications.

### Testing

- Unit tests are provided for the `TransactionService` in `transaction-service`.
- Mocking with Mockito is used for dependencies like KafkaTemplate and TransactionRepository.

### Configuration

- Kafka configuration is specified in `application.properties` files in both services.
- H2 Database configuration is also managed in `application.properties`.
