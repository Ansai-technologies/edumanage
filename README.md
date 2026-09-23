# edumanage
Ansai's product and Operational Infra for educational institutions

# EduManage

Ansai's product and operational infrastructure
for educational institutions in Africa.

EduManage is the first product line of Ansai Technologies
and the beachhead of the Ansai ecosystem.
It is the trust anchor — the product that earns Ansai
the right to serve every community its schools sit in.

---

## What EduManage is

EduManage is the operational infrastructure for
Kenyan secondary schools — CBC and 844 compliant,
multi-tenant, offline-capable, built for the actual
conditions schools experience.

If EduManage went offline for a week, the schools
depending on it would feel it in daily operations.
That is the standard it is built to.

> **Note (2026-09-23):** offline capability is the Labs track's first build
> milestone — no offline/sync code exists in this repo yet. Customer-facing
> copy must not claim it as shipped until the Labs build demonstrates sync
> behavior. See `docs/differentiation-brief.md`.

---

## Reading order for new engineers

Before touching this codebase:

1. Read ansai-core/AGENTS.md — the global constitution
2. Read ansai-core/CONTEXT.md — the defined terms
3. Read this repository's AGENTS.md — the local extension
4. Read this repository's CONTEXT.md — school domain language
5. Read CHANGELOG.md — what has changed recently
6. Read relevant ADRs in ansai-core/docs/decisions/

Do not write code before reading these five things.
The codebase reflects decisions made in those documents.
Understanding the decisions is how you understand the code.

---

## Architecture

EduManage inherits from Ansai Core:
ansai-core/
@ansai/auth      ← authentication
@ansai/tenancy   ← tenant isolation (school_id scoping)
@ansai/roles     ← 22-role RBAC system
@ansai/pipeline  ← data tributary to Ansai Ziwa
@ansai/events    ← event emission
@ansai/audit     ← audit logging

EduManage extends Core with:
- School DNA configuration (schoolType, schoolGender,
  schoolLevel, schoolCategory)
- CBC/CBE compliance module
- Fee management module
- Attendance module
- Examinations module
- Parent portal
- Staff management
- Billing and subscription management

---

## The tenant model

Every school is a tenant.
Every query is scoped to school_id.
This is enforced at middleware level — not application level.
A query without tenant scoping is a gross violation.
See ansai-core/AGENTS.md Section 04.

---

## Stack

Backend: Fastify · Prisma · PostgreSQL
Frontend: React · TypeScript · Vite
Deployment: Render (API) · Cloudflare Pages (web)
DNS: Cloudflare
Storage: Cloudflare R2

---

## Repository structure
edumanage/
├── AGENTS.md       ← local agent constitution
├── CONTEXT.md      ← school domain language
├── CHANGELOG.md    ← what changed and why
├── README.md       ← this file
├── PRD/            ← product requirements documents
├── plans/          ← implementation plans
└── apps/
├── web/        ← React frontend
└── api/        ← Fastify backend

---

*EduManage · Ansai Technologies · Nairobi, Kenya*
*edumanage.co.ke*
