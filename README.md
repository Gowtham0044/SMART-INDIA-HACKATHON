# SMART-INDIA-HACKATHON

# Intelligent Enterprise Assistant for Public Sector

Production-oriented full-stack web application for public-sector complaint management, document workflows, role-based dashboards, AI assistance, and operational analytics.

## Project Architecture

```text
SMART-INDIA-HACKATHON/
  backend/
    src/main/java/com/govassistant/publicsector/
      config/        Security, CORS, seed data
      controller/    REST API controllers
      dto/           Request and response DTOs
      entity/        JPA entities and enums
      exception/     Global exception handling
      repository/    Spring Data JPA repositories
      security/      JWT filter, token service, user details
      service/       Business logic and AI orchestration
    src/main/resources/application.yml
    pom.xml
  frontend/
    src/api/         Axios API clients
    src/components/  Shared dashboard components
    src/context/     Auth context
    src/layouts/     App shell
    src/pages/       Citizen, employee, admin, auth, analytics screens
  database/
    schema.sql
    sample-data.sql
  docker-compose.yml
```

## Core Features

- JWT authentication with BCrypt password hashing.
- RBAC for `CITIZEN`, `EMPLOYEE`, and `ADMIN`.
- Complaint creation, assignment, status updates, and tracking.
- Secure PDF/PNG/JPG upload with metadata and AI summary placeholder.
- In-app notifications.
- Admin user, department, complaint, and analytics views.
- AI assistant endpoints for FAQ, policy search guidance, complaint classification, document summarization, and recommendations.

## ER Diagram Description

- `roles` has many `users`.
- `departments` has many `users` and many `complaints`.
- `users` submit many `complaints` as citizens.
- `users` can be assigned many `complaints` as employees.
- `complaints` has many `documents`.
- `users` receive many `notifications`.
- `users` can generate `audit_logs`.

## API Summary

- `POST /api/auth/register`
- `POST /api/auth/login`
- `GET /api/departments`
- `POST /api/complaints`
- `GET /api/complaints/mine`
- `GET /api/complaints/assigned`
- `GET /api/complaints`
- `PATCH /api/complaints/{id}/status`
- `PATCH /api/complaints/{id}/assign`
- `POST /api/documents/complaints/{complaintId}`
- `GET /api/documents?q=term`
- `GET /api/documents/{id}/download`
- `POST /api/ai/chat`
- `GET /api/notifications`
- `GET /api/admin/users`
- `GET /api/admin/departments`
- `POST /api/admin/departments`
- `GET /api/analytics/summary`

## Local Development

### Backend

```bash
cd backend
mvn spring-boot:run -Dspring-boot.run.profiles=dev
```

Backend runs at `http://localhost:8080`.
The `dev` profile uses an embedded H2 database so the app can run without a local MySQL server. The default profile remains configured for MySQL.

### Frontend

```bash
cd frontend
npm install
npm run dev
```

Frontend runs at `http://localhost:5173`.

## Docker

```bash
docker compose up --build
```

- Frontend: `http://localhost:3000`
- Backend: `http://localhost:8080`
- MySQL: `localhost:3306`

## Seed Users

The backend automatically creates these accounts on startup:

| Role | Email | Password |
|---|---|---|
| Admin | `admin@gov.local` | `Password@123` |
| Employee | `employee@gov.local` | `Password@123` |
| Citizen | `citizen@example.com` | `Password@123` |

## AI Integration Notes

`AiService` currently provides deterministic local responses and classification so the project works without paid external dependencies. To connect OpenAI or a government-hosted NLP model, replace the methods in `backend/src/main/java/com/govassistant/publicsector/service/AiService.java` with calls through a secure AI gateway using `OPENAI_API_KEY`.

## Production Hardening Checklist

- Replace `JWT_SECRET` with a managed secret.
- Store uploaded files in S3/Azure Blob with virus scanning.
- Add refresh tokens and token revocation.
- Add audit logging aspects for all sensitive write operations.
- Add OpenAPI documentation.
- Add CI pipeline with backend tests, frontend build, container scanning, and deployment approvals.
=======
### OUTPUT

<img width="1919" height="1141" alt="Screenshot 2026-06-03 213944" src="https://github.com/user-attachments/assets/718d9e35-e17d-4186-bbc2-5e50c331b596" />

<img width="1919" height="1138" alt="Screenshot 2026-06-03 214031" src="https://github.com/user-attachments/assets/2ecba7b9-f42b-4e63-975b-0393711037a7" />
