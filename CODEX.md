# CODEX.md
## DORA TPRM Web Application – Instructions for Codex

This repository contains a browser-based internal web application for DORA ICT Third-Party Providers Risk Management.

The product goal is to create a complete operational resilience cockpit for ICT third-party providers, contracts, ICT services, critical or important business functions, provider risk, concentration risk, replaceability, exit strategy, evidence and DORA reporting readiness.

## 1. Product context

The application is designed for an organization that must manage ICT third-party risk under DORA. The application must support:

1. ICT provider register.
2. ICT contractual arrangement register.
3. ICT service register.
4. Mapping of ICT services to business functions.
5. Identification of critical or important functions.
6. Provider, service and contract risk assessment.
7. Concentration risk and dependency analysis.
8. Exit strategy and replaceability tracking.
9. DORA contractual clause gap tracking.
10. Evidence repository and audit trail.
11. Exportable reports, including preparation data for Register of Information.

## 2. Current repository state

This is MVP 0 – Technical Foundation.

The full MVP 0 package was prepared as a Codex-ready ZIP. If the source files are not yet expanded in the repository, upload/extract the package contents into the repository root before starting module development.

Expected MVP 0 contents:

1. Next.js / React / TypeScript scaffold.
2. PostgreSQL database configuration.
3. Prisma schema with the main DORA TPRM entities.
4. Local session-based authentication using credentials from `.env`.
5. Dashboard page.
6. Provider page placeholder.
7. Docker Compose for application and database.
8. Seed script with demo records.
9. Documentation and Codex implementation plan.

## 3. Recommended implementation order

Codex should implement the application module by module in this order:

1. MVP 1 – Provider Register CRUD.
2. MVP 2 – Contract Register CRUD and provider linkage.
3. MVP 3 – ICT Service Register CRUD and contract/provider linkage.
4. MVP 4 – Business Function Register and service-to-function mapping.
5. MVP 5 – Risk Assessment Engine.
6. MVP 6 – Executive and Operational Dashboard.
7. MVP 7 – Exit Strategy and Replaceability module.
8. MVP 8 – DORA Contractual Clause Gap Tracker.
9. MVP 9 – Evidence Repository and Audit Log.
10. MVP 10 – Reports and Export module.

Do not skip modules. Each module must remain deployable and testable.

## 4. Development rules

Use the following rules for all work:

1. Keep the application as a modular monolith for now.
2. Use Next.js App Router.
3. Use TypeScript.
4. Use Prisma for all database access.
5. Use server actions or API routes consistently.
6. Avoid introducing unnecessary dependencies.
7. Keep UI professional, clean, executive-friendly and suitable for risk/compliance users.
8. Keep all forms validated on both client and server side where relevant.
9. Add soft delete where business records should not disappear permanently.
10. Maintain audit log entries for create, update, deactivate and delete actions.
11. Do not store production secrets in the repository.
12. Do not remove existing documentation.
13. Do not change the data model without updating docs/architecture/data-model.md.
14. Every module must include acceptance criteria and a short test checklist.

## 5. UI style guidance

Use a modern enterprise UI:

1. Left sidebar navigation.
2. Top page header with title, description and primary action.
3. KPI cards for dashboards.
4. Tables with filters, search, sorting and clear actions.
5. Details pages with tabs or clear sections.
6. Risk badges using consistent labels: Critical, High, Medium, Low, Not assessed.
7. Contract gap badges using consistent labels: Compliant, Minor Gap, Major Gap, Critical Gap, Not Assessed.
8. Use empty states with helpful instructions.

## 6. MVP 1 Codex task

Start with MVP 1 – Provider Register CRUD.

Implement:

1. Provider list using data from PostgreSQL through Prisma.
2. Search by provider name, legal entity name, type and owner.
3. Filters for provider status, risk rating, criticality and provider type.
4. Add provider page/form.
5. Edit provider page/form.
6. Provider details page.
7. Deactivate provider action using `deletedAt` or status.
8. Basic audit log creation for create/update/deactivate.
9. Dashboard KPI update using provider data.
10. Empty state when no providers exist.

## 7. Before opening a pull request

Run:

```bash
npm install
npm run prisma:generate
npm run build
```

If the database is available locally:

```bash
docker compose up -d postgres
npm run prisma:push
npm run db:seed
npm run dev
```

Check:

1. Login works.
2. Dashboard loads.
3. Provider list loads.
4. Add provider works.
5. Edit provider works.
6. Deactivate provider works.
7. No TypeScript build errors.
8. No console errors for normal navigation.
