# Review packet template (inspect loop)

Copy for each loop iteration: `reviews/YYYY-MM-DD-<track>.md`.
The packet is committed to the branch AND pasted as the PR body.
Nothing merges without human approval of the packet.

## Sections

1. **Title line** — date, track, branch
2. **What was built / researched** — scope of this loop iteration
3. **Files changed** — list, or "research only — no code changed"
4. **Key findings** — for research packets: competitor/feature table with sources
5. **Recommendations** — what the agent proposes next
6. **Risks / unknowns** — what could be wrong, what is unverified
7. **How to verify** — concrete steps the human can take to check the work
8. **Decision requested** — the explicit approval question(s)

## Rules

- One packet per loop iteration.
- Facts a decision rests on (prices, dates, names) must carry their source.
- Mark anything unverified as unverified — do not present marketing copy as fact.
- The decision requested must be answerable: approve / reject / redirect.

## Merge gate (hard rule — adopted 2026-09-23)
A PR merges only when every risk flagged in this packet is either:
- RESOLVED on the branch, or
- explicitly DEFERRED with a named owner and a next step.
A packet that discloses a risk the branch does not address does not merge.
Disclosing a risk is not the same as handling it.
