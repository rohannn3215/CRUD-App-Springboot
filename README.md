# Student Management API

A lightweight RESTful CRUD service developed with Spring Boot, Spring Data JPA, and MySQL, implementing soft-delete patterns and layered architecture.

## Tech Stack
- **Java 17+**
- **Spring Boot** (Spring Web, Spring Data JPA)
- **MySQL**
- **Maven**

---

## API Endpoints

Base Path: `/api/students`

| Method | Endpoint | Description | Request Body | Status Code |
| :--- | :--- | :--- | :--- | :--- |
| `POST` | `/create` | Create a new student | JSON payload | `201 Created` |
| `GET` | `/getAll` | Fetch all active students | None | `200 OK` / `404 Not Found` |
| `GET` | `/get/{id}` | Fetch student by ID | None | `200 OK` / `404 Not Found` |
| `PUT` | `/update/{id}` | Update student details | JSON payload | `200 OK` / `404 Not Found` |
| `PATCH` | `/delete-soft/{id}` | Soft delete student | None | `200 OK` |
| `DELETE` | `/delete/{id}` | Permanently delete student | None | `200 OK` |

---

## Usage Guide

### 1. Database Setup
Create database in MySQL:
```sql
CREATE DATABASE crud_db;
```
Configure credentials in `src/main/resources/application.properties`.

### 2. Run Application
```bash
./mvnw spring-boot:run
```
Service runs at `http://localhost:8080`.

### 3. Example Request Payloads

**Create Student (`POST /api/students/create`):**
```json
{
  "name": "Rohan Jadhav",
  "age": 21,
  "email": "rohan@gmail.com",
  "rollNo": 101,
  "subject": "Java"
}
```

**Update Student (`PUT /api/students/update/{id}`):**
```json
{
  "name": "Rohan Jadhav",
  "age": 22,
  "email": "rohan.updated@gmail.com",
  "rollNo": 101,
  "subject": "Spring Boot"
}
```

> **Note:** For `GET`, `DELETE`, and `PATCH` requests, do not send a request body.
