# 🏋️ Fitness Tracker - Spring Boot Backend

![Java](https://img.shields.io/badge/Java-17+-orange?style=for-the-badge&logo=java)
![Spring Boot](https://img.shields.io/badge/Spring%20Boot-3.x-brightgreen?style=for-the-badge&logo=springboot)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-Neon-blue?style=for-the-badge&logo=postgresql)
![Docker](https://img.shields.io/badge/Docker-Containerized-2496ED?style=for-the-badge&logo=docker)
![Render](https://img.shields.io/badge/Deployed%20on-Render-46E3B7?style=for-the-badge&logo=render)

A fully production-ready **Fitness Tracker REST API** built with **Java Spring Boot**, secured with **JWT Authentication**, connected to a **PostgreSQL (Neon)** cloud database, deployed on **Render**, and containerized with **Docker**.

---

## 🌐 Live Deployment

| Service | URL |
|---|---|
| 🚀 Backend API (Render) | [https://fitness-monolith-8ecy.onrender.com](https://fitness-monolith-8ecy.onrender.com) |
| 🗄️ Database | PostgreSQL on [Neon](https://neon.tech) (Cloud) |

> ⚠️ **Note:** The server may take **30–60 seconds** to respond on first request since Render free tier spins down after inactivity. Please be patient!

---

## 📌 Table of Contents

- [About the Project](#-about-the-project)
- [Tech Stack](#-tech-stack)
- [Features](#-features)
- [Database Migration](#-database-migration-mysql--postgresql)
- [Project Structure](#-project-structure)
- [API Endpoints](#-api-endpoints)
- [Environment Variables](#-environment-variables)
- [How to Use — 3 Ways](#-how-to-use--3-ways)
  - [1. Via GitHub (Run Locally)](#1-via-github-run-locally)
  - [2. Via Docker Hub](#2-via-docker-hub)
  - [3. Via Render (Live API)](#3-via-render-live-api)
- [Docker Details](#-docker-details)
- [Contributing](#-contributing)
- [Author](#-author)

---

## 📖 About the Project

The **Fitness Tracker Backend** is a monolithic REST API application that helps users track their fitness activities. It supports secure user registration and login using JWT tokens, and provides endpoints to manage fitness-related data. The application was initially built using **MySQL** and later migrated to **PostgreSQL** to support cloud deployment on **Render** with **Neon** as the database provider.

---

## 🛠️ Tech Stack

| Layer | Technology |
|---|---|
| Language | Java 17+ |
| Framework | Spring Boot 3.x |
| Security | Spring Security + JWT |
| ORM | Spring Data JPA / Hibernate |
| Database (Local/Dev) | MySQL |
| Database (Production) | PostgreSQL (Neon Cloud) |
| Build Tool | Maven |
| Containerization | Docker |
| Deployment | Render (Cloud Platform) |
| API Testing | Postman / Swagger |

---

## ✨ Features

- ✅ **User Registration & Login** — Secure auth with hashed passwords
- ✅ **JWT Authentication** — Stateless token-based security
- ✅ **Role-Based Access Control** — Admin and User roles
- ✅ **Workout Tracking** — Log and manage workouts
- ✅ **Diet / Calorie Tracking** — Monitor daily nutrition
- ✅ **RESTful API** — Clean, standard REST endpoints
- ✅ **PostgreSQL Support** — Production-ready cloud database
- ✅ **Dockerized** — Run anywhere with Docker
- ✅ **Deployed on Render** — Publicly accessible live API

---

## 🔄 Database Migration: MySQL → PostgreSQL

This project was originally developed using **MySQL**. For cloud deployment on **Render**, the database was migrated to **PostgreSQL** hosted on **[Neon](https://neon.tech)**.

### Changes Made During Migration:

1. **`pom.xml` dependency** — Replaced MySQL connector with PostgreSQL driver:
```xml
<!-- Removed -->
<dependency>
    <groupId>com.mysql</groupId>
    <artifactId>mysql-connector-j</artifactId>
</dependency>

<!-- Added -->
<dependency>
    <groupId>org.postgresql</groupId>
    <artifactId>postgresql</artifactId>
    <scope>runtime</scope>
</dependency>
```

2. **`application.properties`** — Updated datasource config:
```properties
# PostgreSQL (Production - Neon)
spring.datasource.url=jdbc:postgresql://<neon-host>/<dbname>?sslmode=require
spring.datasource.driver-class-name=org.postgresql.Driver
spring.jpa.database-platform=org.hibernate.dialect.PostgreSQLDialect
```

---

## 📁 Project Structure

```
fitness-monolith/
│
├── src/
│   ├── main/
│   │   ├── java/com/fitness/
│   │   │   ├── controller/       # REST Controllers
│   │   │   ├── service/          # Business Logic
│   │   │   ├── repository/       # JPA Repositories
│   │   │   ├── model/            # Entity Classes
│   │   │   ├── dto/              # Data Transfer Objects
│   │   │   ├── security/         # JWT & Spring Security Config
│   │   │   └── config/           # App Configuration
│   │   └── resources/
│   │       ├── application.properties
│   │       └── application-prod.properties
│
├── Dockerfile                    # Docker build file
├── pom.xml                       # Maven dependencies
└── README.md
```

---

## 📡 API Endpoints

### 🔐 Authentication
| Method | Endpoint | Description |
|---|---|---|
| POST | `/api/auth/register` | Register a new user |
| POST | `/api/auth/login` | Login and get JWT token |

### 🏋️ Workout
| Method | Endpoint | Description |
|---|---|---|
| GET | `/api/workouts` | Get all workouts |
| POST | `/api/workouts` | Add a new workout |
| PUT | `/api/workouts/{id}` | Update a workout |
| DELETE | `/api/workouts/{id}` | Delete a workout |

### 🥗 Diet / Nutrition
| Method | Endpoint | Description |
|---|---|---|
| GET | `/api/diet` | Get diet logs |
| POST | `/api/diet` | Add a diet entry |
| PUT | `/api/diet/{id}` | Update a diet entry |
| DELETE | `/api/diet/{id}` | Delete a diet entry |

### 👤 User
| Method | Endpoint | Description |
|---|---|---|
| GET | `/api/users/profile` | Get current user profile |
| PUT | `/api/users/profile` | Update user profile |

> 🔑 All endpoints (except `/auth/*`) require a valid **JWT Bearer Token** in the `Authorization` header:
> ```
> Authorization: Bearer <your_token_here>
> ```

---

## 🔐 Environment Variables

Set these environment variables before running the project:

| Variable | Description | Example |
|---|---|---|
| `SPRING_DATASOURCE_URL` | PostgreSQL connection URL | `jdbc:postgresql://host/db?sslmode=require` |
| `SPRING_DATASOURCE_USERNAME` | DB username | `your_db_user` |
| `SPRING_DATASOURCE_PASSWORD` | DB password | `your_db_password` |
| `JWT_SECRET` | Secret key for JWT signing | `mySecretKey123` |
| `JWT_EXPIRATION` | Token expiry in ms | `86400000` |

---

## 🚀 How to Use — 3 Ways

---

### 1. Via GitHub (Run Locally)

#### ✅ Prerequisites
- Java 17+
- Maven
- PostgreSQL or MySQL installed locally
- Git

#### Steps:

```bash
# Step 1: Clone the repository
git clone https://github.com/gopalkrishna06114/Fitness-Tracker-SpringBoot-Backend-.git

# Step 2: Navigate into the project directory
cd Fitness-Tracker-SpringBoot-Backend-
```

#### Configure your database in `src/main/resources/application.properties`:

**For MySQL (local dev):**
```properties
spring.datasource.url=jdbc:mysql://localhost:3306/fitness_db
spring.datasource.username=root
spring.datasource.password=yourpassword
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver
spring.jpa.database-platform=org.hibernate.dialect.MySQL8Dialect
spring.jpa.hibernate.ddl-auto=update
```

**For PostgreSQL:**
```properties
spring.datasource.url=jdbc:postgresql://localhost:5432/fitness_db
spring.datasource.username=postgres
spring.datasource.password=yourpassword
spring.datasource.driver-class-name=org.postgresql.Driver
spring.jpa.database-platform=org.hibernate.dialect.PostgreSQLDialect
spring.jpa.hibernate.ddl-auto=update
```

```bash
# Step 3: Build the project
mvn clean install

# Step 4: Run the project
mvn spring-boot:run
```

The server will start at: **`http://localhost:8080`**

---

### 2. Via Docker Hub

My project is publicly available as a Docker image — no need to clone any code!

#### ✅ Prerequisites
- [Docker](https://www.docker.com/get-started) installed

#### Steps:

```bash
# Step 1: Pull the public Docker image
docker pull gopalkrishnadocker/fitness-monolith:latest
```

```bash
# Step 2: Run the container with your database environment variables
docker run -d \
  -p 8080:8080 \
  -e SPRING_DATASOURCE_URL=jdbc:postgresql://<your-db-host>/<your-db-name>?sslmode=require \
  -e SPRING_DATASOURCE_USERNAME=<your-db-username> \
  -e SPRING_DATASOURCE_PASSWORD=<your-db-password> \
  -e JWT_SECRET=<your-jwt-secret> \
  --name fitness-tracker \
  gopalkrishnadocker/fitness-monolith:latest
```

```bash
# Step 3: Verify the container is running
docker ps
```

The API will be available at: **`http://localhost:8080`**

#### ⛔ To stop the container:
```bash
docker stop fitness-tracker
docker rm fitness-tracker
```

> 💡 **Tip:** You can use [Neon](https://neon.tech) (free) to create a PostgreSQL cloud database and use its connection string in the environment variables above.

---

### 3. Via Render (Live API — No Setup Needed!)

The backend is already **live and deployed** on Render. You can directly call the API without any local setup.

**Base URL:**
```
https://fitness-monolith-8ecy.onrender.com
```

#### Example API Calls:

**Register a new user:**
```bash
curl -X POST https://fitness-monolith-8ecy.onrender.com/api/auth/register \
  -H "Content-Type: application/json" \
  -d '{
    "name": "John Doe",
    "email": "john@example.com",
    "password": "password123"
  }'
```

**Login:**
```bash
curl -X POST https://fitness-monolith-8ecy.onrender.com/api/auth/login \
  -H "Content-Type: application/json" \
  -d '{
    "email": "john@example.com",
    "password": "password123"
  }'
```

**Access a protected route (with token):**
```bash
curl -X GET https://fitness-monolith-8ecy.onrender.com/api/workouts \
  -H "Authorization: Bearer <your_jwt_token>"
```

> ⚠️ **Note:** Free-tier Render services **spin down** after 15 minutes of inactivity. The **first request may take 30–60 seconds** to respond. Subsequent requests will be fast.

---

## 🐳 Docker Details

### Dockerfile Overview

The project uses a multi-layer Dockerfile to create an optimized image:

```dockerfile
# Use official Java base image
FROM openjdk:17-jdk-slim

# Set working directory
WORKDIR /app

# Copy the built JAR file
COPY target/fitness-monolith-*.jar app.jar

# Expose port
EXPOSE 8080

# Run the application
ENTRYPOINT ["java", "-jar", "app.jar"]
```

### Build Your Own Image (Optional):

```bash
# Build JAR first
mvn clean package -DskipTests

# Build Docker image
docker build -t gopalkrishnadocker/fitness-monolith:latest .

# Push to Docker Hub (requires docker login)
docker login
docker push gopalkrishnadocker/fitness-monolith:latest
```

### Docker Hub Image:
🔗 `docker pull gopalkrishnadocker/fitness-monolith:latest`

---

## 🤝 Contributing

Contributions are welcome! Here's how:

```bash
# Fork the repo, then clone your fork
git clone https://github.com/your-username/Fitness-Tracker-SpringBoot-Backend-.git

# Create a new branch
git checkout -b feature/your-feature-name

# Make your changes and commit
git commit -m "Add: your feature description"

# Push to your fork
git push origin feature/your-feature-name

# Open a Pull Request on GitHub
```

---

## 👨‍💻 Author

**Gopal Krishna**

- GitHub: [@gopalkrishna06114](https://github.com/gopalkrishna06114)
- Project Repo: [Fitness-Tracker-SpringBoot-Backend-](https://github.com/gopalkrishna06114/Fitness-Tracker-SpringBoot-Backend-)
- Live API: [https://fitness-monolith-8ecy.onrender.com](https://fitness-monolith-8ecy.onrender.com)

---

## 📄 License

This project is open source and available under the [MIT License](LICENSE).

---

<p align="center">Made with ❤️ by Gopal Krishna | Powered by Spring Boot + PostgreSQL + Docker + Render</p>
