<div align="center">

<h1>🏨 The Elite Hotel</h1>
<h3>Hotel Booking & Management System</h3>

<p>
  <img src="https://img.shields.io/badge/Status-Active-22c55e?style=for-the-badge" />
  <img src="https://img.shields.io/badge/License-MIT-blue?style=for-the-badge" />
  <img src="https://img.shields.io/badge/PRs-Welcome-orange?style=for-the-badge" />
</p>

<p>
  <img src="https://img.shields.io/badge/React-20232A?style=for-the-badge&logo=react&logoColor=61DAFB" />
  <img src="https://img.shields.io/badge/Vite-646CFF?style=for-the-badge&logo=vite&logoColor=white" />
  <img src="https://img.shields.io/badge/Bootstrap-7952B3?style=for-the-badge&logo=bootstrap&logoColor=white" />
  <img src="https://img.shields.io/badge/SpringBoot-6DB33F?style=for-the-badge&logo=spring&logoColor=white" />
  <img src="https://img.shields.io/badge/PostgreSQL-316192?style=for-the-badge&logo=postgresql&logoColor=white" />
  <img src="https://img.shields.io/badge/JWT-black?style=for-the-badge&logo=jsonwebtokens" />
  <img src="https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white" />
</p>

> A full-stack hotel booking and management platform with role-based access control, JWT authentication, and a real-time room availability engine — built with Spring Boot and React.

**[Live Demo](#)** · **[Report Bug](https://github.com/V1vekgupta/Hotel-Booking-and-Management-System/issues)**

</div>

---

## 📑 Table of Contents
- [Description](#-description)
- [What Makes This Stand Out](#-what-makes-this-stand-out)
- [Features](#-features)
- [Tech Stack](#️-tech-stack)
- [Project Structure](#-project-structure)
- [API Reference](#-api-reference)
- [Quick Start](#-quick-start)
- [Environment Variables](#-environment-variables)
- [Screenshots](#-screenshots)
- [Future Improvements](#-future-improvements)

---

## 📝 Description

A full-stack hotel booking platform built with **Spring Boot, Spring Security, and React**, featuring separate experiences for guests and administrators. Implements **JWT-based authentication with role-based access control (RBAC)**, a **date-range room availability engine**, transactional email for verification and password resets, and a **PostgreSQL** database with a clean JPA/Hibernate domain model.

---

## 🎯 What Makes This Stand Out

| Capability | Details |
|---|---|
| 🔐 **Security & Auth** | Spring Security with stateless JWT tokens and role-based access control (RBAC) across 2 roles — Guest (`ROLE_USER`) and Admin (`ROLE_ADMIN`) |
| 🛏️ **Booking Engine** | Date-range availability search that excludes rooms with overlapping bookings, unique booking confirmation codes, and booking lookup by code |
| 📧 **Transactional Email** | SMTP-based email verification on signup and secure token-based password reset flow |
| 🖼️ **Image Management** | Room photo upload and update via multipart form data |
| 👥 **Role-Scoped Platform** | Guest-facing booking flow and a protected Admin dashboard for room, booking, user, and role management |
| 🐳 **Containerized Backend** | Dockerized Spring Boot backend for consistent, portable deployment |

---

## ✨ Features

### 🧳 Guest
- Browse and search available rooms by type and check-in/check-out dates
- View room details and photos
- Book a room and receive a unique booking confirmation code
- Look up an existing booking using its confirmation code
- Register with email verification, log in, and reset a forgotten password

### 🛠️ Admin
- Add, update, and delete rooms (with photo upload)
- View and manage all bookings across the platform
- Manage users and assign or remove roles
- Access admin-only protected endpoints via RBAC

### 🔐 Authentication
- Register with automatic `ROLE_USER` assignment and email verification
- Log in to receive a JWT for authenticated requests
- Forgot-password / reset-password flow via emailed token

---

## 🛠️ Tech Stack

**Frontend:** React, Vite, React Router, Bootstrap / React-Bootstrap, Axios, React Date Range

**Backend:** Spring Boot, Spring Security (JWT + RBAC), Spring Data JPA / Hibernate, Maven

**Database:** PostgreSQL

**Email:** Spring Mail (SMTP)

**Tools:** Docker, Postman, Git

---

## 📂 Project Structure

```
Hotel-Booking-and-Management-System/
├── Backend/                        # Spring Boot REST API
│   ├── src/main/java/learning/hotelbackend/
│   │   ├── controller/              # REST endpoints (Auth, Room, Booking, User, Role)
│   │   ├── service/                 # Business logic
│   │   ├── repository/              # Data access (JPA)
│   │   ├── model/                   # JPA entities (User, Role, Room, BookedRoom)
│   │   ├── request/ response/       # DTOs
│   │   ├── security/                # JWT filter & Spring Security config
│   │   ├── exception/                # Custom exceptions + global handler
│   │   └── config/                   # App configuration & data seeding
│   ├── src/main/resources/
│   │   └── application.properties
│   └── Dockerfile
│
└── Frontend/                       # React Frontend
    ├── src/
    │   ├── components/
    │   │   ├── admin/                # Admin dashboards
    │   │   ├── auth/                 # Login, register, password reset
    │   │   ├── booking/               # Booking flow & confirmation
    │   │   ├── room/                  # Room listing & details
    │   │   └── layout/ common/ utils/ # Shared UI & API calls
    │   └── assets/
    └── vite.config.js
```

---

## 🔑 API Reference

> All protected routes require an `Authorization: Bearer <JWT>` header.

### Authentication
| Method | Endpoint | Access | Description |
|---|---|---|---|
| `POST` | `/auth/register-user` | Public | Register a new account |
| `GET` | `/auth/verify-email` | Public | Verify email via token |
| `POST` | `/auth/login` | Public | Log in and receive a JWT |
| `POST` | `/auth/forgot-password` | Public | Request a password reset email |
| `POST` | `/auth/reset-password` | Public | Reset password with a valid token |

### Rooms
| Method | Endpoint | Access | Description |
|---|---|---|---|
| `GET` | `/rooms/all-rooms` | Public | Get all rooms |
| `GET` | `/rooms/available-rooms` | Public | Search available rooms by date range & type |
| `GET` | `/rooms/room/{roomId}` | Public | Get a single room's details |
| `GET` | `/rooms/room/types` | Public | Get distinct room types |
| `POST` | `/rooms/add/new-room` | Admin | Add a new room |
| `PUT` | `/rooms/update/{roomId}` | Admin | Update a room |
| `DELETE` | `/rooms/delete/room/{roomId}` | Admin | Delete a room |

### Bookings
| Method | Endpoint | Access | Description |
|---|---|---|---|
| `POST` | `/bookings/room/{roomId}/booking` | Auth | Book a room |
| `GET` | `/bookings/confirmation/{confirmationCode}` | Public | Look up a booking by confirmation code |
| `GET` | `/bookings/user/{email}/bookings` | Auth | Get a user's bookings |
| `GET` | `/bookings/all-bookings` | Admin | Get all bookings |
| `DELETE` | `/bookings/booking/{bookingId}/delete` | Auth / Admin | Cancel a booking |

### Users & Roles
| Method | Endpoint | Access | Description |
|---|---|---|---|
| `GET` | `/users/all` | Admin | Get all users |
| `GET` | `/users/{email}` | Auth / Admin | Get a user's profile |
| `DELETE` | `/users/delete/{email}` | Auth / Admin | Delete a user |
| `GET` | `/roles/all-roles` | Admin | Get all roles |
| `POST` | `/roles/create-new-role` | Admin | Create a role |
| `POST` | `/roles/assign-user-to-role` | Admin | Assign a role to a user |
| `POST` | `/roles/remove-user-from-role` | Admin | Remove a role from a user |
| `DELETE` | `/roles/delete/{roleId}` | Admin | Delete a role |

---

## ⚡ Quick Start

### Prerequisites
- Java 17+
- Node.js 18+
- PostgreSQL 14+
- Maven 3.8+ (or the included `mvnw` wrapper)

```bash
# 1. Clone the repo
git clone https://github.com/V1vekgupta/Hotel-Booking-and-Management-System.git
cd Hotel-Booking-and-Management-System

# 2. Start the backend
cd Backend
cp .env.example .env       # Fill in your credentials
./mvnw spring-boot:run

# 3. Start the frontend (new terminal)
cd ../Frontend
cp .env.example .env       # Fill in your credentials
npm install
npm run dev
```

> ⚠️ Make sure PostgreSQL is running and the target database exists before starting the backend.

Alternatively, build and run the backend with Docker:
```bash
cd Backend
docker build -t lakeside-hotel-backend .
docker run -p 9192:9192 --env-file .env lakeside-hotel-backend
```

---

## 🔐 Environment Variables

### Backend — `Backend/.env`
```env
SERVER_PORT=9192

DATABASE_URL=jdbc:postgresql://localhost:5432/hotel_db
DATABASE_USERNAME=your_db_username
DATABASE_PASSWORD=your_db_password
DATABASE_DRIVER=org.postgresql.Driver

HIBERNATE_DIALECT=org.hibernate.dialect.PostgreSQLDialect
DDL_AUTO=update

AUTH_TOKEN_EXPIRATION_IN_MS=86400000
AUTH_TOKEN_JWT_SECRET=your_base64_encoded_jwt_secret

APP_FRONTEND_URL=http://localhost:5173
APP_ADMIN_EMAIL=admin@lakesidehotel.com
APP_ADMIN_PASSWORD=change_me_immediately

MAIL_FROM=your_email@example.com
MAIL_HOST=smtp-relay.brevo.com
MAIL_PORT=587
MAIL_USERNAME=your_smtp_username
MAIL_PASSWORD=your_smtp_password
```

> ⚠️ `AUTH_TOKEN_JWT_SECRET` must be a **Base64-encoded** string — the app decodes it directly and will fail to start otherwise.

### Frontend — `Frontend/.env`
```env
VITE_API_BASE_URL=http://localhost:9192
```

> ⚠️ Never commit `.env` files. Add `.env` to `.gitignore` and use `.env.example` as a committed template.

---

## 📸 Screenshots

<div align="center">

| Home Page | Room Listing |
|:---:|:---:|
| _add screenshot_ | _add screenshot_ |

| Booking Flow | Admin Dashboard |
|:---:|:---:|
| _add screenshot_ | _add screenshot_ |

</div>

> 📝 Drop screenshots into a `docs/screenshots/` folder and reference them as `![Home Page](docs/screenshots/home.png)`. Send me the images (or the deployed link above) and I'll wire both sections up for real.

---

## 🌟 Future Improvements

- Add a `BookingStatus` lifecycle (pending / confirmed / completed / cancelled) instead of raw row existence
- Integrate real payment processing via Stripe
- Build an admin analytics dashboard (occupancy, revenue, upcoming check-ins)
- Add room reviews & ratings, and a guest wishlist
- Support coupon / discount codes at checkout
- Move to refresh-token auth with HttpOnly cookies
- Deploy via Docker Compose & CI/CD (GitHub Actions)
- Write unit and integration tests (JUnit 5, Mockito, React Testing Library)

---

## 🤝 Contributing

Contributions are welcome! Feel free to fork this repository and submit a pull request.

1. Fork the repository
2. Create a feature branch: `git checkout -b feature/your-feature`
3. Commit your changes: `git commit -m "feat: add your feature"`
4. Push and open a Pull Request

---

## 📄 License

This project is licensed under the **MIT License**
---

<div align="center">

Built with ❤️ by **[Vivek Gupta](https://github.com/V1vekgupta)**

⭐ Star this repo if you found it useful!

</div>
