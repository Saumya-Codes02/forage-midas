# 💰 Midas Core

A Spring Boot backend application developed as part of the **JPMorgan Chase Advanced Software Engineering Job Simulation** on Forage.

The project simulates a financial transaction processing system using an event-driven architecture. It consumes transactions from Apache Kafka, validates and persists them, integrates with an external Incentive REST API, and exposes user balances through a REST endpoint.

---

## 🚀 Features

- 📩 Consume transaction messages using Apache Kafka
- ✅ Validate incoming transactions
- 💾 Persist user data using Spring Data JPA
- 🗄️ Store data in an H2 in-memory database
- 🌐 Integrate with an external Incentive REST API
- 💵 Apply incentive amounts to recipient balances
- 🔍 Expose a REST endpoint to query account balances
- 🧪 Automated verification using Maven and JUnit

---

## 🏗️ Architecture

```
                    +----------------+
                    | Kafka Producer |
                    +-------+--------+
                            |
                            ▼
                     Apache Kafka Topic
                            |
                            ▼
                  +---------------------+
                  | Kafka Consumer      |
                  | (Spring Boot)       |
                  +----------+----------+
                             |
               Validate Transaction
                             |
                             ▼
                  +---------------------+
                  | Incentive REST API  |
                  +----------+----------+
                             |
                    Incentive Response
                             |
                             ▼
                  +---------------------+
                  | H2 Database         |
                  | Spring Data JPA     |
                  +----------+----------+
                             |
                             ▼
                 GET /balance?userId={id}
```

---

## 🛠️ Tech Stack

- Java 17
- Spring Boot 3
- Spring Web
- Spring Data JPA
- Apache Kafka
- REST APIs
- RestTemplate
- H2 Database
- Maven
- JUnit 5
- IntelliJ IDEA

---

## 📁 Project Structure

```
src
├── main
│   ├── java
│   │   └── com.jpmc.midascore
│   │       ├── component
│   │       ├── controller
│   │       ├── entity
│   │       ├── foundation
│   │       ├── repository
│   │       ├── KafkaConsumer.java
│   │       ├── KafkaProducer.java
│   │       ├── AppConfig.java
│   │       └── MidasCoreApplication.java
│   └── resources
│       └── application.yml
│
└── test
```

---

## ⚙️ REST API

### Get User Balance

```
GET /balance?userId=9
```

### Response

```json
{
  "amount": 3434.0002
}
```

If the user does not exist:

```json
{
  "amount": 0.0
}
```

---

## 📬 Kafka Message Format

Transactions are published as JSON.

Example:

```json
{
  "senderId": 9,
  "recipientId": 10,
  "amount": 16.0
}
```

---

## 💵 Incentive API

The application integrates with an external REST service.

```
POST http://localhost:8080/incentive
```

Request

```json
{
  "senderId": 9,
  "recipientId": 10,
  "amount": 16
}
```

Response

```json
{
  "amount": 4.0
}
```

---

## ▶️ Running the Project

### Start the Incentive API

```bash
cd services
java -jar transaction-incentive-api.jar
```

### Run Spring Boot

```bash
mvn spring-boot:run
```

The application runs on

```
http://localhost:33400
```

---

## 🧪 Running Tests

Run all tests

```bash
mvn test
```

Run a specific test

```bash
mvn test -Dtest=TaskFiveTests
```

---

## 📚 Concepts Demonstrated

- Event-Driven Architecture
- Message Queues
- Apache Kafka
- Spring Boot
- RESTful APIs
- Dependency Injection
- JSON Serialization
- Spring Data JPA
- Database Persistence
- External API Integration
- Backend System Design

---

## 📖 Learning Outcomes

This project provided practical experience with:

- Building backend services using Spring Boot
- Consuming Kafka messages
- Processing financial transactions
- Working with relational databases
- Designing RESTful APIs
- Integrating third-party services
- Testing and debugging distributed applications

---

## 👨‍💻 Author

**Saumya Shukla**

- GitHub: https://github.com/Saumya-Codes02
- LinkedIn: https://linkedin.com/in/saumya-shukla-0b665032b

---

## 📜 Acknowledgements

Developed as part of the **JPMorgan Chase Advanced Software Engineering Job Simulation** offered through **Forage**.
