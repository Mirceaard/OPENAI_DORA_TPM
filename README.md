# DORA ICT Third-Party Risk Management Web App – MVP 0

This package is the technical foundation for the DORA ICT Third-Party Providers Management application.

MVP 0 includes:

- Next.js / React / TypeScript web application
- PostgreSQL database configuration
- Prisma data model for the main DORA entities
- Minimal environment-based login
- Protected dashboard
- Executive dashboard with live counters from the database
- Placeholder Provider Register page for MVP 1
- Docker Compose deployment option
- Seed script with sample data

---

## 1. What you need to install on your computer

For local development, install:

1. Node.js 22 LTS or newer
2. Docker Desktop
3. Visual Studio Code
4. Git, optional but recommended

For server deployment, you need:

1. Linux server or Windows server capable of running Docker
2. Docker and Docker Compose
3. Open inbound access to the selected web port, default `3000`
4. Later, a reverse proxy and HTTPS certificate should be added before production usage

---

## 2. First local run without Docker for the web app

Open a terminal in the project folder and run:

```bash
npm install
```

Create your environment file:

```bash
cp .env.example .env
```

On Windows PowerShell, use:

```powershell
Copy-Item .env.example .env
```

Edit `.env` and change at least:

```env
APP_ADMIN_EMAIL="admin@sibs.local"
APP_ADMIN_PASSWORD="ChangeMe123!"
AUTH_SECRET="replace-with-a-long-random-secret"
```

Start only the database using Docker:

```bash
docker compose up -d postgres
```

Generate Prisma client:

```bash
npm run prisma:generate
```

Push the database schema:

```bash
npm run prisma:push
```

Optional: add demo data:

```bash
npm run db:seed
```

Start the application:

```bash
npm run dev
```

Open in browser:

```text
http://localhost:3000
```

Login with the credentials configured in `.env`.

---

## 3. Run everything with Docker Compose

From the project folder:

```bash
docker compose up --build
```

Then open:

```text
http://localhost:3000
```

Important: the Docker Compose file contains default credentials. Before deploying on a shared server, replace these values in `docker-compose.yml` or use a production environment file.

---

## 4. Health check

After starting the app, test database connectivity:

```text
http://localhost:3000/api/health
```

Expected result:

```json
{
  "status": "ok",
  "database": "connected"
}
```

---

## 5. Current application pages

| URL | Purpose |
|---|---|
| `/login` | Minimal MVP login |
| `/dashboard` | Executive dashboard with database counters |
| `/providers` | Placeholder for the next module: Provider Register |
| `/api/health` | Technical health check |

---

## 6. What you should check after receiving this MVP 0 package

1. Unzip the package.
2. Open the folder in Visual Studio Code.
3. Create `.env` from `.env.example`.
4. Change admin password and `AUTH_SECRET`.
5. Start PostgreSQL with Docker.
6. Run Prisma schema push.
7. Start the app.
8. Login.
9. Confirm the dashboard opens.
10. Optionally run the seed script and confirm the dashboard counters change.

---

## 7. Development sequence after MVP 0

The next module is MVP 1 – Provider Register.

MVP 1 will add:

1. Provider list from database
2. Search and filters
3. Add provider form
4. Edit provider form
5. Provider detail page
6. Soft delete / deactivate provider
7. Status badges
8. Basic audit log for provider changes

After you confirm MVP 0 runs on your side, the Provider Register module can be added on top of this package.

---

## 8. Security notes

This MVP uses minimal environment-based login so that the application can be started quickly.

Before real production usage, add:

1. Active Directory / Azure AD / SSO integration
2. HTTPS
3. Strong password policy or external identity provider
4. Real role-based access control
5. Secure document storage
6. Backups
7. Infrastructure monitoring
8. Production-grade audit logging

---

## 9. Important implementation note

This MVP is a working technical foundation, not yet a full DORA-compliant business application. The business functionality will be added module by module.

---

# Codex-ready documentation

This package includes complete documentation for continuation in Codex.

Start here:

1. `CODEX.md` – main Codex instruction file.
2. `docs/codex/01-codex-onboarding.md` – onboarding guide.
3. `docs/codex/02-codex-master-prompt.md` – prompt to start Codex work.
4. `docs/codex/03-codex-task-prompts.md` – module-by-module prompts.
5. `docs/codex/04-github-and-codex-workflow.md` – GitHub/Codex workflow.
6. `docs/codex/05-ready-to-use-issues.md` – issue bodies for GitHub.
7. `docs/modules/` – module specifications.
8. `docs/runbooks/` – setup and deployment instructions.
9. `docs/testing/test-plan.md` – test plan.
10. `docs/dora/dora-requirements-mapping.md` – DORA-oriented mapping.

Recommended first Codex task:

```text
Implement MVP 1 – Provider Register CRUD based on CODEX.md and docs/modules/mvp-1-provider-register.md. Keep the application deployable. Run build and fix TypeScript errors.
```
