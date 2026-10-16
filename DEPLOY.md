# CoOpSphere Deployment

## Recommended deployment

- Frontend: Render Static Site
- Backend: Render Web Service
- Database: PostgreSQL (Neon, Render PostgreSQL, or another PostgreSQL provider)
- Repository: GitHub

## 1. Push the project to GitHub

Extract this ZIP and push the project root to your GitHub repository.

## 2. Create PostgreSQL

Create a PostgreSQL database and copy its connection string.

It should use the SQLAlchemy/psycopg format expected by the backend, for example:

`postgresql+psycopg://USER:PASSWORD@HOST:5432/DATABASE`

## 3. Deploy with Render Blueprint

In Render, create a new Blueprint and select the GitHub repository.

Render will read `render.yaml` and create:

- `coopsphere-api`
- `coopsphere-web`

When prompted, provide `DATABASE_URL`.

## 4. Verify backend

Open:

`https://YOUR-BACKEND.onrender.com/health`

Expected response:

`{"status":"healthy"}`

Then open:

`https://YOUR-BACKEND.onrender.com/docs`

## 5. Verify frontend

Open the generated frontend URL.

The frontend is configured to call:

`YOUR-BACKEND/api/v1`

## Important before public production

The current project contains demo seed accounts/data. This is useful for SIH/demo deployment, but for a real production deployment:

1. Remove automatic seeding from the backend start command.
2. Change/remove demo passwords.
3. Generate a strong JWT secret.
4. Review CORS settings.
5. Pin frontend dependency versions.
6. Add automated tests and production logging.

For a college/SIH demonstration, the included seed step can remain temporarily.
