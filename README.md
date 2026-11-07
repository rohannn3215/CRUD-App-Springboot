# 🎓 Spring Boot Student Management CRUD Application

A robust RESTful CRUD API built using **Spring Boot**, **Spring Data JPA**, and **MySQL**, featuring **Soft Delete** functionality and clean layered architecture.

---

## 🚀 Features

- **Full CRUD Operations**: Create, Read (single & all), Update, and Delete student records.
- **Soft Delete**: Non-destructive deletion where records are marked with `deleted = true` rather than being dropped from the database.
- **Layered Architecture**: Clear separation of concerns between Controller, Service, Repository, and Entity layers.
- **Auto-generated Primary Keys**: Uses `GenerationType.IDENTITY` for automatic MySQL increment.
- **RESTful Response Standards**: Proper HTTP status codes (`201 Created`, `200 OK`, `404 Not Found`).

---

## 🛠️ Tech Stack & Prerequisites

- **Java**: 17+ (or 21)
- **Framework**: Spring Boot 4.x / 3.x (Spring Web, Spring Data JPA)
- **Database**: MySQL 8.x / 9.x
- **Build Tool**: Maven
- **API Testing**: Postman / cURL

---

## ⚙️ Configuration & Setup

### 1. Database Configuration
Make sure MySQL is running and create the database:
```sql
CREATE DATABASE IF NOT EXISTS crud_db;
```

Check `src/main/resources/application.properties` to ensure credentials match your MySQL setup:
```properties
spring.application.name=crud-application

spring.datasource.url=jdbc:mysql://localhost:3306/crud_db
spring.datasource.username=root
spring.datasource.password=YOUR_PASSWORD

spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true
spring.jpa.properties.hibernate.format_sql=true
```

### 2. Run the Application
You can run the application directly from your IDE (`CrudApplication.java`) or using Maven in your terminal:
```bash
./mvnw spring-boot:run
```
*(On Windows Command Prompt: `mvnw.cmd spring-boot:run`)*

The server will start at: `http://localhost:8080`

---

## 📡 API Endpoints Reference

Base URL: `http://localhost:8080/api/students`

| Method | Endpoint | Description | Request Body | Success Response |
| :--- | :--- | :--- | :--- | :--- |
| **POST** | `/create` | Create a new student | JSON (Student details) | `201 Created` |
| **GET** | `/getAll` | Fetch all active (non-deleted) students | None *(Body: none)* | `200 OK` / `404 Not Found` |
| **GET** | `/get/{id}` | Fetch a student by ID | None *(Body: none)* | `200 OK` / `404 Not Found` |
| **PUT** | `/update/{id}` | Update existing student | JSON (Updated fields) | `200 OK` / `404 Not Found` |
| **PATCH** | `/delete-soft/{id}` | Soft delete student (`deleted = true`) | None | `200 OK` ("Record deleted") |
| **DELETE**| `/delete/{id}` | Permanently remove record | None | `200 OK` ("Record deleted") |

---

## 🧪 How to Test with Postman

### 1. Create Student (POST)
- **Method**: `POST`
- **URL**: `http://localhost:8080/api/students/create`
- **Headers**: `Content-Type: application/json`
- **Body**: (raw -> JSON)
```json
{
  "name": "Rohan Jadhav",
  "age": 21,
  "email": "rohan@gmail.com",
  "rollNo": 101,
  "subject": "Spring Boot"
}
```
- **Response**: `201 Created`

---

### 2. Get All Active Students (GET)
- **Method**: `GET`
- **URL**: `http://localhost:8080/api/students/getAll`
- **Body**: Ensure the **Body** tab is set to **`none`**.
- **Response**: `200 OK` (Array of student objects with `deleted: false`)

---

### 3. Get Student by ID (GET)
- **Method**: `GET`
- **URL**: `http://localhost:8080/api/students/get/1`
- **Body**: Ensure the **Body** tab is set to **`none`**.
- **Response**: `200 OK` (Student object) or `404 Not Found`

---

### 4. Update Student (PUT)
- **Method**: `PUT`
- **URL**: `http://localhost:8080/api/students/update/1`
- **Headers**: `Content-Type: application/json`
- **Body**: (raw -> JSON)
```json
{
  "name": "Rohan Jadhav",
  "age": 22,
  "email": "rohan.new@gmail.com",
  "rollNo": 101,
  "subject": "Spring Boot & Microservices"
}
```
- **Response**: `200 OK`

---

### 5. Soft Delete Student (PATCH)
- **Method**: `PATCH`
- **URL**: `http://localhost:8080/api/students/delete-soft/1`
- **Response**: `200 OK` with text `"Record deleted"`.
- *Note*: Calling `/getAll` or `/get/1` after this will no longer return this student.

---

### 6. Hard Delete Student (DELETE)
- **Method**: `DELETE`
- **URL**: `http://localhost:8080/api/students/delete/1`
- **Response**: `200 OK` with text `"Record deleted"`.
- *Note*: Permanently deletes the row from MySQL.

---

## 🏛️ Project Architecture

```
com.rj.crud_application
 ├── controller
 │    └── StudentController.java     # Handles incoming HTTP REST requests
 ├── service
 │    └── StudentService.java        # Business logic & soft delete handling
 ├── repository
 │    └── StudentRepository.java     # Spring Data JPA queries
 ├── entity
 │    └── Student.java               # JPA Entity mapped to MySQL table
 └── CrudApplication.java            # Main Spring Boot application entry point
```
