# 🏨 Hotel Booking & Management System

A full-stack hotel booking and management platform with a **Spring Boot** REST API backend and a **React (Vite)** frontend. Guests can browse rooms, check availability, and book stays; admins can manage rooms, bookings, users, and roles — all secured with JWT authentication.

<p align="left">
  <img alt="Java" src="https://img.shields.io/badge/Java-17-orange?logo=openjdk">
  <img alt="Spring Boot" src="https://img.shields.io/badge/Spring%20Boot-3.5.4-brightgreen?logo=springboot">
  <img alt="React" src="https://img.shields.io/badge/React-18-61DAFB?logo=react">
  <img alt="Vite" src="https://img.shields.io/badge/Vite-4-646CFF?logo=vite">
  <img alt="PostgreSQL" src="https://img.shields.io/badge/PostgreSQL-Database-4169E1?logo=postgresql">
  <img alt="License" src="https://img.shields.io/badge/License-MIT-lightgrey">
</p>

---

## ✨ Features

**Guest experience**
- Browse and search available rooms by type and date range
- View room details and photos
- Book a room and receive a unique booking confirmation code
- Look up a booking using its confirmation code
- Register with email verification, log in, and reset a forgotten password

**Admin / management**
- JWT-secured, role-based access control (`ADMIN` / `USER`)
- Add, update, and delete rooms
- View and manage all bookings
- Manage users and assign or remove roles
- File upload support for room photos

**Platform**
- RESTful API built with Spring Boot, Spring Security, and Spring Data JPA
- PostgreSQL persistence with configurable Hibernate DDL strategy
- JWT-based stateless authentication (`jjwt`)
- Transactional email support (SMTP, configured for Brevo) for verification and password-reset emails
- Global exception handling with meaningful HTTP error responses
- Dockerized backend for easy deployment
- Responsive React UI styled with Bootstrap / React-Bootstrap and a date-range picker for booking

---

## 🧱 Tech Stack

| Layer          | Technology                                                                 |
|----------------|-----------------------------------------------------------------------------|
| Backend        | Java 17, Spring Boot 3.5.4, Spring Web, Spring Data JPA, Spring Security   |
| Auth           | JWT (`io.jsonwebtoken`)                                                    |
| Database       | PostgreSQL                                                                 |
| Email          | Spring Mail (SMTP, Brevo-compatible)                                       |
| Build          | Maven                                                                      |
| Containerization | Docker (multi-stage build)                                              |
| Frontend       | React 18, Vite, React Router                                              |
| UI             | Bootstrap 5, React-Bootstrap, React Icons, React Date Range                |
| HTTP Client    | Axios                                                                      |

---

## 🗂️ Project Structure

```
Hotel-Booking-and-Management-System/
├── Backend/                       # Spring Boot REST API
│   ├── src/main/java/learning/hotelbackend/
│   │   ├── controller/             # REST controllers (Auth, Room, Booking, User, Role)
│   │   ├── service/                 # Business logic
│   │   ├── repository/              # Spring Data JPA repositories
│   │   ├── model/                   # JPA entities (User, Role, Room, BookedRoom)
│   │   ├── request/  response/      # DTOs
│   │   ├── security/                # JWT filters, WebSecurityConfig, user details
│   │   ├── exception/                # Custom exceptions + global handler
│   │   └── config/                   # Startup data initialization
│   ├── src/main/resources/           # application.properties (env-driven)
│   ├── Dockerfile
│   └── pom.xml
│
└── Frontend/                       # React + Vite client
    ├── src/
    │   ├── components/
    │   │   ├── admin/                # Admin dashboards
    │   │   ├── auth/                 # Login, register, password reset
    │   │   ├── booking/               # Booking flow & confirmation
    │   │   ├── room/                  # Room listing & details
    │   │   ├── home/ layout/ common/  # Shared UI
    │   │   └── utils/                 # Helpers, API calls
    │   └── assets/
    ├── vite.config.js
    └── package.json
```

---

## 🔌 API Overview

All endpoints are prefixed by the backend's base URL (default `http://localhost:9192`).

| Resource   | Endpoint                                          | Description                          |
|------------|----------------------------------------------------|---------------------------------------|
| Auth       | `POST /auth/register-user`                         | Register a new account               |
| Auth       | `GET  /auth/verify-email`                           | Verify email via token                |
| Auth       | `POST /auth/login`                                  | Log in and receive a JWT              |
| Auth       | `POST /auth/forgot-password`                        | Request a password reset email        |
| Auth       | `POST /auth/reset-password`                         | Reset password with a valid token     |
| Rooms      | `GET  /rooms/all-rooms`                             | List all rooms                        |
| Rooms      | `GET  /rooms/available-rooms`                       | Search available rooms by date/type   |
| Rooms      | `GET  /rooms/room/{roomId}`                         | Get a single room's details           |
| Rooms      | `GET  /rooms/room/types`                            | List distinct room types              |
| Rooms      | `POST /rooms/add/new-room`                          | Add a new room (admin)                |
| Rooms      | `PUT  /rooms/update/{roomId}`                       | Update a room (admin)                 |
| Rooms      | `DELETE /rooms/delete/room/{roomId}`                | Delete a room (admin)                 |
| Bookings   | `POST /bookings/room/{roomId}/booking`              | Book a room                           |
| Bookings   | `GET  /bookings/confirmation/{confirmationCode}`    | Look up a booking by confirmation code|
| Bookings   | `GET  /bookings/user/{email}/bookings`              | List a user's bookings                |
| Bookings   | `GET  /bookings/all-bookings`                       | List all bookings (admin)             |
| Bookings   | `DELETE /bookings/booking/{bookingId}/delete`       | Cancel a booking                      |
| Users      | `GET  /users/all`                                   | List all users (admin)                |
| Users      | `GET  /users/{email}`                               | Get a user's profile                  |
| Users      | `DELETE /users/delete/{email}`                      | Delete a user (admin)                 |
| Roles      | `GET  /roles/all-roles`                             | List roles (admin)                    |
| Roles      | `POST /roles/create-new-role`                       | Create a role (admin)                 |
| Roles      | `POST /roles/assign-user-to-role`                   | Assign a role to a user (admin)       |
| Roles      | `POST /roles/remove-user-from-role`                 | Remove a role from a user (admin)     |
| Roles      | `DELETE /roles/delete/{roleId}`                     | Delete a role (admin)                 |

---

## 🚀 Getting Started

### Prerequisites
- Java 17+
- Maven (or use the included `mvnw` wrapper)
- Node.js 18+ and npm
- PostgreSQL instance
- SMTP credentials (e.g. Brevo) if you want email verification / password reset to work

### 1. Clone the repository
```bash
git clone https://github.com/V1vekgupta/Hotel-Booking-and-Management-System.git
cd Hotel-Booking-and-Management-System
```

### 2. Configure the backend
The backend reads all configuration from environment variables (see `Backend/src/main/resources/application.properties`). Create a `.env` file or export the following variables before running:

```bash
SERVER_PORT=9192

DATABASE_URL=jdbc:postgresql://localhost:5432/hotel_db
DATABASE_USERNAME=postgres
DATABASE_PASSWORD=your_password
DATABASE_DRIVER=org.postgresql.Driver

HIBERNATE_DIALECT=org.hibernate.dialect.PostgreSQLDialect
DDL_AUTO=update
DB_AUTO_COMMIT=false

MAX_FILE_SIZE=10MB
MAX_REQUEST_SIZE=10MB

SHOW_SQL=true
HIBERNATE_SQL_LOG_LEVEL=INFO
HIBERNATE_BINDER_LOG_LEVEL=INFO

AUTH_TOKEN_EXPIRATION_IN_MS=86400000
AUTH_TOKEN_JWT_SECRET=your_jwt_secret

APP_FRONTEND_URL=http://localhost:5173
EMAIL_VERIFICATION_TOKEN_EXPIRY_MINUTES=60
PASSWORD_RESET_TOKEN_EXPIRY_MINUTES=30

MAIL_FROM=your_email@example.com
MAIL_HOST=smtp-relay.brevo.com
MAIL_PORT=587
MAIL_USERNAME=your_smtp_username
MAIL_PASSWORD=your_smtp_password
SMTP_AUTH=true
TTLS=true
TTLS_REQUIRED=true
MAIL_PROTOCOL=smtp
```

### 3. Run the backend
```bash
cd Backend
./mvnw spring-boot:run
```
The API will start on `http://localhost:9192` (or your configured `SERVER_PORT`).

Alternatively, build and run with Docker:
```bash
cd Backend
docker build -t lakeside-hotel-backend .
docker run -p 9192:9192 --env-file .env lakeside-hotel-backend
```

### 4. Run the frontend
```bash
cd Frontend
npm install
npm run dev
```
The app will be available at `http://localhost:5173`.

> Make sure the frontend's API base URL (in `src/components/utils/`) points to your running backend.

---

## 🧪 Running Tests

```bash
cd Backend
./mvnw test
```

---

## 🤝 Contributing

Contributions are welcome! To contribute:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/your-feature`)
3. Commit your changes (`git commit -m "Add your feature"`)
4. Push to the branch (`git push origin feature/your-feature`)
5. Open a Pull Request

---

## 📄 License

This project is available under the MIT License. Add a `LICENSE` file to formalize this if you intend to distribute the project.

---

## 👤 Author

**Vivek Gupta** — [GitHub](https://github.com/V1vekgupta)
