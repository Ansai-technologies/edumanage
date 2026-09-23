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

## Changes in this revision — pre-review fixes (2026-09-23)

The founder's pre-review (see `~/workspace/reviews/REVIEW-NOTES.md` §1) found
four honesty issues in the first draft of the brief. All four are fixed in
this revision:

1. **Sales paragraph vs gating rule.** §6's sales paragraph claimed offline as
   shipped ("it keeps working when the network doesn't") in present tense,
   violating §2a's own rule. Fixed: §6 is now explicitly labeled
   **DRAFT COPY — not for use until the sync milestone is demonstrated**, and
   the paragraph is rephrased in future/committed terms throughout.
2. **Honesty tags on §3.** The first draft claimed all claims were tagged but
   §3 (secondary differentiators) carried no tags and read as marketed
   features. Fixed: every §3 item is now tagged — bursar-grade financial
   rigor `[roadmap]`, tenant isolation `[committed]`, RBAC + audit
   `[committed]` — and the "as marketed features" language is reworded to
   "first-class design concerns".
3. **Constitution attribution.** The first draft attributed the offline quote
   ("If EduManage went offline for a week…") to the constitution; the line
   exists **only in README.md** (zero hits in AGENTS.md/CONTEXT.md, verified
   via API). Fixed: §2a now attributes it to the README, the differentiator
   is retagged `[roadmap]` (the commitment is currently README-aspiration
   only — zero offline/sync code in the repo), with an explicit promotion
   path: it returns to `[committed]` when a real offline/sync commitment lands
   in AGENTS.md/CONTEXT.md or the Labs sync milestone is demonstrated.
   README's own "offline-capable" line is annotated with the same caveat so
   the repo's front door no longer contradicts the brief.
4. **"22-role RBAC" count.** Unverified anywhere — the constitution names the
   `@ansai/roles` package only. Fixed: the brief now says "Role-based access +
   full audit log" with an inline caveat that the specific count stays out of
   customer copy until confirmed.

Consistency pass: the positioning statement's "offline-capable" now carries
the `[roadmap]` tag, and §7 open question 3 reflects the retag.

## Files changed

- `docs/differentiation-brief.md` — new (the brief), revised per the four
  fixes above
- `README.md` — offline-capable claim annotated with the Labs-milestone caveat
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
5. **Offline capability is `[roadmap]`, not `[committed]`** — retagged in this
   revision. Verified in-repo: the aspiration exists only in the README; no
   offline-related code exists (apps/api and apps/web are empty stubs). The
   brief gates customer-facing offline claims on a demonstrable Labs build
   milestone, and the README now carries the same caveat.

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
  `[roadmap]` and gated accordingly in the brief; the README caveat stops the
  repo's front door from contradicting it.
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
4. New in this revision: confirm the four pre-review fixes above are accurately
   described (grep the brief for `[roadmap]`/`[committed]` counts; check the
   README caveat renders).

## Traceability re-check (2026-09-23, after the fixes)

The fixes touched only honesty framing — no competitor claim was altered.
Re-verified: every competitor row in the §2a table (Cloud School, Elimikasasa,
Citycloud, Shulevora, Jibu ERP — "none advertised" offline) and every named
claim (Elimikasasa KES 2,500/mo + Switch & Save, Citycloud "AI assistant",
Shulevora Excel-import, Cloud School opaque pricing) still traces to rows in
the round-1 packet `reviews/2026-09-23-edumanage-competitors.md` on main.

## Decision requested

Approve the differentiation brief (`docs/differentiation-brief.md`) as the
positioning source for the EduManage Labs rework:

(a) approve as-is,
(b) approve with edits (list them),
(c) redirect (tell the track to redo differently).
