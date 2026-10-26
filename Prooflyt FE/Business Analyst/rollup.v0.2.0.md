---
id: agent-ba/prooflyt_fe/rollup.md
type: spec
project: 4d1bbbde-de2d-432c-bc57-8da402ac5266
version: 0.2.0
author: acd154e9-7d7c-493d-b538-c1e75f4fcbbe
produces: agent-ba/prooflyt_fe/rollup.md
depends_on: []
commit_kind: fork
confidence: agent
run_id: 1ec6e415-88ab-5018-9bdd-aa6651811a58
---

# Business Analysis — D-COPSCAR

## Discovery

**Brief Quality:** thin (Problem: strong, Outcomes: weak, Stakeholders: weak)

**Declaration:** Thin. The brief defines what to build (the empty state, its content, the reused upload dialog, design tokens, frontend only) but gives no business metric, no named stakeholders, and no evidence of the problem. Assumptions: (1) the goal is first-upload activation; (2) the target audience is new or zero-proof accounts; (3) the seed context lists ba_* variables with no content, so no further source material was supplied. Existing rollup and story files contain only a smoke-test placeholder (US-SMOKE-1), so there are no conflicting stories to reconcile.

## Business Objectives

### OBJ-001: New Prooflyt accounts with no proofs upload their first proof soon after signing up, instead of stalling on the blank proofs list.
- **Leading KPI:** Share of users who open the proofs list with zero proofs and click 'Upload your first proof' (empty-state button click-through rate).
- **Lagging KPI:** Share of new accounts that complete a first proof upload within 7 days of first login.
- **Target:** Proposed, not confirmed: at least 25% of zero-proof sessions click the empty-state button within 30 days of release, and first-upload-within-7-days rises by a measured baseline uplift over 60 days. Baseline and target need product owner sign-off.
- **Impact:** More accounts reach their first successful upload, which is the first step to using Prooflyt's core value.

## EP-001: Proofs list empty state with first-upload call to action (→ OBJ-001)
In the Prooflyt web frontend, replace the blank proofs table with an empty state when the list has no items. It shows an illustration slot, the heading 'No proofs yet', one line of help text, and an 'Upload your first proof' primary button that opens the existing upload dialog. Uses existing design tokens; frontend only, with no backend, API, or upload dialog changes. This drives the leading KPI (empty-state button click-through) and gives zero-proof accounts a direct path to the first upload that the lagging KPI measures.

### US-001-01: As a New Prooflyt account owner with zero proofs, I want to see a 'No proofs yet' empty state with one line of help text instead of a blank proofs table, so that I know the list is empty by design and what to do next, so more zero-proof accounts reach the 'Upload your first proof' button (empty-state click-through KPI)
**Priority:** Must Have

**Acceptance Criteria:**
- Given the proofs list has no items, when the user opens the proofs list, then the heading 'No proofs yet' and one line of help text are shown in place of the table
- Given the proofs list has one or more items, when the user opens the proofs list, then the proofs table is shown and the empty state is not rendered
- Given the empty state is displayed, when it renders, then its heading, help text and button use existing design tokens with no new styles

**Test Cases:**
- **TC-001-01**: the user opens the proofs list
- **TC-001-02**: [edge] the user opens the proofs list
- **TC-001-03**: it renders

### US-001-02: As a New Prooflyt account owner with zero proofs, I want to click the 'Upload your first proof' primary button to open the existing upload dialog, so that I can start my first upload immediately from the empty state, which turns the empty-state click-through into a first upload (lagging KPI)
**Priority:** Must Have

**Acceptance Criteria:**
- Given the empty state is shown on the proofs list, when the user clicks 'Upload your first proof', then the existing upload dialog opens unchanged
- Given the upload dialog was opened from the empty state, when the user closes it without uploading, then the empty state remains displayed
- Given the empty state is shown, when the user views the button, then it is styled as the primary button using existing design tokens

**Test Cases:**
- **TC-001-04**: the user clicks 'Upload your first proof'
- **TC-001-05**: [edge] the user closes it without uploading
- **TC-001-06**: the user views the button

### US-001-03: As a Prooflyt product designer, I want to have an illustration slot in the proofs empty state, so that artwork can be added later without changing the empty-state layout, keeping the call to action visible for the click-through KPI
**Priority:** Should Have

**Acceptance Criteria:**
- Given the proofs list has no items, when the empty state renders, then an illustration slot appears above the heading 'No proofs yet'
- Given no illustration asset is available, when the empty state renders, then the illustration slot is still present and the heading, help text and button still display

**Test Cases:**
- **TC-001-07**: the empty state renders
- **TC-001-08**: [edge] the empty state renders

### US-001-04: As a Existing Prooflyt user with proofs, I want to open the proofs list and see my proofs in the table as before, so that the empty-state change does not hide or alter my existing proofs, so my workflow is unaffected
**Priority:** Should Have

**Acceptance Criteria:**
- Given the proofs list has one or more items, when the user opens the proofs list, then all proofs display in the table unchanged
- Given the proofs list has one or more items, when the user opens the proofs list, then neither the 'No proofs yet' heading nor the 'Upload your first proof' button appears

**Test Cases:**
- **TC-001-09**: the user opens the proofs list
- **TC-001-10**: [edge] the user opens the proofs list

## Business Rules

### BR-001: The empty state is shown only when the proofs list has zero items; when one or more proofs exist, the table renders as before.
**Rationale:** Existing users with proofs must not have their list hidden or altered (US-001-04). | **Enforcement:** Frontend conditional render in the proofs list component based on the item count already loaded.

### BR-002: The empty state contains exactly four elements: an illustration slot, the heading 'No proofs yet', one line of help text, and the primary button 'Upload your first proof'.
**Rationale:** The CR specifies this content; additional elements would dilute the call to action (US-001-01, US-001-03). | **Enforcement:** Frontend component markup and UI review against the CR.

### BR-003: The 'Upload your first proof' button opens the existing upload dialog without modifying its behaviour.
**Rationale:** The CR scopes out new upload dialog behaviour; the button is an entry point only (US-001-02). | **Enforcement:** Frontend button handler invokes the existing dialog open action; no changes to dialog component logic.

### BR-004: The empty state uses existing design tokens for colour, typography, and spacing; no new tokens are introduced.
**Rationale:** The CR requires existing design tokens for visual consistency. | **Enforcement:** Code review and linting for hard-coded style values in the empty-state component.

### BR-005: The change is frontend only: no backend, API, or data-model changes are made, and the empty state is derived from the existing proofs list response.
**Rationale:** The CR explicitly excludes backend or API changes. | **Enforcement:** Change review confirms no diffs in backend services, API contracts, or schemas.

## Non-Functional Requirements

### NFR-001: The empty state must render without any additional network requests beyond the existing proofs list request.
**Category:** Performance | **Target:** 0 additional HTTP requests attributable to the empty state | **Priority:** Must Have

### NFR-002: The empty state must appear once the proofs list response is received, without added render delay.
**Category:** Performance | **Target:** Empty state visible within 100 ms of list data resolving, measured on a reference device | **Priority:** Should Have

### NFR-003: The 'Upload your first proof' button must be reachable and operable by keyboard and expose an accessible name.
**Category:** Accessibility | **Target:** 100% of empty-state actions reachable via Tab and activated via Enter/Space; 0 critical axe-core violations on the empty state | **Priority:** Must Have

### NFR-004: Empty-state text must meet WCAG 2.1 AA contrast against its background.
**Category:** Accessibility | **Target:** Contrast ratio ≥ 4.5:1 for body text and ≥ 3:1 for the heading | **Priority:** Must Have

### NFR-005: The change must not add new endpoints, expose new data fields, or change authentication or authorisation handling.
**Category:** Security | **Target:** 0 new API routes; 0 new data fields in responses; security review sign-off on the diff | **Priority:** Must Have

### NFR-006: The empty-state check must add no meaningful cost to list rendering for large proof sets.
**Category:** Scalability | **Target:** Empty-state check is O(1) on the item count; no extra list iteration beyond the existing render path | **Priority:** Should Have

### NFR-007: The empty-state layout must remain intact on common viewport widths and not require scrolling to reach the primary button.
**Category:** Usability | **Target:** Primary button fully visible without scrolling at 1280×720 and 375×667 viewports | **Priority:** Should Have
