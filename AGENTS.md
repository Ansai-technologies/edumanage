# EduManage — AGENTS.md
# Local Agent Constitution — Tier 1 Extension

Version: 1.0
Date: May 2026
Status: Active

---

## IMPORTANT — Read global constitution first

Before reading this file, read:
ansai-core/AGENTS.md — the global constitution

This file extends the global constitution.
It does not replace it.
If anything here appears to conflict with
ansai-core/AGENTS.md — the global file wins.
Flag the conflict as uncovered territory.

---

## 01 — What you are working on

EduManage is the operational infrastructure for
Kenyan secondary schools.
It is multi-tenant — every school is a tenant.
It handles real money, real student records,
real examination data.

The bursar using the fee module is a named human being
doing her job. The parent checking their child's balance
is a named human being checking on their child.
Build with that awareness at all times.

---

## 02 — The school domain

Before working on any EduManage feature, read:
edumanage/CONTEXT.md — the school domain language

Key terms you will encounter constantly:
- school_id — the tenant identifier, never missing
- tenantGuard — middleware that enforces tenant scoping
- School DNA — the configuration that cascades everywhere
- deriveSchoolConfig() — never bypass this
- TRANSITION — the default school level for 2026
- Bursar — the named human behind every financial feature

---

## 03 — EduManage-specific gross violations

In addition to the gross violations in ansai-core/AGENTS.md,
these are EduManage-specific violations that require
immediate stop and human judgment:

**Missing school_id scoping.**
Any query that does not include WHERE school_id = ?
or equivalent Prisma scope is a cross-tenant risk.
Stop. Flag. Ask for human review before proceeding.

**Bypassing deriveSchoolConfig().**
Any module that reads school configuration directly
from the database instead of through deriveSchoolConfig()
creates inconsistency risk across the system.
Stop. Use deriveSchoolConfig(). Always.

**Fee calculation without edge case handling.**
Any fee calculation that does not explicitly handle:
overpayment, duplicate payment, zero balance,
negative balance (credit), partial payment.
Stop. All five cases must be handled before the
feature is considered complete.

**Receipt without audit trail.**
Any payment flow that does not generate a receipt
with full audit trail — bursar ID, timestamp,
amount, method, previous balance, new balance.
Stop. The receipt is non-negotiable.

**Rank generation in CBC mode.**
CBC explicitly prohibits student ranking by KNEC.
Any feature that generates or displays student ranks
in a CBC school is a compliance violation.
Stop. Check schoolLevel before any ranking logic.

---

## 04 — The module structure

EduManage is organized into modules.
Each module owns its own data schema, API surface,
and UI surface.
Modules do not reach into each other's data directly.

Current modules:
- school-dna — School DNA configuration
- admissions — Student enrollment
- academics — Classes, streams, subjects, timetable
- attendance — Daily and period attendance
- examinations — Marks, grades, reports (CBC and 844)
- fees — Fee structures, invoices, payments, receipts
- staff — Staff records, roles, assignments
- parents — Parent portal and communication
- boarding — Dormitories, matron/patron management
- billing — Subscription and platform billing

When working in a module — stay in that module.
When you need data from another module, use its
defined API surface. Never query another module's
tables directly.

---

## 05 — The critical path for EduManage

These four areas require 100% test coverage before
any school handles real data.
In addition to the global critical paths:

**Fee calculations**
Every combination of: new payment, partial payment,
overpayment, duplicate prevention, balance update,
receipt generation.
Tests must cover all five edge cases.

**Tenant isolation**
Every query in every module must be tested to confirm
it cannot return data from a different school_id.
Tenant isolation tests run on every deployment.

**CBC compliance**
No-ranking enforcement must be tested in CBC mode.
SBA tracking must produce KNEC-exportable output.
Grade calculations must match KNEC's eight-level scale.

**Authentication and role enforcement**
Every route must be tested against the role matrix:
which roles can access it, which cannot.
A bursar must not be able to access principal reports.
A parent must not be able to edit student records.

---

## 06 — Tier 2 documents for EduManage

When working in specific areas within EduManage,
these Tier 2 documents provide deeper context.
Fetch them before working in the relevant area.

| Working area | Fetch this document |
|-------------|---------------------|
| Fee payments, billing | ansai-core/docs/context/finance-domain.md |
| Authentication, roles | ansai-core/docs/context/auth-rules.md |
| CBC compliance | edumanage/docs/context/cbc-rules.md |
| School DNA configuration | edumanage/docs/context/school-dna.md |
| Parent portal | edumanage/docs/context/parent-portal.md |

If a document does not exist yet — flag it as missing.
Do not invent rules not yet documented.

---

## 07 — Current deployment state

Backend: edumanage-api.onrender.com
Frontend: edumanage.co.ke (Cloudflare Pages)
Database: PostgreSQL on Render
Storage: Cloudflare R2
DNS: Cloudflare

Before making any change that affects the deployed
system — check the CHANGELOG.md for recent changes.
Check STATUS.md for anything currently broken.
Do not deploy without CI passing.

---

## 08 — Amendment record

Changes to this file follow Category 1 governance
for EduManage-specific additions and Category 2
governance for changes that affect other product lines.
All amendments logged in ansai-core/AMENDMENTS.md.
