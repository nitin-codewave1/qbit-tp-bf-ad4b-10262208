---
id: agent-developer/prooflyt_fe/web-app/INTAKE.md
type: intake
project: 4d1bbbde-de2d-432c-bc57-8da402ac5266
version: 0.1.0
author: acd154e9-7d7c-493d-b538-c1e75f4fcbbe
produces: agent-developer/prooflyt_fe/web-app/INTAKE.md
depends_on: []
commit_kind: append
confidence: agent
run_id: 1ec6e415-88ab-5018-9bdd-aa6651811a58
okf_id: web-app/INTAKE.md
---

<!-- SECTION: web-app.intake | status: VERIFIED -->
## What this run read

| Input | Role(s) | Parsed | Taken from it | How the role was decided |
|---|---|---|---|---|
| `design-brief.md` | design_brief | yes | 5,564 bytes, 1 identifier(s) | declared in INPUTS.yaml |
| `feedback.md` | feedback | yes | 509 bytes, 0 identifier(s) | declared in INPUTS.yaml |
| `requirements.md` | requirements | yes | 7,666 bytes, 8 identifier(s) | declared in INPUTS.yaml |
| `stories.md` | user_stories | yes | 2,646 bytes, 1 identifier(s) | declared in INPUTS.yaml |

## Inputs expected

| Role | Status |
|---|---|
| `requirements` | supplied (1 file(s)) |
| `user_stories` | supplied (1 file(s)) |
| `design_brief` | supplied (1 file(s)) |
| `platform` | not supplied — the run degrades, see GAPS.md |
| `api_docs` | not supplied — the run degrades, see GAPS.md |
| `feedback` | supplied (1 file(s)) |

## Identifiers

- Distinct identifiers found: **1**
- Of those, user stories: **1**
- With established acceptance detail: **1** (100%, floor 60%)
  - counted when a story carries inline criteria, **or** a `§` reference that resolves to a real requirements section
- Requirements sections available to resolve against: **0**

Roles were declared in `INPUTS.yaml`.
<!-- /SECTION: web-app.intake -->
