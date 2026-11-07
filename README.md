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
| `POST` | `/create` | Create a new student (`deleted = false`) | JSON | `201 Created` |
| `GET` | `/getAll` | Get all active students | None | `200 OK` / `404 Not Found` |
| `GET` | `/get/{id}` | Get student by ID | None | `200 OK` / `404 Not Found` |
| `PUT` | `/update/{id}` | Update student by ID | JSON | `200 OK` / `404 Not Found` |
| `PATCH` | `/delete-soft/{id}` | Soft delete student (`deleted = true`) | None | `200 OK` / `404 Not Found` |
| `DELETE` | `/delete/{id}` | Permanently delete student from DB | None | `200 OK` / `404 Not Found` |

---

## Soft Delete Mechanism

This application implements a **Soft Delete** pattern using a boolean `deleted` flag.

| Operation | Hard Delete (`DELETE`) | Soft Delete (`PATCH`) |
| :--- | :--- | :--- |
| **SQL Action** | `DELETE FROM student WHERE id = ?` | `UPDATE student SET deleted = true WHERE id = ?` |
| **Database State** | Row is permanently removed | Row stays in database with `deleted = true` |
| **Read Impact** | Inaccessible | Filtered out from `/getAll` and `/get/{id}` |
| **Data Recovery** | Not possible | Possible by updating `deleted = false` |

### How It Works in Code:
- **Entity**: `Student.java` contains a `Boolean deleted` column.
- **Repository**: Uses Spring Data JPA custom queries:
  - `findByIdAndDeletedIsFalse(Long id)`
  - `findByDeletedIsFalse()`
- **Service**: 
  - `createStudent`: Sets `deleted = false` on initial creation.
  - `deleteStudentSoftly`: Sets `deleted = true` without deleting the row.
  - `getAllStudent` & `getStudent`: Only return records where `deleted = false`.

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
