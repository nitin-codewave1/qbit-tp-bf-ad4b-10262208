---
id: agent-ba/prooflyt_fe/discovery/discovery.md
type: discovery
project: 4d1bbbde-de2d-432c-bc57-8da402ac5266
version: 0.1.0
author: acd154e9-7d7c-493d-b538-c1e75f4fcbbe
produces: agent-ba/prooflyt_fe/discovery/discovery.md
depends_on: []
commit_kind: append
confidence: agent
run_id: 1ec6e415-88ab-5018-9bdd-aa6651811a58
okf_id: DISCOVERY
---

---
id: DISCOVERY
type: discovery
status: active
created_at: 2026-10-26T17:52:48.104800+00:00
rig: ba
---

# Discovery

**Brief quality:** thin (problem: strong, outcomes: weak, stakeholders: weak)

**Declaration:** Thin. The brief defines what to build (the empty state, its content, the reused upload dialog, design tokens, frontend only) but gives no business metric, no named stakeholders, and no evidence of the problem. Assumptions: (1) the goal is first-upload activation; (2) the target audience is new or zero-proof accounts; (3) the seed context lists ba_* variables with no content, so no further source material was supplied. Existing rollup and story files contain only a smoke-test placeholder (US-SMOKE-1), so there are no conflicting stories to reconcile.

## Problem
When the Prooflyt web proofs list has no items, it shows a blank table, so users get no guidance on what to do next.

**Root cause:** A blank table gives no signal that the list is empty or that uploading is the next step. The upload action is hidden until a user already knows where to find it, which likely slows first use. The brief does not confirm this from usage data.

**Boundary:** Most affected: new or first-time users and accounts with zero proofs. Least affected: established users with proofs, who never see the empty state.

**Prior attempts:** None stated. The existing upload dialog is reused, so no new upload flow is being built.

## Outcome
**Before:** An account with no proofs sees a blank proofs table with no guidance or upload prompt.

**After:** An account with no proofs sees an empty state with an illustration slot, the heading 'No proofs yet', one line of help text, and an 'Upload your first proof' button that opens the existing upload dialog.

**Measurement:** Assumed: share of accounts that upload a first proof within 7 days of first login. The brief names no metric, so this is a proposed baseline to confirm with the product owner.

**Impact index:** More new accounts take their first upload action from the proofs list.

## Stakeholders
**Decision maker:** Not named in the brief. Assumed to be the Prooflyt product owner, whose success means activation improves with no backend or API change.

**Champion:** Not named in the brief. Assumed to be whoever raised change request CR-108.

**End user:** Assumed: a new user who has just signed in to the Prooflyt web app for the first time and opens the proofs page. They have no proofs yet and may not know the upload dialog exists. The brief does not describe their context or alternatives.
