# Mini Issue Tracker — Figma Design Implementation Brief

**Artifact:** `05_Figma_Brief_v1.0.md`  
**Status:** **WORKING DRAFT — developer elected to proceed to F1 with Control B SKIPPED; NOT independently approved**  
**Review record:** On 2026-11-08 the developer explicitly chose to SKIP independent Control B and proceed to F1. No reviewer, independent acceptance, or approval is claimed. Input Pack v1.0 and Screen Contracts v1.0 remain REVIEW / NOT APPROVED; use their current versions as the implementation basis. Figma Agent **may generate the working wireframes now**. Record skipped review as an acknowledged process deviation, not as a passed quality gate.  
**Source of truth:** S1 `SD_Spec.docx.pdf` (§1, §3, §5, §8); `01_Input_Pack_v1.0.md`; `02_Screen_Map_v1.0.md`; `03_Screen_Contracts_v1.0.md` (§2–§7, §10); `Decision_Log_v0.1.md` (approved D-01–D-09).

## 1. Purpose and scope

Create an **editable, desktop, grayscale, low-fidelity UX/UI wireframe plan** for a small internal team issue tracker. The MVP covers eight source user stories (US-01–US-08): create an issue, view issues and their details, assign one responsible team member, set priority, view progress, comment, update status, and view important not-Closed issues.

The product has two user roles: **Team Member** and **Team Lead**, with **exactly three predefined users in the first release** (two Team Members and one Team Lead). Only authenticated team members can access issue content (BR-01). This design task models that access boundary; it does **not** define or implement an authentication method.

**No new product behavior may be inferred from visual examples.** SOURCE requirements and approved UX choices are different: S1 defines business behavior; D-01–D-09 define the approved presentation and navigation. All interactions shown in Figma are illustrative, not evidence of real persistence or authorization.

## 2. Design constraints and Figma deliverable

- Use **one Figma working page** named `Mini Issue Tracker — Wireframes`; use meaningful names for frames, layers, variants, and components.
- Deliver **editable Figma-native layers**, not flattened pictures; use reusable **local components** for tabs, issue rows, fields, action buttons, disabled states, priority/status values, comments, validation, and error/empty states.
- Use **Auto Layout where appropriate**, grayscale only, low-fidelity spacing and typography, straightforward desktop layout. Focus on hierarchy and required data, not decoration.
- Place design notes, state matrices, T-ID references, role examples, and source annotations **outside product frames** in a clearly named reference area.
- **No page icon placeholders, decorative squares, row-selection controls, or bulk-action controls.** No unapproved auxiliary navigation.
- Use **canonical frames plus compact component/state examples**. Do **not** generate full page duplicates for every role × assignee × status combination.
- At this stage annotate navigation intent using T-ID labels; **do not build prototype interactions**. Do not request export files, backend functionality, real login, conditional logic, or code authorization checks.

## 3. Canonical screens and states — exact IDs

| Exact ID | Kind / frame label | Required visible content and purpose | Notes |
|---|---|---|---|
| **S-01** | Authentication boundary / explanatory placeholder | Noninteractive indication that issues require an authenticated team member | **Not a login page**; no guessed username/password, SSO, or sign-in flow. Demonstration begins from authenticated context on S-02 (D-02). Keep it as a separate reference/annotation if needed, not an invented interactive product form. |
| **S-02** | Issues List — shared screen | Header/title, **All** and **Important** tabs, **Create Issue** action, rows displaying ID, Title, Status, Priority, and Assignee **if assigned** | One shared list, not two separate product pages (D-01). |
| **S-02-A** | All — list state | All registered issues with required row fields | Demonstration starting tab; do not claim S1 mandates the initial tab. |
| **S-02-B** | Important — filtered list state | The same row layout with the precise Important predicate | Include High/Resolved and Critical/Resolved as eligible samples. |
| **S-02-C** | Empty — contextual state within S-02 | No issue rows; neutral visible empty-state indication while retaining tabs and Create Issue | Show compact **Empty All** and **Empty Important** examples. Exact optional copy is not approved and may be represented by a descriptive annotation, not invented mandatory text. |
| **M-01** | Create Issue modal | Only two editable issue inputs: **Title** and **Description**, both required; **Create** and **Cancel** actions; validation indication | Opens over S-02; no priority, assignee, or status input during Create (D-01). |
| **S-03** | Issue Details | **ID, Title, Description, Status, Priority, Author, Created at**, and **Assignee if assigned**; comments list with each comment's body, author, creation date/time; relevant permission-aware controls | A single details screen for read, assignment, priority, status, and comments; reached from a row or after successful Create (D-09). |

**State reference, not additional product pages:** create-validation state; empty comment validation; failed comment save/error-with-no-new-comment; editable versus disabled assignee/priority/status controls; `Not Set` and `Unassigned`; all four status values; and four role/assignee contexts.

## 4. Required labels, values, and data behavior

Use the following functional labels consistently where needed: **All**, **Important**, **Create Issue**, **Title**, **Description**, **Create**, **Cancel**, **ID**, **Status**, **Priority**, **Assignee**, **Author**, **Created at**, **Apply**, **Back to Issues**, and **Add comment**. UI labels are implementation identifiers from the approved contracts, not claims that S1 supplies exact copy for all labels.

- **Create inputs:** only Title and Description are entered by the user; both are mandatory (US-01). After success the issue obtains system-generated **unique ID**, **author**, **created_at**, and **status = Open** (AC-01.4, BR-03). Priority starts **unset**, displayed **Not Set** (BR-04/05, D-03). Initial assignee is **Unassigned** (D-04, an approved UX decision rather than a source default).
- **Priority choices for Team Lead:** **Low**, **Normal**, **High**, **Critical** only. `Not Set` means no value, **not a fifth selectable level**; no Reset action (BR-05/06, D-03).
- **Status values:** exactly **Open**, **In Progress**, **Resolved**, **Closed** (BR-07). Do not conflate Resolved with Closed.
- **Assignee:** zero or one current assignee; when selected, the person must be a team member. Only Team Lead can assign or reassign; show the current assignee on issue details and, when present, on list rows (US-03, D-04).
- **Comments:** body text cannot be empty. A successfully saved comment is shown in S-03 with its **author** and **creation date/time**. A failed save must display an error and **must not create a new comment** (US-06).
- Actual timestamp format/timezone and the exact wording of unspecified empty/error messages are **not defined by S1**. Use neutral annotated examples, not unapproved prescribed copy (pending optional D-10). **Exception:** the source Gherkin explicitly provides **`Title is required`** for an empty Title.
- Use the same issue IDs and values consistently between All, Important, and Details; the Important tab is only a view of the same issue collection.

## 5. Controls and permissions

Show readable values to both roles. Where an action is not permitted, its editing control remains **visible but disabled**, never hidden (D-05). `Apply` belongs **beside each of Assignee, Priority, and Status controls** and commits only that selected field; after successful Apply, **remain on S-03** (D-06).

| Action | Member — not assignee | Member — assignee | Lead — not assignee | Lead — assignee | Control / reference |
|---|---|---|---|---|---|
| View list and details | Yes | Yes | Yes | Yes | S-02/S-03; BR-01, US-02 |
| Create issue | Yes | Yes | Yes | Yes | M-01; BR-02, US-01 |
| Add nonempty comment | Yes | Yes | Yes | Yes | S-03; US-06 |
| Assign / reassign assignee | Disabled | Disabled | Enabled | Enabled | C-11 + local C-17 Apply; US-03, D-04/D-05/D-06 |
| Set / change priority | Disabled | Disabled | Enabled | Enabled | C-12 + local C-17 Apply; BR-06, D-03/D-05/D-06 |
| Change status | Disabled | Enabled **only for permitted transition** | **Disabled** | Enabled **only for permitted transition** | C-13 + local C-17 Apply; BR-08/08.1, AC-07.4, D-05/D-06 |

**Important:** Team Lead's global role **never overrides** the current-assignee requirement for status. If assignee is Unassigned, nobody can change status. If status is Closed, nobody can move status, including its assignee. These are **status-specific** restrictions and must not implicitly disable comments or Lead priority edits on Closed issues.

Include one compact visual reference for **all four contexts** (Member/non-assignee, Member/assignee, Lead/non-assignee, Lead/assignee), with enabled/disabled examples. Do not build four full duplicate S-03 screens.

## 6. Allowed status transitions

For the **current assignee only**, enable exactly these status changes (BR-08/08.1):

| Current status | Allowed next status |
|---|---|
| **Open** | **In Progress** |
| **In Progress** | **Resolved** |
| **Resolved** | **Closed** or **In Progress** |
| **Closed** | **None** |

All other transitions are forbidden, including `Open → Closed`, `In Progress → Closed`, `Resolved → Open`, and **every transition out of Closed**. The same-state label is display, not a new transition. Show a compact status-reference block with **all four statuses**, allowed-next choices and disabled Closed state. Note denied changes without depicting a successful result (G3 §3–§4; T-14–T-19).

## 7. Important predicate — exact inclusion rule

**Important = (Priority is High OR Critical) AND (Status is NOT Closed)** (BR-09/09.1, US-08).

| Example | Important? | Reason |
|---|---|---|
| High + Open | Yes | High, not Closed |
| Critical + In Progress | Yes | Critical, not Closed |
| **High + Resolved** | **Yes** | Resolved is not Closed |
| **Critical + Resolved** | **Yes** | Resolved is not Closed |
| Critical + Closed | No | Closed excludes regardless of priority |
| High + Closed | No | Closed excludes regardless of priority |
| Low / Normal + any status | No | Not High/Critical |
| Not Set + Open | No | Priority is unset |

Preserve the Important filter when returning to the tab. If an issue becomes Closed while its Details was opened from Important, **it is no longer listed** after returning (D-07). Never create a separate Important repository or contradictory duplicate issue data.

## 8. Required empty, validation, disabled, and error examples

Include these **compact states or component examples**, not additional full product pages:

1. **S-02-C / Empty All:** no registered issues. Keep All/Important tabs and Create Issue available; empty is not an error.
2. **S-02-C / Empty Important:** issues may exist in All, but no issue matches Important predicate.
3. **M-01 / Required Title:** click Create with Title empty → do not create an issue; display source-backed **`Title is required`**.
4. **M-01 / Required Description:** click Create with Description empty → do not create an issue; show a required-field validation indication without inventing a source-mandated error string.
5. **S-03 / Empty comment:** submitting empty text adds no comment; show a neutral validation indication.
6. **S-03 / Failed comment save:** display a visible generic error indication and **zero new comments**. Do not show a fake successful comment, author or timestamp.
7. **S-03 / Permission-disabled controls:** Member cannot edit Assignee/Priority; **Lead/non-assignee cannot edit Status**; Closed has no allowed status transition.
8. **S-03 / Unassigned and Not Set:** visually distinct absence states, without a fabricated person or a fifth priority choice.

Optional aesthetic wording for neutral placeholders is **not a new product requirement**. Exact non-source copy requires separate approval if promoted from annotations to binding requirements (D-10 not approved).

## 9. Navigation intent — annotations only

Annotate the following T-ID connections **outside product frames**. At this stage these are specifications for subsequent manual prototype linking, **not interactive prototype wiring**:

| T-ID | Intent |
|---|---|
| **T-01** | Authenticated demonstration context → S-02-A; no login implementation (D-02). |
| **T-02/T-03** | Switch **All ↔ Important** within S-02; show contextual empty state when necessary. |
| **T-04/T-05** | Click an issue row in All/Important → S-03 of that **same issue**. |
| **T-06/T-07** | Click Create Issue in either tab → M-01; preserve originating-tab context. |
| **T-08** | Cancel M-01 → originating list tab, without creating an issue. |
| **T-09** | On **successful** Create with valid required fields → S-03 of the **newly created issue** (D-09). Validation/save failure does not take this route. |
| **T-10/T-11** | Lead can assign/reassign one team member via local Apply; Member cannot. Stay S-03. |
| **T-12/T-13** | Lead can set priority via local Apply; Member cannot. Stay S-03. |
| **T-14–T-17** | Current assignee selects one of four legal status transitions and presses local Apply; stay S-03. |
| **T-18/T-19** | Non-assignee or illegal status transition → **no change and no successful route**. |
| **T-20/T-21** | Successful comment → shown with author/time; failed save → error, no new comment; stay S-03. |
| **T-22/T-23** | Back from S-03 to the originating All/Important tab; apply the current filter (D-07). If S-03 was reached after Create, retain the tab from which M-01 was opened. |
| **T-24/T-25** | Contextual Empty All / Empty Important within S-02, not separate new screens. |

## 10. Sample demonstration data — fictional only

Use fictional, fixed records and deterministic *illustrative* results (D-08). Do not claim these represent an actual database. Use exactly **three simulated predefined identities**: **Member A** and **Member B** (Team Members), **Lead C** (Team Lead).

| Issue ID | Title (illustrative) | Priority | Status | Assignee | Author (illustrative) |
|---|---|---|---|---|---|
| ISS-001 | Login fails after update | Critical | Open | Member A | Member B |
| ISS-002 | Dashboard data is stale | High | In Progress | Member B | Member A |
| ISS-003 | Search results mismatch | High | Resolved | Member A | Lead C |
| ISS-004 | Notification delivery failed | Critical | Closed | Member B | Member A |
| ISS-005 | Layout breaks at desktop width | Not Set | Open | Unassigned | Lead C |
| ISS-006 | Service restarts unexpectedly | Critical | Resolved | Member B | Member A |

Use a short fictional Description and Created at on S-03, and sample comments with author/time in a successful-comment example. In the **Important** tab show **ISS-001, ISS-002, ISS-003, ISS-006** only. Keep ISS-004 out (Closed) and ISS-005 out (Not Set).

Show a compact illustrative state sequence, without implementing data mutation: a current assignee of ISS-002 sees `In Progress`, selects `Resolved`, presses Status Apply, and sees `Resolved` on S-03. A Lead who is **not** the assignee sees the Status editor disabled. Use fixed visual variants to convey the result rather than asking Figma to implement conditional rules.

## 11. Exclusions — list once

Do **not** create attachments/upload controls, AI categorization, AI priority suggestions, issue deletion, separate change-history UI, external integrations, client/customer portal, billing, time tracking, CI/CD, full project management, mobile app, separate priority/assignment/comments management pages, real sign-in/SSO/password pages, separate settings screens, decorative placeholders, row selection, bulk operations, or product-facing controls for response-time measurement, HTTPS, or backups.

No backend/API/database architecture, upload/export workflow, working authentication, real persistence, executable authorization, or dynamic filtering is requested from the design agent. System constraints remain out of scope for static UI evidence.

## 12. Acceptance checklist — review the generated wireframes against the contract

- [ ] One Figma working page, clean grayscale low-fi, editable native layers, meaningful names, reusable local components, suitable Auto Layout.
- [ ] Canonical IDs present and correctly classified: S-01 boundary, S-02 with S-02-A/B/C states, M-01 modal, S-03 details. No duplicate product screens for each role/status.
- [ ] S-02 rows show minimum ID, Title, Status, Priority, and Assignee when assigned; S-03 shows all eight required issue fields plus comments with body/author/time.
- [ ] M-01 has **only** Title and Description issue inputs, both required; no priority/status/assignee selector. Create initializes Open, unset priority, Unassigned (D-04), and reaches new-issue S-03 only after success (D-09).
- [ ] Priority offers only Low/Normal/High/Critical, with Not Set rendered as absence and no reset control.
- [ ] All four role/assignee contexts represented in compact state reference; Member assignment/priority disabled; **Lead/non-assignee status disabled**.
- [ ] Exactly four allowed status transitions; Closed has no outgoing status action, with no accidental ban on unrelated comments or Lead priority changes.
- [ ] Important includes **High/Resolved** and **Critical/Resolved**, excludes all Closed, Low, Normal, and Not Set; one shared list model.
- [ ] Empty All, Empty Important, required Title/Description, empty comment, failed-save/no-comment, disabled, Not Set/Unassigned example states present.
- [ ] Cancel creates nothing; comment save failure creates nothing; successful comments show text, author, date/time.
- [ ] T-01–T-25 navigation intent is described **only with external annotations**; return retains originating tab and reapplies predicate.
- [ ] Fictional data is consistent across rows/details and demonstrates positive/negative Important cases; no dynamic logic is claimed.
- [ ] Notes and state references are outside product frames; no page icon placeholders, decorative squares, row selections, bulk controls, or extra functionality.
- [ ] No Figma prototype wiring, export, backend implementation, authentication coding, or claims of server-side tests.
- [ ] **Review-status transparency:** Control B was **SKIPPED by explicit developer choice on 2026-11-08**; this is not independent acceptance. The wireframes are a working F1 draft based on REVIEW contracts, and must not be labeled fully approved or independently verified.

**Source identifiers:** S1 BR-01–BR-11, BR-08.1, BR-09.1; US-01–US-08 and their 33 AC. **Approved UX decisions:** D-01–D-09. **Unapproved optional UX copy details:** proposed D-10 (not incorporated as binding rules). **Test status:** tests in Screen Contracts are specifications and remain NOT RUN.
