# OIC Complaints Management System (CMS) — Production Project Scaffold

This repo contains a production-oriented scaffold for the OIC CMS using:
- **Backend**: .NET 8 Web API + EF Core + Identity + JWT + refresh tokens
- **Frontend**: Angular (standalone components) + Angular Material
- **Database**: SQL Server
- **Deployment**: Docker Compose + Nginx reverse proxy

## What is implemented (aligned to SOW)
- Public portal: complaint submission + ticket tracking (Ticket ID + Email)
- Internal portal: login + RBAC-ready endpoints
- Ticket lifecycle + comments (internal vs customer-visible)
- SLA matrix + escalation + SLA state (OnTime/Warning/Breached)
- Email templates and SMTP sender (toggle with config)
- Audit trail writes for core actions
- Basic analytics endpoint (dashboard KPIs + trend)
- CSV export endpoint

## Quick start (local)
### 1) Backend only
1. Install .NET 8 SDK and SQL Server.
2. Update `backend/src/CMS.Api/appsettings.json` connection string and JWT signing key.
3. Run:
   - `dotnet run --project backend/src/CMS.Api/CMS.Api.csproj`
4. Open Swagger (dev): `/swagger`

### 2) Full stack (Docker)
1. Build Angular and put output into `frontend/dist/` (run `npm install` then `npm run build`).
2. Run:
   - `docker compose up --build`
3. Browse:
   - Public portal: `http://localhost/`
   - API: `http://localhost/api/health`

## Default users (seed)
- `admin / ChangeMe!12345`
- `supervisor / ChangeMe!12345`

> Change these passwords immediately in production.

## Notes
- For first run, the backend uses `EnsureCreated()` for DB creation. For real production governance, switch to EF Migrations.
- Close/Reopen is restricted to Admin/Supervisor/Central roles.
