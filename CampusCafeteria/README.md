# Campus Cafeteria

Pre-order and pickup system for a campus cafeteria.

- `frontend/` React + Vite + TypeScript
- `backend/` Express + TypeScript, Oracle DB via `oracledb`
- `database/` SQL: schema, seed data, PL/SQL procedures, trigger, views

## Run locally
1. Backend: copy `backend/.env.example` to `backend/.env`, fill it in, then
   `cd backend && npm install && npm run dev`
2. Load the database (from `backend/`): `npx tsx src/run-schema.ts`, `src/run-seed.ts`,
   `src/install-queue-cursor.ts`, `src/install-order-procedures.ts`, `src/install-order-status.ts`,
   `src/install-status-trigger.ts`, `src/install-report-views.ts`, `src/scripts/set-demo-passwords.ts`
   (the scripts read `../database/...`, so run them from inside `backend/`)
3. Frontend: `cd frontend && npm install && npm run dev`

## Deploy
| Part | Where | Settings |
|---|---|---|
| Database | Oracle Autonomous DB (Always Free) | Allow access from anywhere, mTLS not required, use the TLS connection string |
| Backend | Render (Web Service) | Root dir `backend`, build `npm install --include=dev && npm run build`, start `npm start` |
| Frontend | Vercel | Root dir `frontend`, env `VITE_API_BASE` = backend URL + `/api` |

Backend env vars: `DB_USER`, `DB_PASSWORD`, `DB_CONNECT_STRING`, `JWT_SECRET`, `FRONTEND_URL`.
Health check: `<backend-url>/api/health`.
