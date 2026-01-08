# Spring Boot + Maven

This template provides the backend setup for the MediTracker application.

## Technology Stack

- **Spring Boot 3.4.2** - Application framework
- **Java 17** - Programming language
- **Maven** - Dependency management and build tool
- **PostgreSQL** - Relational database
- **Flyway** - Database migration tool
- **Spring Security** - Authentication and authorization
- **JWT (JSON Web Tokens)** - Stateless authentication
- **Spring Data JPA** - Data persistence layer
- **Thymeleaf** - Server-side template engine
- **Lombok** - Reduces boilerplate code

## Prerequisites

- Java 17 or higher
- Maven 3.6 or higher
- PostgreSQL 12 or higher
- Docker (optional, for containerized deployment)

## Getting Started

### 1. Database Setup

Create a PostgreSQL database:

```sql
CREATE DATABASE meditracker;
CREATE USER myuser WITH PASSWORD 'meditracker_pass';
GRANT ALL PRIVILEGES ON DATABASE meditracker TO myuser;
```

### 2. Configuration

Update `src/main/resources/application.properties` if needed, but the important defaults there expect the postgres container:

```properties
spring.datasource.url=jdbc:postgresql://localhost:5432/meditracker
spring.datasource.username=myuser
spring.datasource.password=meditracker_pass
```

### 3. Running the Application

```bash
mvn spring-boot:run
```

The application will start on `http://localhost:8080`

## Database Migrations

This project uses **Flyway** for database version control. Migration scripts are located in `src/main/resources/db/migration/`.

Flyway automatically runs migrations on application startup. Hibernate's auto-DDL is disabled to ensure controlled schema changes.

## Authentication

The application uses **JWT (JSON Web Tokens)** for stateless authentication:

- Token expiration: 1 hour (configurable in `application.properties`)
- Authentication endpoint: `/api/auth/login`
- Register endpoint: `/api/auth/register`

Include the JWT token in the `Authorization` header for protected endpoints:

```
Authorization: Bearer <your-jwt-token>
```

## API Endpoints

### Public Endpoints
- `POST /api/auth/login` - User login
- `POST /api/auth/register` - User registration
- `GET /` - Home page

### Protected Endpoints
- `GET /api/profile` - User profile
- `GET /api/medicines` - Medicine list
- `GET /api/prescriptions` - Prescription list
- `GET /api/admin/**` - Admin endpoints (requires ADMIN role)

## Project Structure

```
src/main/java/org/springbozo/meditracker/
├── config/                 # Security and JWT configuration
├── constants/              # Application constants
├── controller/             # REST controllers
├── DAO/                    # Data Transfer Objects
├── model/                  # JPA entities
├── repository/             # Spring Data repositories
└── service/                # Business logic layer
```

## Security Configuration

The application implements custom security with:

- Password-based authentication
- JWT token generation and validation
- Role-based access control (RBAC)
- Custom authentication entry point
- Token filter for request validation

```

## Development Tips

### Hot Reload

For development with automatic restart on file changes, use Spring Boot DevTools (already included):

```bash
mvn spring-boot:run
```

### Database Console

To access the H2 console during development:

```
http://localhost:8080/h2-console
```

## Resources

- [Spring Boot Documentation](https://docs.spring.io/spring-boot/docs/current/reference/html/)
- [Spring Security Reference](https://docs.spring.io/spring-security/reference/)
- [Flyway Documentation](https://flywaydb.org/documentation/)
- [JWT.io](https://jwt.io/)

## License

This project is open source and available under the [MIT License](LICENSE).
