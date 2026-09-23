# Review packet — EduManage differentiation brief (Labs track)

Date: 2026-09-23 | Track: EduManage — Labs rework | Branch: labs/edumanage-differentiation-brief

## What was built / researched

Round 2 of the EduManage inspect loop, executing the decision already approved
in round 1 (merged as edumanage#1): synthesize the competitor research into a
differentiation brief.

Deliverable: `docs/differentiation-brief.md` — the positioning and
differentiation document for the EduManage Labs rework track. It converts the
round-1 competitor findings into: a positioning statement, three headline
differentiators (offline-capable operations, Kenya-native domain model /
School DNA, compliance-by-design), secondary differentiators (bursar-grade
financial rigor, tenant isolation, RBAC + audit), an explicit what-NOT-to-lead-with
list (agentic/AI, price, feature breadth), a migration/switching story, a
one-paragraph sales version, and open questions for the Labs track.

**Deliberate honesty framing:** every claim is tagged `[committed]` (architectural
commitment in the constitution/docs, must be proven in the Labs build before any
customer copy uses it) or `[roadmap]` (not yet built). No code has shipped in
this repo yet — apps/ are stubs — so the brief claims no shipped features.

No code was changed in this iteration.

## Files changed

- `docs/differentiation-brief.md` — new (the brief)
- `reviews/2026-09-23-edumanage-differentiation-brief.md` — this packet

## Key findings

1. **Offline is the cleanest differentiator in the market.** Every competitor
   surveyed (Cloud School, Elimikasasa, Citycloud, Shulevora, Jibu ERP)
   advertises no offline capability. Kenyan school connectivity is ~$45/month
   and unreliable outside towns (UNICEF Giga, 2026, per round-1 research).
2. **Elimikasasa is the market anchor, not Cloud School.** KES 2,500/mo flat,
   free under 100 students, one-term trial, "Switch & Save" (12 months free +
   end-to-end migration). EduManage cannot and should not win a price war
   against this anchor.
3. **Citycloud already contests the AI space** ("AI assistant", "AI document
   generation") — so leading with agentic operations would invite a comparison
   EduManage currently loses. The Baraza/agent layer is the second act, not
   the pitch.
4. **The battleground is switching, not features.** Elimikasasa's free
   end-to-end migration is the offer to beat. The brief therefore specifies a
   migration story: Excel import (table stakes), M-Pesa history import
   (nobody advertises this — ours to take), parallel-run onboarding with
   reconciliation reports, and a CBC data migration path.
5. **Offline capability is `[committed]` but unbuilt** — verified in-repo:
   the README claims "offline-capable", but no offline-related code exists
   (apps/api and apps/web are empty stubs). The brief explicitly gates
   customer-facing offline claims on a demonstrable Labs build milestone.

## Recommendations

1. Approve the differentiation brief as the positioning source for the
   EduManage Labs rework — PRD authors and agents must write against it.
2. First Labs build milestone = demonstrable offline/sync story (the headline
   collapses without it).
3. Commission hands-on trial accounts (Cloud School + Elimikasasa) before any
   head-to-head sales sheet is written — vendor marketing pages only tell you
   what vendors want you to know (round-1 risk, still open).

## Risks / unknowns

- The offline headline is the strongest lever and the most exposed: if the
  Labs build can't demonstrate sync behavior, the headline is vapor. Tagged
  `[committed]` and gated accordingly in the brief.
- Cloud School's current pricing is still opaque (modular, unpublished) —
  a hands-on trial is needed to map it.
- EduManage's own pricing strategy is unset; the brief deliberately proposes
  no number, only that it must not race Elimikasasa's anchor to zero.
- Competitor feature claims rest on marketing pages (round-1 caveat, unchanged).

## How to verify

1. Read `docs/differentiation-brief.md` on this branch.
2. Spot-check the competitor claims against the round-1 packet
   (`reviews/2026-09-23-edumanage-competitors.md`) — every claim in the brief
   should trace back to a row in that table.
3. Confirm the `[committed]` / `[roadmap]` tagging feels honest — if any claim
   reads like a shipped feature, flag it.

## Decision requested

Approve the differentiation brief (`docs/differentiation-brief.md`) as the
positioning source for the EduManage Labs rework:

(a) approve as-is,
(b) approve with edits (list them),
(c) redirect (tell the track to redo differently).
