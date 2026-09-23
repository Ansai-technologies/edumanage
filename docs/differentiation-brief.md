# EduManage — Differentiation Brief (Labs track)

Date: 2026-09-23 | Status: Draft — for founder review
Basis: `reviews/2026-09-23-edumanage-competitors.md` (round-1 competitor research,
approved for merge as edumanage#1).

> **Honesty note.** Claims below are tagged:
> `[committed]` = architectural commitment in the EduManage constitution/docs —
> must be proven in the Labs build before any customer-facing copy uses it.
> `[roadmap]` = not yet built, not committed.
> Nothing in this repo has shipped code yet (apps/ are stubs).

---

## 1. Positioning statement

EduManage is the **operational infrastructure for Kenyan secondary schools** —
CBC and 844 compliant, multi-tenant, **offline-capable** `[roadmap]`, built for the actual
conditions schools experience.

It is not another cloud dashboard that breaks when the Wi-Fi does. It is the
trust anchor: the system the bursar, the principal, and the parent each trust
with real money, real records, and real results.

## 2. Where EduManage wins — the three headline differentiators

### 2a. Offline-capable operations — the structural gap in the market `[roadmap]`

Every competitor surveyed is cloud-only:

| Competitor | Offline story |
|---|---|
| Cloud School (cloudschool.co.ke) | cloud-based, none advertised |
| Elimikasasa (elimikasasa.co.ke) | none advertised |
| Citycloud (citycloudschool.co.ke) | none advertised |
| Shulevora (shulevora.co.ke) | none advertised |
| Jibu ERP (jibuerp.com) | none advertised |

Kenyan school connectivity still costs ~$45/month and is unreliable outside
towns (UNICEF Giga, 2026 — per round-1 research). When the network fails,
cloud-only systems stop working — attendance can't be taken, fees can't be
recorded, exams can't be entered.

EduManage's README sets the bar: *"If EduManage went offline for a week, the
schools depending on it would feel it in daily operations. That is the standard
it is built to."* This is the headline because no competitor can credibly
answer it — and because in Kenya, offline isn't an edge case, it's Tuesday.

**Rule:** the headline leads with offline as a commitment; no customer copy
claims it as shipped until the Labs build demonstrates sync behavior.
(Retagged `[roadmap]` 2026-09-23: the commitment currently exists only as a
README aspiration — zero offline/sync code in the repo. It promotes to
`[committed]` when a real offline/sync commitment lands in AGENTS.md/CONTEXT.md
or the Labs sync milestone is demonstrated.)

### 2b. Kenya-native domain model — School DNA + TRANSITION defaults `[committed]`

Competitors bolt CBC onto generic school software. EduManage starts from how
Kenyan schools actually run in 2026:

- **School DNA** (schoolType / schoolGender / schoolLevel / schoolCategory)
  configures behavior system-wide — never bypassed.
- **TRANSITION** is the default school level — the constitution was written
  during the CBC transition and assumes it, not as a plugin.
- Dual-curriculum (CBC + 844) handling is default, not a module add-on.

This is the answer to "why not just Cloud School": generic systems encode
generic assumptions; EduManage encodes Kenyan ones.

### 2c. Compliance-by-design `[committed]`

KNEC CBA export readiness, SBA tracking, and **no-ranking enforcement in CBC
mode** (a KNEC requirement competitors do not advertise). Boards of
management and auditors — the people who sign contracts — care about this
more than feature lists.

## 3. Secondary differentiators (trust-anchor material)

- **Bursar-grade financial rigor** `[roadmap]` — fee edge cases (overpayment,
  duplicate, partial, credit) and receipt audit trails as first-class design
  concerns, not afterthoughts. The bursar is a named human being; money that
  can't be reconciled is trust that can't be rebuilt.
- **Tenant model as a selling point** `[committed]` — every query scoped to
  `school_id`, enforced at middleware. Multi-tenant from day one; school data
  can never leak across schools by design. (Elimikasasa's aggressive switching
  offers target multi-school groups; isolation guarantees matter to them.)
- **Role-based access + full audit log** `[committed]` (inherited from Ansai
  Core) — who did what, when, to which record. Auditors and principals ask for
  this. (The README's "22-role" count is unverified — the constitution names
  the `@ansai/roles` package only; the specific count stays out of customer
  copy until confirmed.)

## 4. What we do NOT lead with

- **Agentic operations / "AI".** The Baraza/agent infrastructure is Ansai's
  long-term edge, but Citycloud already markets an "AI assistant" and "AI
  document generation". Until EduManage's agentic layer is demonstrably
  better than a chatbot, pitching it invites a comparison we lose. Ship the
  core; the agents are the second act.
- **Price alone.** Elimikasasa anchors the market at KES 2,500/month flat,
  free under 100 students, one-term trial, and "Switch & Save" (12 months
  free + end-to-end migration). We cannot win a race to zero against that
  anchor — and shouldn't try. Our pricing must be defensible against the
  value of offline operations, not undercut a loss-leader.
- **Feature breadth.** Jibu ERP sells breadth (vehicle tracking, LMS,
  biometrics); Cloud School sells modules. EduManage sells depth in the
  Kenyan operational core: fees, attendance, exams, compliance — the things
  that run the school day.

## 5. The switching battleground

Round-1's most important finding: **switching costs are the real battleground,
not features.** Elimikasasa does end-to-end migration for free with 12 months
free. No differentiator survives a painful migration.

EduManage therefore needs a migration story, not just a better product:

1. **Excel-import migration** (table stakes — Shulevora already offers this).
2. **M-Pesa history import** — pull the school's existing paybill/till
   transaction history so fee balances reconcile on day one. Nobody advertises
   this; it is ours to take.
3. **Parallel-run onboarding** — the school runs EduManage alongside its old
   system for one term, with reconciliation reports showing the old system and
   EduManage agreeing. This converts trust from an obstacle into a sales tool.
4. **CBC data migration path** — assessment records, SBA entries, CBA history
   preserved across the move (the compliance-by-design angle, operationalized).

## 6. One-paragraph sales version — DRAFT COPY, not for use until the sync milestone is demonstrated

> Kenyan schools don't run on perfect connectivity. EduManage is being built
> for that reality: to keep working when the network doesn't, to speak Kenyan
> school language (School DNA, CBC + 844 as defaults), to be ready for KNEC
> compliance out of the box, and to treat your bursar's ledger with the rigor
> real money demands. We will migrate you from your current system — M-Pesa
> history included — and run parallel until your books agree.

## 7. Open questions (for the Labs track)

1. EduManage's own pricing is unset — the Labs track must propose a pricing
   strategy that answers Elimikasasa's KES 2,500/mo anchor without racing to
   zero (e.g., anchor on offline reliability + migration value).
2. Cloud School's current pricing is opaque (modular, unpublished) — needs a
   hands-on trial account to map before any head-to-head sales sheet is made.
3. Offline capability is `[roadmap]` (retagged 2026-09-23 — was `[committed]`;
   the aspiration exists only in the README, no offline/sync code) — the first
   Labs build milestone must be a demonstrable sync story, or the headline
   collapses.

---

*EduManage · Ansai Technologies · Nairobi, Kenya · edumanage.co.ke*
