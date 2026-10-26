---
id: agent-developer/prooflyt_fe/web-app/SELF-CHECK.md
type: self-check
project: 4d1bbbde-de2d-432c-bc57-8da402ac5266
version: 0.1.0
author: acd154e9-7d7c-493d-b538-c1e75f4fcbbe
produces: agent-developer/prooflyt_fe/web-app/SELF-CHECK.md
depends_on: []
commit_kind: append
confidence: agent
run_id: 1ec6e415-88ab-5018-9bdd-aa6651811a58
okf_id: web-app/SELF-CHECK.md
---

<!-- SECTION: web-app.self-check | status: VERIFIED -->
## Verification pass

| # | Check | Result | Detail |
|---|---|---|---|
| 1 | anchors open and close; ids unique and well-formed | **PASS** | 12 section(s); all 12 sections present, in order |
| 2 | every referenced id resolves | **PASS** | every id cited carries this run's surface code |
| 3 | every minted id carries this surface's code | **PASS** | 15 minted, all carrying `WEB` |
| 4 | no VERIFIED section contains an uncited claim | **NOT RUN** | a judgement about prose; the document's own verification pass covers it |
| 5 | locked sections reproduced byte-for-byte | **PASS** | the document is written through the locking engine |
| 6 | every story this document answers for appears in the coverage table | **PASS** | 1 in scope, 0 not found in the document |
| 7 | no schema is restated | **NOT RUN** | a judgement about prose, not a pattern this module can assert |
| 8 | no file written outside output_root | **PASS** | every write is jailed to `/tmp/qbit/specialist/1ec6e415-88ab-5018-9bdd-aa6651811a58/002_prooflyt_fe-2-agent-developer_agent-developer/devagent/output/web-app` |
| 9 | every Q- has a class; every GAP- names its closing artefact | **NOT RUN** | 13 GAP- id(s) are defined in the specification's prose; whether each names a closing artefact is the document's own verification pass |
| 10 | no GAP- raised for a condition that cannot occur | **NOT RUN** | a judgement about the condition, not the id |

**6 passed, 0 failed, 4 not run.**

A check marked `NOT RUN` has nothing to check yet at this milestone — no specification sections exist. It is reported as not run rather than as a pass: reporting a pass that was never performed is invariant I-2 broken against ourselves.
<!-- /SECTION: web-app.self-check -->
