# Forumly

A self-contained forum application built with Spring Boot. Users can register, create posts, leave comments, and vote — all secured with Spring Security and persisted via an embedded H2 database.

## Features

- User registration and authentication (Spring Security, BCrypt)
- Create, browse, and read forum posts
- Nested commenting on posts
- Upvote / downvote posts
- Schema migrations managed by Flyway
- Deployable as a standalone JAR or via Docker

## Tech Stack

| Layer       | Technology                          |
|-------------|-------------------------------------|
| Backend     | Java 17, Spring Boot 3, Spring MVC  |
| Security    | Spring Security 6                   |
| Persistence | Spring Data JPA, H2 (file mode)     |
| Migrations  | Flyway                              |
| Templating  | Thymeleaf + Thymeleaf Security extras |
| Build       | Maven                               |
| Container   | Docker (multi-stage build)          |
| Observability | Spring Boot Actuator              |

## Getting Started

**Prerequisites:** Java 17+

### Run with Docker

```bash
docker compose -f docker/docker-compose.yml up -d
```

### Run as JAR

```bash
./mvnw clean package -DskipTests
java -jar target/forumly-app.jar
```

Open [http://localhost:8080](http://localhost:8080) in your browser.

A `data/` directory is created on first run to hold the H2 database files.

## Project Structure

```
src/main/java/com/dominikmiskovic/forumly/
├── config/          # Security and migration configuration
├── controller/      # MVC controllers (Home, Post, Comment, Vote, Auth)
├── dto/             # Request and response DTOs
├── model/           # JPA entities (User, Post, Comment, Vote)
├── repository/      # Spring Data repositories
├── service/         # Business logic
└── exception/       # Custom exceptions
```

## Architecture

The app follows a standard layered MVC architecture. Spring Security handles authentication and route protection. Flyway runs versioned SQL migrations on startup. The H2 database runs in file mode so data survives restarts.

```
Browser → Thymeleaf templates ← Controllers → Services → Repositories → H2 (file)
                                      ↑
                               Spring Security
```
