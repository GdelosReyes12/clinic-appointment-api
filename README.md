# Clinic Appointment API

This project is a simple Clinic Appointment API built using FastAPI and Docker.

## Laboratory Context

This project was developed in an offline Windows 11 laboratory environment.

Python was not installed directly on the computer. The application was executed using Docker and a prebuilt Docker image named clinic-fastapi-base:1.0.

## Features

- Create clinic appointments
- View all appointments
- View one appointment
- Update appointment details
- Cancel appointments

## Technologies Used

- Python
- FastAPI
- Docker
- Git

## How to Run

docker compose up --build

Open http://localhost:8000/docs.

## Authentication

This API uses simple bearer token authentication to protect appointment-related endpoints.

### Test Account

| Field    | Value               |
|----------|---------------------|
| Username | admin               |
| Password | clinic123           |
| Token    | clinic-secret-token |

### How to Log In

Send a POST request to the login endpoint with the test account credentials.

**Endpoint:** `POST /login`

**Request body:**
```json
{
  "username": "admin",
  "password": "clinic123"
}
```

**Response:**
```json
{
  "access_token": "clinic-secret-token",
  "token_type": "bearer"
}
```

### Public Endpoints

These endpoints do not require a token.

| Method | Endpoint | Description          |
|--------|----------|----------------------|
| GET    | /        | Welcome message      |
| POST   | /login   | Login to get a token |

### Protected Endpoints

These endpoints require a valid bearer token in the Authorization header.

| Method | Endpoint                        | Description           |
|--------|---------------------------------|-----------------------|
| GET    | /me                             | View current user     |
| GET    | /appointments                   | View all appointments |
| GET    | /appointments/{appointment_id}  | View one appointment  |
| POST   | /appointments                   | Create appointment    |
| PUT    | /appointments/{appointment_id}  | Update appointment    |
| DELETE | /appointments/{appointment_id}  | Cancel appointment    |

### How to Authorize in Swagger UI

1. Open http://localhost:8000/docs
2. Click the **Authorize** button
3. Enter `clinic-secret-token` in the value field
4. Click **Authorize** then **Close**
5. Protected endpoints can now be tested

### Educational Limitation

This authentication approach is for instructional purposes only and is not suitable for production use. The following limitations apply:

- The token is a plain hardcoded string with no expiration
- Passwords are stored as plain text in the source code
- There is no database-backed user management
- There is no HTTPS encryption
- There is no role-based access control
- There is no audit logging

A real clinic appointment system should use secure password hashing, JWT tokens with expiration, database-backed users, HTTPS, and proper access control to protect patient data.
