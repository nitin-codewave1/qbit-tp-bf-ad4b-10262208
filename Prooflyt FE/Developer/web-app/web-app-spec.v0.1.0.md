---
id: agent-developer/prooflyt_fe/web-app/WEB-APP-SPEC.md
type: spec
project: 4d1bbbde-de2d-432c-bc57-8da402ac5266
version: 0.1.0
author: acd154e9-7d7c-493d-b538-c1e75f4fcbbe
produces: agent-developer/prooflyt_fe/web-app/WEB-APP-SPEC.md
depends_on: [US-001-01, US-001-02, US-001-03, US-001-04]
commit_kind: append
confidence: agent
run_id: 1ec6e415-88ab-5018-9bdd-aa6651811a58
okf_id: web-app/WEB-APP-SPEC.md
---

<!-- SECTION: web-app.overview | status: VERIFIED -->
## Overview

**Product:** Prooflyt, web application. **Change request:** CR-108, epic EP-001. **Run mode:** bootstrap, one surface (`web-app`).

**Purpose.** Replace the blank proofs table shown to an account with zero proofs with an empty state. The empty state shows an illustration slot, the heading "No proofs yet", one line of help text, and the primary button "Upload your first proof". The button opens the existing upload dialog unchanged. [BR-001, BR-002, BR-003, US-001-01, US-001-02, US-001-03]

**Primary actors (signed-in users of this surface):**
- New Prooflyt account owner with zero proofs. This is the primary target. [US-001-01, US-001-02]
- Existing Prooflyt user with one or more proofs. Must see no change. [US-001-04]

**Non-actor:** Prooflyt product designer. Named in US-001-03 as the beneficiary of the illustration slot. The designer does not sign in to this surface for the purposes of these stories.

**Design input:** Design brief present; Figma MCP not connected. `spec_mode` for this surface is `FULL-FROM-BRIEF` (core 4.5). The brief supplies 4 stories, 0 screens, 0 components and 71 token IDs with no values. Visual definitions are therefore derived from behaviour and the requirements, not from frames. [design-brief.md]

**Explicitly out of scope:**
- Any backend, API or data-model change. No new endpoints, no new response fields, no change to authentication or authorisation. [BR-005, NFR-005]
- Any change to upload dialog behaviour. The button is an entry point only. [BR-003]
- Any new design token. [BR-004]
- Artwork for the illustration. The slot is specified; the asset is not. [US-001-03]
- Admin surface and any other surface.

**Feedback artefacts.** The change request lists `spec` and `api_contract` as outputs. This run produces the specification set only and writes no contract. No new endpoint is introduced [NFR-005], so the existing proofs-list response is the only data input [BR-005]. That response is not supplied (`contract_source: none`). See `web-app.routing` and `web-app.coverage` for the gaps this leaves. [feedback.md, RUN-CONTEXT]

**Contract posture.** `contract_source: none`. No API-bound section can be completed. Every API-bound element is `BLOCKED` and no endpoint, path, shape or error set is assumed. This run does not halt for it (core 10.1). [RUN-CONTEXT]
<!-- /SECTION: web-app.overview -->
<!-- SECTION: web-app.routing | status: DRAFT-UNVERIFIED -->
## Routing

| Route | Page | Layout | Required permission |
|---|---|---|---|
| Proofs list route (path not supplied, GAP-WEB-002) | Proofs list page, containing the empty state or the proofs table | GAP-WEB-003 | GAP-WEB-003 |

- The proofs list is a web route owned by this surface. [ASM-WEB-001]
- The empty state is not a route. It is a conditional render inside the proofs list. [BR-001]
- **Protected-route rules:** not supplied. [GAP-WEB-003]
- **Unauthenticated redirect:** not supplied. [GAP-WEB-003]
- The change adds no route and changes no authentication handling. [NFR-005]

**Gaps:**
- GAP-WEB-002: the path of the proofs list route is not supplied.
- GAP-WEB-003: layout nesting, protected-route rules and unauthenticated redirect are not supplied.

**Assumption:**
- ASM-WEB-001: the proofs list is a web-app route rendered for a signed-in user. This is inferred from the stories, not stated.
<!-- /SECTION: web-app.routing -->
<!-- SECTION: web-app.module-map | status: VERIFIED -->
## Module map

| Feature area | Route owner | Change in this run |
|---|---|---|
| Proofs list | Proofs list route (GAP-WEB-002) | Adds the empty-state branch when item count is zero. [BR-001] |
| Upload dialog | Existing, not in this change | None. The button only invokes its open action. [BR-003] |

- Module-level specs are not produced by this run. The proofs list is the single affected module. The module name `proofs` is a candidate for later module-level specs.
- The upload dialog is out of this change's module scope.
<!-- /SECTION: web-app.module-map -->
<!-- SECTION: web-app.state-management | status: DRAFT-UNVERIFIED -->
## State management

**Server state.** The proofs list is derived from the existing proofs-list response. The empty state requires no new server request. [BR-005, NFR-001]

**Client state.**
- The empty-state branch is determined by the item count already loaded for the list. No second source of truth. [BR-001]
- Evaluating the count is O(1) against the item count and adds no list iteration beyond the existing render path. [NFR-006]

**Transitions:**
- Zero items: empty state shown, table hidden. [BR-001, US-001-01]
- One or more items: table shown, empty state and "Upload your first proof" button not rendered. [BR-001, US-001-04]
- Closing the upload dialog without uploading leaves the empty state displayed. [US-001-02]

**Cache and invalidation.** Not specified. After a first upload completes, the list must move from the empty state to the table. How the list is refreshed (refetch, cache update, or none) is not specified. [GAP-WEB-004]

**Gap:**
- GAP-WEB-004: the cache and invalidation policy for the proofs list, and specifically what happens after the first upload completes from the empty state, is not supplied.
<!-- /SECTION: web-app.state-management -->
<!-- SECTION: web-app.auth-flows | status: DRAFT-UNVERIFIED -->
## Auth flows

- The change adds no authentication handling. Login, refresh, session expiry and logout are unchanged. [NFR-005]
- The empty state is shown only to an authenticated account. This is inferred from the stated actors. [ASM-WEB-001]

**Not supplied:**
- Login, token refresh, session-expiry and logout behaviour. [GAP-WEB-005]
- Mid-flow expiry, for example a session expiring while the upload dialog is open from the empty state. [GAP-WEB-005]

**Gap:**
- GAP-WEB-005: the auth flows for this surface are not supplied. Specified only as unchanged.
<!-- /SECTION: web-app.auth-flows -->
<!-- SECTION: web-app.authorization-ui | status: DRAFT-UNVERIFIED -->
## Authorization UI

**Roles in scope for this surface:**

| Role | Visible navigation | Empty state | Enabled action |
|---|---|---|---|
| New account owner (zero proofs) | Proofs list | Shown | "Upload your first proof" enabled, opens upload dialog [BR-003] |
| Existing user (one or more proofs) | Proofs list | Not shown | Table actions unchanged [US-001-04] |

- The two rows are the same signed-in role, distinguished by item count. [ASM-WEB-002]
- **Enabled-action rule for the upload button:** no permission matrix is supplied. Whether the upload action is permission-gated is unknown. [GAP-WEB-006]

**Roles excluded:**
- Prooflyt product designer: not a signed-in actor of this surface in the supplied stories. [US-001-03]
- Any operator or administrative role: belongs to the admin surface. The backend role matrix is not supplied, so no other roles are speculated about. [I-1]

**Gap:**
- GAP-WEB-006: no permission matrix is supplied for the upload action.
<!-- /SECTION: web-app.authorization-ui -->
<!-- SECTION: web-app.design-system | status: BLOCKED -->
## Design system

**Reason:** The design brief supplies 71 token IDs with paths but no token values. The type scale, spacing scale and breakpoints are not supplied. Specifying colour, typography or spacing values would be invention. [design-brief.md, BR-004, GAP-WEB-007]

**Unblocks with:**
- Token values for the IDs in the brief's tokens index, or a Figma connection that resolves them.
- The type scale and spacing scale.

**Constraint that holds regardless:** the empty state uses only existing tokens. No new token is introduced. [BR-004, US-001-01]

**Gap:**
- GAP-WEB-007: token values, type scale and spacing scale are not supplied.
<!-- /SECTION: web-app.design-system -->
<!-- SECTION: web-app.responsive | status: DRAFT-UNVERIFIED -->
## Responsive

**Cited viewport targets:**
- Primary button fully visible without scrolling at 1280×720 and 375×667. [NFR-007]
- The empty-state layout remains intact at common viewport widths. [NFR-007]

**Not supplied:**
- Breakpoint values. [GAP-WEB-008]
- The layout change at each breakpoint. [GAP-WEB-008]

**Gap:**
- GAP-WEB-008: breakpoints and their layout changes are not supplied. Only the two viewport targets above are cited.
<!-- /SECTION: web-app.responsive -->
<!-- SECTION: web-app.browser-support | status: BLOCKED -->
## Browser support

**Reason:** No supported browsers or versions are supplied in any input. Browser support is not assumed. [GAP-WEB-009]

**Unblocks with:** the supported browser and version list from the product owner or a platform input.

**Gap:**
- GAP-WEB-009: supported browsers and versions are not supplied.
<!-- /SECTION: web-app.browser-support -->
<!-- SECTION: web-app.accessibility | status: DRAFT-UNVERIFIED -->
## Accessibility

**Target standard:** WCAG 2.1 AA. [NFR-004]

**Cited requirements, scoped to the empty state:**
- The "Upload your first proof" button is reachable by Tab and activated by Enter or Space. [NFR-003, US-001-02]
- The button exposes an accessible name. [NFR-003]
- Contrast: at least 4.5:1 for body text and at least 3:1 for the heading. [NFR-004]
- Zero critical axe-core violations on the empty state. [NFR-003]

**Verification:** the cited targets are verified by Tab and Enter/Space operation checks and an axe-core run scoped to the empty state. [NFR-003]

**Not supplied:**
- Focus return to the button after the upload dialog closes without uploading. [GAP-WEB-010]
- Heading level for "No proofs yet". [GAP-WEB-010]
- Whether WCAG 2.1 AA applies to the whole application or only the empty state. [GAP-WEB-010]

**Gap:**
- GAP-WEB-010: focus management, heading level and the scope of the WCAG target beyond the empty state are not supplied.
<!-- /SECTION: web-app.accessibility -->
<!-- SECTION: web-app.performance | status: DRAFT-UNVERIFIED -->
## Performance

**Cited targets:**
- Zero additional HTTP requests attributable to the empty state. [NFR-001]
- Empty state visible within 100 ms of list data resolving, on a reference device. [NFR-002]
- Empty-state check is O(1) on item count. [NFR-006]

**Gap:** the reference device for the 100 ms target is not defined. [GAP-WEB-011]

**Not supplied:**
- Bundle budget. [GAP-WEB-012]
- Route-level code splitting. [GAP-WEB-012]
- The largest-payload route. [GAP-WEB-012]

**Gaps:**
- GAP-WEB-011: reference device not defined.
- GAP-WEB-012: bundle budget, code-splitting policy and largest-payload route not supplied.
<!-- /SECTION: web-app.performance -->
<!-- SECTION: web-app.coverage | status: DRAFT-UNVERIFIED -->
## Coverage

**Story → requirement coverage:**

| Story | Covering requirements | Status | Notes |
|---|---|---|---|
| US-001-01 | BR-001, BR-002, BR-004 | Covered | Heading and help text are specified by BR-002. Help-text copy is not supplied (GAP-WEB-001). |
| US-001-02 | BR-003, BR-004, NFR-003 | Partial | Closing the dialog without uploading leaves the empty state displayed. No BR states this directly. Covered indirectly through BR-001 (zero items, empty state shown). Focus return is GAP-WEB-010. |
| US-001-03 | BR-002 | Partial | The slot is one of four elements. Behaviour when no illustration asset exists is not a requirement. [GAP-WEB-013] |
| US-001-04 | BR-001, BR-005 | Covered | Non-empty list shows no heading and no button, per BR-001. |

**Uncovered elements:**
- GAP-WEB-001: the help-text copy is not supplied. BR-002 specifies one line of help text without its content.
- GAP-WEB-013: the illustration slot with no asset (US-001-03, second Given) is not specified as a requirement.

**Contradiction check (four directions):**
- Story ↔ design: no contradiction. The brief has no screens to contradict the stories.
- Story ↔ requirement: no contradiction found.
- Requirement ↔ requirement: no contradiction found.
- Design ↔ design: no contradiction found.

**Gaps:**
- GAP-WEB-001: help-text copy not supplied.
- GAP-WEB-013: no-asset state of the illustration slot not specified.

**Assumptions:**
- ASM-WEB-001 and ASM-WEB-002 (see above).

**Consequence for the feedback artefacts:** no `api_contract` is produced by this run. [feedback.md, BR-005]
<!-- /SECTION: web-app.coverage -->
