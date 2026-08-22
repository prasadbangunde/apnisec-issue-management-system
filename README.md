# ApniSec — Enterprise Issue Management System

A full-stack issue management platform built with **Next.js, TypeScript, PostgreSQL, Prisma, and Tailwind CSS**.

The application provides user authentication, secure issue management, profile management, validation, rate limiting, and email notifications through a structured frontend/backend architecture.

## Features

* User registration and login
* JWT-based authentication
* HTTP-only authentication cookies
* Password hashing with bcrypt
* User profile management
* Create, view, update, and delete issues
* Issue filtering by type
* Issue priorities: Low, Medium, High, Critical
* Issue statuses: Open, In Progress, Resolved, Closed
* Issue ownership and authorization checks
* Request validation with Zod
* API rate limiting
* Standardized API responses and error handling
* Welcome email on user registration
* Email notification when an issue is created
* PostgreSQL database with Prisma ORM
* Responsive frontend built with Tailwind CSS

## Tech Stack

### Frontend

* Next.js 16
* React 19
* TypeScript
* Tailwind CSS
* Lucide React

### Backend

* Next.js App Router API Routes
* TypeScript
* JWT
* bcryptjs
* Zod
* Resend

### Database

* PostgreSQL
* Prisma ORM
* Prisma Migrations

## Architecture

The project follows a layered architecture that separates API routes, controllers, business logic, data access, validation, and utility functions.

```text
src/
├── app/
│   ├── api/
│   │   ├── auth/
│   │   ├── issues/
│   │   └── users/
│   ├── dashboard/
│   ├── login/
│   ├── profile/
│   └── register/
│
├── backend/
│   ├── controllers/
│   ├── errors/
│   ├── middlewares/
│   ├── repositories/
│   ├── services/
│   ├── types/
│   ├── utils/
│   └── validators/
│
├── components/
│   ├── auth/
│   ├── dashboard/
│   ├── home/
│   ├── layout/
│   └── ui/
│
└── lib/
    ├── api.ts
    └── prisma.ts

prisma/
├── schema.prisma
└── migrations/
```

### Request Flow

```text
Client
  ↓
Next.js API Route
  ↓
Controller
  ↓
Service Layer
  ↓
Repository Layer
  ↓
Prisma ORM
  ↓
PostgreSQL
```

This separation keeps HTTP handling, business logic, and database access independent from each other.

## Authentication & Security

The application implements several security mechanisms:

* Passwords are hashed using bcrypt before storage.
* JWTs are used for authenticated sessions.
* Authentication tokens are stored in HTTP-only cookies.
* Protected resources verify the authenticated user's identity.
* Users can only access and modify issues they own.
* Zod validates incoming authentication and issue data.
* API requests are rate-limited.
* Sensitive environment variables are excluded from version control.

### Password Requirements

Registration requires passwords to contain:

* At least 8 characters
* At least one uppercase letter
* At least one lowercase letter
* At least one number

## Issue Management

Each issue contains:

* Issue type
* Title
* Description
* Priority
* Status
* Owner
* Creation timestamp
* Last updated timestamp

### Issue Types

* Cloud Security
* Red Team Assessment
* VAPT

### Priorities

* Low
* Medium
* High
* Critical

### Statuses

* Open
* In Progress
* Resolved
* Closed

## API Endpoints

### Authentication

| Method | Endpoint             | Description                |
| ------ | -------------------- | -------------------------- |
| POST   | `/api/auth/register` | Register a new user        |
| POST   | `/api/auth/login`    | Authenticate a user        |
| POST   | `/api/auth/logout`   | Log out the current user   |
| GET    | `/api/auth/me`       | Get the authenticated user |

### Issues

| Method    | Endpoint          | Description           |
| --------- | ----------------- | --------------------- |
| GET       | `/api/issues`     | Get the user's issues |
| POST      | `/api/issues`     | Create an issue       |
| GET       | `/api/issues/:id` | Get a specific issue  |
| PUT/PATCH | `/api/issues/:id` | Update an issue       |
| DELETE    | `/api/issues/:id` | Delete an issue       |

### User

| Method  | Endpoint             | Description         |
| ------- | -------------------- | ------------------- |
| GET/PUT | `/api/users/profile` | Manage user profile |

## Database Design

The application uses PostgreSQL with Prisma ORM.

### User

```text
User
├── id
├── email
├── name
├── password
├── createdAt
└── updatedAt
```

### Issue

```text
Issue
├── id
├── type
├── title
├── description
├── priority
├── status
├── userId
├── createdAt
└── updatedAt
```

A user can own multiple issues, while each issue belongs to one user.

## Getting Started

### 1. Clone the repository

```bash
git clone https://github.com/prasadbangunde/apnisec-issue-management-system.git
cd apnisec-issue-management-system
```

### 2. Install dependencies

```bash
npm install
```

### 3. Configure environment variables

Create a `.env` file in the project root.

```env
DATABASE_URL=
DIRECT_URL=
JWT_SECRET=
RESEND_API_KEY=
EMAIL_FROM=
NEXT_PUBLIC_APP_URL=http://localhost:3000
```

Do not commit your `.env` file to GitHub.

### 4. Set up the database

Run the Prisma migrations:

```bash
npx prisma migrate dev
```

Generate the Prisma client if required:

```bash
npx prisma generate
```

### 5. Start the development server

```bash
npm run dev
```

Open:

```text
http://localhost:3000
```

## Available Scripts

```bash
npm run dev
```

Starts the development server with Turbopack.

```bash
npm run build
```

Creates a production build.

```bash
npm run start
```

Starts the production server.

```bash
npm run lint
```

Runs ESLint.

```bash
npx prisma studio
```

Opens Prisma Studio for database inspection.

## Project Highlights

* Layered backend architecture
* REST-style API endpoints using Next.js Route Handlers
* JWT authentication with HTTP-only cookies
* Database access through Prisma repositories
* Zod-based request validation
* Ownership-based authorization
* API rate limiting
* Centralized application errors
* Reusable React UI components
* PostgreSQL relational data model
* Email integration with Resend

## Future Improvements

* Role-based access control
* Admin dashboard
* Advanced issue search and filtering
* Pagination for large issue datasets
* Production-grade distributed rate limiting
* Automated testing
* CI/CD pipeline
* Monitoring and application logging
* Dockerized deployment

## Author

**Prasad Bangunde**

GitHub: https://github.com/prasadbangunde
