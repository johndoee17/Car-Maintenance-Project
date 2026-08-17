# Car Maintenance Tracker

A secure full-stack web application aligned with the submitted technical report. The implemented MVP includes:

- User registration and login
- JWT-protected routes
- Owner-scoped vehicle CRUD
- Owner-scoped service and maintenance CRUD
- Dashboard summaries from MongoDB
- Client and server validation
- Cross-user access protection
- Cascading service cleanup when a vehicle is deleted
- Loading, empty, success and error states

## Technology

- Frontend: React + Vite + React Router
- Backend: Node.js + Express
- Database: MongoDB + Mongoose
- Authentication: JSON Web Token (JWT) + bcrypt password hashing

## 1. Prerequisites

Install:

- Node.js 20.19+
- MongoDB locally, or create a MongoDB Atlas database

## Optional: start MongoDB with Docker

If you already use Docker, run:

```bash
docker compose up -d
```

This exposes MongoDB on `mongodb://127.0.0.1:27017`.

## 2. Configure the backend

Copy `backend/.env.example` to `backend/.env` and update the values:

```env
PORT=5000
MONGODB_URI=mongodb://127.0.0.1:27017/car-maintenance-tracker
JWT_SECRET=replace-this-with-a-long-random-secret
JWT_EXPIRES_IN=7d
CLIENT_ORIGIN=http://localhost:5173
```

## 3. Configure the frontend

Copy `frontend/.env.example` to `frontend/.env`.

```env
VITE_API_URL=http://localhost:5000/api
```

## 4. Install dependencies

From the project root:

```bash
npm install
npm run install:all
```

## 5. Run in development

```bash
npm run dev
```

Open `http://localhost:5173`.

## Suggested demonstration flow

1. Register User A and create a vehicle.
2. Add, edit and remove service records for that vehicle.
3. Demonstrate dashboard totals and recent services.
4. Register User B in another browser/incognito session.
5. Demonstrate that User B cannot access User A's vehicle/service IDs through the API.
6. Demonstrate validation by submitting invalid mileage/cost values.
7. Delete a vehicle and confirm its dependent service records are removed.

## Main API routes

### Authentication

- `POST /api/auth/register`
- `POST /api/auth/login`
- `GET /api/auth/me`

### Vehicles

- `GET /api/vehicles`
- `POST /api/vehicles`
- `GET /api/vehicles/:id`
- `PUT /api/vehicles/:id`
- `DELETE /api/vehicles/:id`

### Services

- `GET /api/vehicles/:vehicleId/services`
- `POST /api/vehicles/:vehicleId/services`
- `GET /api/services/:id`
- `PUT /api/services/:id`
- `DELETE /api/services/:id`

### Dashboard

- `GET /api/dashboard/summary`

## Security notes

The backend never trusts a resource ID by itself for private data. Vehicle and service queries are always constrained by the authenticated user's ID. Passwords are stored as hashes, secrets are read from environment variables, and protected API routes require a valid bearer token.

## Deferred backlog items

The final MVP intentionally does not implement fuel tracking, expense tracking, reminders, receipt upload or mileage-based recommendations. Those features remain future work, matching the final scope documented in the report.

## Evidence support files

- `TECHNICAL_EVIDENCE_CHECKLIST.md` lists the screenshots/code evidence to capture.
- `API_TESTS.http` contains ready-to-edit API and cross-user security tests for VS Code REST Client or similar HTTP clients.
