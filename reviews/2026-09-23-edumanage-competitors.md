# Review packet — EduManage competitor research (Labs track)

Date: 2026-09-23 | Track: EduManage — competitor differentiation (Labs) | Branch: labs/edumanage-competitor-research

## What was researched

Web research (2026-09-23) on Kenyan school-management systems to ground the
EduManage differentiation rework: Cloud School, Elimikasasa, Citycloud,
Shulevora, Jibu ERP, plus secondary mentions (iOSoft/SIMSCardi, Alif Cloud).
Sources are vendor sites unless noted. No code was changed in this iteration —
research artifacts only.

## Key findings (competitor table)

| Competitor | Offering | Pricing (as advertised) | Notes / gaps |
|---|---|---|---|
| Cloud School (cloudschool.co.ke) | CBC grading + CBC report cards, M-Pesa paybill/till auto-posting, multi-curriculum (CBC, 8-4-4, IGCSE, ACE), modular pricing (pay for modules used), cloud-based, data export | Dated 2020 proposal: Pro KES 25,000/term, Enterprise KES 35,000/term (Standard tier unclear in doc). Current pricing is modular, not public. | Most established Kenyan player; current pricing opaque |
| Elimikasasa (elimikasasa.co.ke) | CBC + 8-4-4 in parallel, M-Pesa (Paybill/Till/STK Push), parent SMS, biometric attendance (ZKTeco F18), payroll (PAYE/NHIF/NSSF/SHIF), library/transport/inventory, report cards | Premium KES 2,500/mo flat; free for schools <100 students; one-term free trial; "Switch & Save": 12 months free + end-to-end migration | Most aggressive switching offer; the market price anchor |
| Citycloud (citycloudschool.co.ke) | Built-in AI assistant, AI document generation, Student Mgmt, Fees & Finance, Exams & Grading, SmartDocs, HRM, Calendar & Tasks, live demo | Free / KES 2,000 / KES 4,500 per month; KES 250,000 one-time lifetime licence | AI-first positioning; lifetime-licence option |
| Shulevora (shulevora.co.ke) | CBC/CBE + 8-4-4, SMS gateway, teacher & parent mobile portals, Excel-import migration, guided rollout | Free up to 75 learners; Basic KES 2,000 + KES 18/learner/month; founding cohort gets 1 term free | Per-learner pricing; modern mobile UX focus |
| Jibu ERP (jibuerp.com) | Mobile app, online exams, LMS integration, vehicle tracking, WhatsApp, biometric | ~KES 50,000 price range (one-time) | ERP-style breadth; less Kenya-specific depth |
| Alif Cloud / iOSoft / SIMSCardi | Generic school-management players | Alif: $1.29/student/month | Background noise; not Kenya-specific leaders |

Table stakes across all of them: CBC + 8-4-4 support, M-Pesa fee collection,
parent SMS/portal, attendance tracking, report cards, cloud access.

## Recommended differentiation angles for EduManage

1. **Offline-capable operations** — the one structural gap in the market: every
   competitor above is cloud-only, while Kenyan school connectivity still costs
   ~$45/month and is unreliable outside towns (UNICEF Giga, 2026). EduManage is
   architected offline-capable — verify this claim in code, then make it the
   headline.
2. **Kenya-native domain model (School DNA + TRANSITION defaults)** —
   competitors bolt CBC onto generic school software; EduManage's School DNA
   config (schoolType / gender / level / category) and default dual-curriculum
   handling match how Kenyan schools actually run in 2026.
3. **Compliance-by-design** — KNEC CBA export readiness, SBA tracking, and
   no-ranking enforcement in CBC mode (a KNEC requirement competitors do not
   advertise). Auditors and boards of management care about this.
4. **Bursar-grade financial rigor** — fee edge cases (overpayment, duplicate,
   partial, credit) plus receipt audit trails as a marketed feature, not an
   afterthought. This is the trust-anchor material.
5. **Agentic operations (later, not now)** — the Baraza/agent infrastructure is
   Ansai's long-term edge; do not pitch it until the core is solid. Citycloud
   already markets an "AI assistant", so this space is contested.

## Risks / unknowns

- Cloud School's current pricing is not public (only a 2020 proposal found) —
  their modular pricing is unknown.
- No hands-on trial of any competitor was done; feature claims are from
  marketing pages and should be treated as such.
- EduManage's offline capability is claimed in the README but NOT verified in
  code — this must be verified before it becomes the headline differentiator.
- EduManage's own pricing strategy is unset; Elimikasasa's KES 2,500/mo flat +
  12-month free switching sets the anchor to beat.
- Switching costs are the real battleground (Elimikasasa does end-to-end
  migration for free) — EduManage needs a migration story, not just a better
  product.

## How to verify

Read this packet; spot-check two or three of the vendor sites linked above;
confirm the competitor table matches what is advertised. No code changed —
this branch contains only research artifacts (`reviews/`).

## Decision requested

Approve the differentiation brief for the EduManage Labs rework track:

(a) Headline = offline-capable + Kenya-native domain model + compliance-by-design.
(b) Commission a hands-on feature-parity audit (trial accounts on Cloud School
    + Elimikasasa) before any rework code is written — yes or no?
