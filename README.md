# Student Management API

A lightweight RESTful CRUD service built with Spring Boot, Spring Data JPA, and MySQL with soft-delete support.

---

## Tech Stack

| Technology | Purpose |
| :--- | :--- |
| Java 17+ | Core Programming Language |
| Spring Boot | Application Framework |
| Spring Data JPA / Hibernate | Data Persistence & ORM |
| MySQL | Relational Database |
| Maven | Build & Dependency Management |

---

## API Endpoints

Base URL: `http://localhost:8080/api/students`

| Method | Endpoint | Description | Request Body | Response Status |
| :--- | :--- | :--- | :--- | :--- |
| `POST` | `/create` | Create a new student | JSON | `201 Created` |
| `GET` | `/getAll` | Get all active students | None | `200 OK` / `404 Not Found` |
| `GET` | `/get/{id}` | Get student by ID | None | `200 OK` / `404 Not Found` |
| `PUT` | `/update/{id}` | Update student by ID | JSON | `200 OK` / `404 Not Found` |
| `PATCH` | `/delete-soft/{id}` | Soft delete student | None | `200 OK` / `404 Not Found` |
| `DELETE` | `/delete/{id}` | Permanently delete student | None | `200 OK` / `404 Not Found` |

---

## Request & Response Samples

### 1. Create Student
- **Endpoint**: `POST /api/students/create`
- **Request Body**:
```json
{
  "name": "Rohan Jadhav",
  "age": 21,
  "email": "rohan@gmail.com",
  "rollNo": 101,
  "subject": "Java"
}
```
- **Response**: `201 Created`

### 2. Update Student
- **Endpoint**: `PUT /api/students/update/{id}`
- **Request Body**:
```json
{
  "name": "Rohan Jadhav",
  "age": 22,
  "email": "rohan.new@gmail.com",
  "rollNo": 101,
  "subject": "Spring Boot"
}
```
- **Response**: `200 OK`

---

## Quick Start

| Step | Action | Command / Detail |
| :--- | :--- | :--- |
| **1. Database** | Create MySQL DB | `CREATE DATABASE crud_db;` |
| **2. Configuration** | Set credentials | Edit `src/main/resources/application.properties` |
| **3. Run** | Start application | `./mvnw spring-boot:run` |
| **4. Base URL** | Server port | `http://localhost:8080/api/students` |
