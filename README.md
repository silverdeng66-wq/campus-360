# CAMPUS360 — University Management System

A complete role-based University Management System with secure authentication, an Administrator Portal, and a Student Portal — built with Node.js, Express, MongoDB, React, and Vite.

## Features

- **Secure Authentication** — JWT-based login, bcrypt password hashing, password recovery, rate limiting
- **Administrator Portal** — Full CRUD for students, departments, courses, enrollments, users, reports, audit logs
- **Student Portal** — Personalized dashboard, course views, enrollment management, academic records, notifications
- **Role-Based Access Control** — Backend-enforced permissions; students can only access their own records
- **Real MongoDB Data** — Live statistics via MongoDB aggregation pipelines, no hardcoded data
- **Responsive Design** — Works on desktop, tablet, and mobile

## Tech Stack

| Layer | Technology |
|-------|-----------|
| Backend | Node.js, Express, Mongoose |
| Database | MongoDB |
| Frontend | React 18, Vite 5, React Router 6 |
| Auth | JWT, bcryptjs |
| Charts | Recharts |
| Icons | Lucide React |
| Notifications | React Hot Toast |

## Project Structure

```
CAMPUS360/
├── backend/          # Express API + MongoDB
├── frontend/         # React + Vite SPA
├── docs/             # Documentation
├── package.json      # Root scripts
└── README.md
```

## Quick Start

### Prerequisites

- Node.js 18+
- MongoDB (running on localhost:27017)

### 1. Install Dependencies

```bash
cd backend && npm install
cd ../frontend && npm install
```

### 2. Configure Environment

Backend `.env` is pre-configured for local development. Update if your MongoDB URI differs:

```bash
# backend/.env
MONGODB_URI=mongodb://localhost:27017/campus360
JWT_SECRET=your_secret_here
```

### 3. Start MongoDB

Ensure MongoDB is running on `localhost:27017`.

### 4. Seed the Database

This creates an admin account, departments, courses, students, and enrollments:

```bash
cd backend
node scripts/seedDatabase.js
```

### 5. Start the Backend

```bash
cd backend
npm run dev
```

### 6. Start the Frontend

```bash
cd frontend
npm run dev
```

### 7. Open the App

Navigate to `http://localhost:5173`

## Demo Credentials

| Role | Email | Password |
|------|-------|----------|
| Administrator | admin@campus360.edu | Admin@123456 |
| Student | alice@student.campus360.edu | Student@123 |

## Initial Admin Setup

If you need to create just an admin without seeding all data:

```bash
cd backend
node scripts/createAdmin.js
```

## API Endpoints

### Auth
- `POST /api/auth/login` — Login
- `POST /api/auth/logout` — Logout
- `GET /api/auth/me` — Current user
- `POST /api/auth/forgot-password` — Request reset
- `POST /api/auth/reset-password` — Reset password
- `PUT /api/auth/change-password` — Change password

### Students (admin: all, student: own only)
- `GET /api/students` — List (admin)
- `POST /api/students` — Create (admin)
- `GET /api/students/:id` — View (admin or own)
- `PUT /api/students/:id` — Update (admin or own limited fields)
- `DELETE /api/students/:id` — Archive/delete (admin)

### Departments, Courses, Enrollments, Users, Reports, Audit Logs, Notifications
See full API documentation in `docs/api-documentation.md`.

## Security

- Passwords hashed with bcrypt (12 rounds)
- JWT tokens with expiry
- Role-based authorization middleware on every protected route
- Rate limiting on auth endpoints
- Helmet security headers
- MongoDB sanitization (NoSQL injection prevention)
- CORS restrictions
- Password reset tokens are hashed and time-limited (1 hour)
- Never exposes password hashes to frontend
- Prevents privilege escalation (students can't change roles)
- Protects last active admin from deletion

## Testing

```bash
cd backend
npm test
```

Tests cover: admin/student login, invalid credentials, inactive accounts, role-based access, privilege escalation prevention, password hashing verification, and forgot-password user enumeration prevention.

## License

MIT
