# UX/UI Design Input Pack — Mini Issue Tracker

**File:** `01_Input_Pack_v1.0.md`  
**Version:** v1.0  
**Status:** REVIEW — Control A completed; awaiting human decision approval / Control B. NOT APPROVED  
**Source specification:** `SD_Spec.docx.pdf` (S1)  
**Purpose:** Source-checked input for UX/UI planning. SOURCE requirements are separated from decision candidates; no unapproved design decisions are binding.

---

## 0. Source and extraction status

### Source file read

**S1 — `SD_Spec.docx.pdf`**

The complete 13-page specification was available and read. The following sections were accessible:

- §0 — Customer Request
- §1 — Discovery / Problem Analysis
- §2 — Product Vision + Initial Product Scope
- §3 — Stakeholder Needs & Stakeholder Requirements, including BR-01–BR-12
- §4 — Prioritization of Needs + Candidate MVP
- §5 — Detailed Functional Requirements / User Stories + Acceptance Criteria
- §6 — Quality Attributes + Security Requirements
- §7 — Feasibility, Estimation & Risk Assessment
- §8 — MVP / Release Scope and Updated NFRs
- §9 — UX/UI & Interaction Design (heading available; no further detailed requirements in the supplied pages)

**Extraction rule:** §8 defines the final Release MVP. Earlier prioritization in §4 is retained as context, not used to override §8. Conflicts and gaps are recorded in the unresolved questions section.

**Classification:**
- `SOURCE` — explicitly stated in S1.
- `DERIVED` — follows from one or more source requirements; supporting sources are identified.
- `PROPOSED` — possible design suggestion, not a binding requirement.
- `UNRESOLVED` — requires clarification or a human decision.

---

## 1. Product purpose, actors and release boundaries

### 1.1 Product purpose

`SOURCE` — Mini Issue Tracker is an internal web application for a small software development team. It supports registering issues, tracking their lifecycle, assigning responsibility, setting priorities and discussing issues. It also helps the team identify important unresolved issues.

**Source:** S1 §1 Problem Statement and Product Business Goal; §2 Product Vision.

### 1.2 Primary actors

| Actor | Description | Source |
|---|---|---|
| Team Member | Authenticated member of the internal team. Can create issues, view issues, add comments and manage status when assigned to the issue. | S1 §1 Primary Users; §3 BR-01, BR-02, BR-08; §5 US-01, US-02, US-05, US-06, US-07 |
| Team Lead | Authenticated team lead. Can perform team-member activities and is authorized to assign issues and set/change priority. | S1 §1 Primary Users; §1 Open Questions; §3 BR-01, BR-06; §5 US-03, US-04 |

`SOURCE` — The first version has three predefined users: two Team Members and one Team Lead.

**Source:** S1 §1 Open Questions; §3 BR-01.

### 1.3 Secondary stakeholders

`SOURCE` — Product Owner / customer and System Administrator are secondary stakeholders. They are interested in outcomes or proper system operation but are not primary users in the main MVP scenarios.

**Source:** S1 §1 Stakeholders.

### 1.4 Release boundary

`SOURCE` — The product is a web application for internal team members, not an external customer portal. The first release is limited to the final scope listed in §8.

**Source:** S1 §1 KC-01–KC-07; §8 Release Scope.

---

## 2. Release scope

### 2.1 Included in Release MVP

`SOURCE` — The final Release MVP is **US-01 through US-08**.

| User Story | Name | Included capability | Source |
|---|---|---|---|
| US-01 | Create Issue | Register an issue with a title and description. | S1 §5 US-01 |
| US-02 | View Issues | View the issue list and individual issue details. | S1 §5 US-02 |
| US-03 | Assign Issue to the responsible team member | Assign one team member as the issue assignee. | S1 §5 US-03 |
| US-04 | Set Issue Priority | Set or change issue priority. | S1 §5 US-04 |
| US-05 | Track Issue Progress | View the current issue status. | S1 §5 US-05 |
| US-06 | Add Comment | Add comments to an issue. | S1 §5 US-06 |
| US-07 | Update Issue Status | Change issue status according to the specified rules. | S1 §5 US-07; §3 BR-07, BR-08 |
| US-08 | View Important Open Issues | Find High/Critical issues that are not Closed. | S1 §5 US-08; §3 BR-09, BR-09.1 |

**Source:** S1 §8 MVP / Release Scope.

### 2.2 Deferred

`SOURCE` — **US-09 — Attach files to an issue** is deferred and is not part of the first release.

The specification identifies additional implementation needs for attachments, including file storage, file-size limits, malware scanning and backup.

**Source:** S1 §5 US-09; §7 Recommended scope adjustment; §8 Deferred.

### 2.3 Future requirements

`SOURCE` — The following stakeholder requirements are future requirements, not part of the current Release MVP:

- `SR-10` — Automatic issue categorization.
- `SR-11` — Automatic priority recommendation.

**Source:** S1 §3 SR-10, SR-11; §4 Future / Deferred Requirements; §8 Future.

`SOURCE` — If AI functionality is implemented in the future, it must be recommendation-based. It must not automatically change category or priority without a user action.

**Source:** S1 §3 BR-12.

### 2.4 Explicitly out of scope

`SOURCE` — The following are outside the current product scope:

- Customer support portal.
- Billing.
- Source-code hosting.
- Continuous Integration / Continuous Delivery.
- Time tracking.
- Full project management.
- Mobile application.
- Integration with GitHub, GitLab, Jira or other issue trackers in the first version.
- Issue attachments in the first release.
- Automatic issue categorization and automatic priority recommendation in the first release.
- Issue deletion.
- Separate user-facing change history.

**Sources:** S1 §1 KC-05, KC-06; §2 Out of Scope; §3 BR-10, BR-11; §8 Release Scope.

`DERIVED` — The UX/UI design must not introduce screens, controls or flows for deferred/future functions as if they were available in the current release.

**Reason:** Only US-01–US-08 are included in the final Release MVP; US-09 is deferred and SR-10/SR-11 are future requirements.

**Source:** S1 §8.

---

## 3. Included User Stories and Acceptance Criteria

All acceptance criteria below preserve their original identifiers. The four US-03 criteria are unnumbered in S1; they are referenced by their original position and are not assigned invented AC IDs.

### US-01 — Create Issue

**Actor:** Team Member (any authenticated team member).  
**Goal:** Create an issue with a title and description so that a problem is recorded and can be tracked.

**Source:** S1 §5 US-01; §3 BR-01, BR-02.

| Original ID | Acceptance criterion | Type | Source |
|---|---|---|---|
| AC-01.1 | The user can enter a Title and a Description. | SOURCE | S1 §5 US-01, AC-01.1 |
| AC-01.2 | Title is required. | SOURCE | S1 §5 US-01, AC-01.2 |
| AC-01.3 | Description is required. | SOURCE | S1 §5 US-01, AC-01.3 |
| AC-01.4 | After creation, the issue receives an ID, status = Open, created_at and author. | SOURCE | S1 §5 US-01, AC-01.4 |
| AC-01.5 | After creation, the issue priority is not set. | SOURCE | S1 §5 US-01, AC-01.5; §3 BR-04 |

**Additional source examples — not additional ACs:**

- The Gherkin example for successful creation shows an authenticated user entering a title and description and clicking Create. The result is a new issue with status Open, a unique ID and the current user as author.
- The Gherkin example for an empty title says the issue is not created and the system displays `Title is required`.

**Source:** S1 §5, Gherkin scenarios for AC-01 and AC-02.

`DERIVED` — Both Title and Description must be present for successful creation because AC-01.2 and AC-01.3 independently mark them as required.

**Source:** S1 §5 AC-01.2, AC-01.3.

`SOURCE` — Any authenticated team member may create an issue; creation is not restricted to Team Lead.

**Source:** S1 §1 Open Questions; §3 BR-02.

### US-02 — View Issues

**Actor:** Team Member.  
**Goal:** View registered issues and inspect their current details.

**Source:** S1 §5 US-02; §3 BR-01.

| Original ID | Acceptance criterion | Type | Source |
|---|---|---|---|
| AC-02.1 | An authenticated team member can view the list of registered issues. | SOURCE | S1 §5 US-02, AC-02.1 |
| AC-02.2 | Each issue in the list displays at least: ID, Title, Status, Priority and Assignee if one is assigned. | SOURCE | S1 §5 US-02, AC-02.2 |
| AC-02.3 | The user can select an issue from the list and open its details page. | SOURCE | S1 §5 US-02, AC-02.3 |
| AC-02.4 | The issue details page displays: ID, Title, Description, Status, Priority, Assignee if assigned, Author and Created at. | SOURCE | S1 §5 US-02, AC-02.4 |
| AC-02.5 | If there are no registered issues, the system displays an empty list or a message indicating that there are no issues. | SOURCE | S1 §5 US-02, AC-02.5 |

`SOURCE` — Assignee is displayed conditionally: only if an assignee has been assigned.

**Source:** S1 §5 AC-02.2 and AC-02.4.

### US-03 — Assign Issue to the responsible team member

**Actor:** Team Lead.  
**Goal:** Assign an issue to a team member so that responsibility for its execution is clear.

**Source:** S1 §5 US-03; §1 Open Questions.

**Acceptance Criteria 03 — four original unnumbered points:**

| Original reference | Acceptance criterion | Type | Source |
|---|---|---|---|
| US-03, AC, point 1 | One assignee can be selected. | SOURCE | S1 §5 US-03, Acceptance Criteria 03, bullet 1 |
| US-03, AC, point 2 | The assignee must be a member of the team. | SOURCE | S1 §5 US-03, Acceptance Criteria 03, bullet 2 |
| US-03, AC, point 3 | Only Team Lead can assign an issue. | SOURCE | S1 §5 US-03, Acceptance Criteria 03, bullet 3; §1 Open Questions |
| US-03, AC, point 4 | The current assignee is displayed in the issue. | SOURCE | S1 §5 US-03, Acceptance Criteria 03, bullet 4 |

`DERIVED` — The assignment control must not allow selecting more than one assignee for a single issue.

**Reason:** US-03, AC, point 1 explicitly permits selecting one assignee.

**Source:** S1 §5 US-03, Acceptance Criteria 03, bullet 1.

### US-04 — Set Issue Priority

**Actor:** Team Lead.  
**Goal:** Set the issue priority so that the team can determine the order of work.

**Source:** S1 §5 US-04; §3 BR-05, BR-06.

| Original ID | Acceptance criterion | Type | Source |
|---|---|---|---|
| AC-04.1 | Allowed values for a set Priority are Low, Normal, High and Critical. | SOURCE | S1 §5 US-04, AC-04.1 |
| AC-04.2 | Only Team Lead can set and change priority. | SOURCE | S1 §5 US-04, AC-04.2; §3 BR-06 |

`SOURCE` — Before a priority is set, the issue may have an unset/empty priority. `Not Set` means absence of a priority, not a fifth priority level.

**Source:** S1 §1 Open Questions; §3 BR-04, BR-05.

### US-05 — Track Issue Progress

**Actor:** Team Member.  
**Goal:** See the current status of an issue to understand its current progress.

**Source:** S1 §5 US-05.

| Original ID | Acceptance criterion | Type | Source |
|---|---|---|---|
| AC-05.1 | The current status is displayed for every issue. | SOURCE | S1 §5 US-05, AC-05.1 |
| AC-05.2 | Status is displayed on the issue page. | SOURCE | S1 §5 US-05, AC-05.2 |
| AC-05.3 | Status is displayed in the issues list. | SOURCE | S1 §5 US-05, AC-05.3 |

### US-06 — Add Comment

**Actor:** Team Member.  
**Goal:** Add comments to an issue to discuss the problem.

**Source:** S1 §5 US-06.

| Original ID | Acceptance criterion | Type | Source |
|---|---|---|---|
| AC-06.1 | Comment text cannot be empty. | SOURCE | S1 §5 US-06, AC-06.1 |
| AC-06.2 | An added comment is stored and shown for the issue. | SOURCE | S1 §5 US-06, AC-06.2 |
| AC-06.3 | The comment author is stored and displayed. | SOURCE | S1 §5 US-06, AC-06.3 |
| AC-06.4 | The comment creation date/time is stored and displayed. | SOURCE | S1 §5 US-06, AC-06.4 |
| AC-06.5 | If saving fails, no comment is created and an error is produced. | SOURCE | S1 §5 US-06, AC-06.5 |

`DERIVED` — A failed comment save must not be represented as a successful comment or appear in the saved comments list.

**Reason:** AC-06.5 explicitly says a failed save does not create a comment.

**Source:** S1 §5 AC-06.5.

### US-07 — Update Issue Status

**Actor:** Team Member who is responsible for the issue (the current assignee).  
**Goal:** Change the issue status so that the team can see the current state of work.

**Source:** S1 §5 US-07; §3 BR-07, BR-08, BR-08.1.

| Original ID | Acceptance criterion | Type | Source |
|---|---|---|---|
| AC-07.1 | A new issue is created with status Open. | SOURCE | S1 §5 US-07, AC-07.1; §3 BR-03 |
| AC-07.2 | Allowed statuses are Open, In Progress, Resolved and Closed. | SOURCE | S1 §5 US-07, AC-07.2; §3 BR-07 |
| AC-07.3 | After a status change, the system stores the new value and displays it on the next view of the issue. | SOURCE | S1 §5 US-07, AC-07.3 |
| AC-07.4 | A user who is not the issue assignee cannot change its status. | SOURCE | S1 §5 US-07, AC-07.4 |
| AC-07.5 | The system does not allow a status value outside the defined list. | SOURCE | S1 §5 US-07, AC-07.5 |

**Allowed status transitions:**

| From | To | Type | Source |
|---|---|---|---|
| Open | In Progress | SOURCE | S1 §3 BR-08.1 |
| In Progress | Resolved | SOURCE | S1 §3 BR-08.1 |
| Resolved | Closed | SOURCE | S1 §3 BR-08.1 |
| Resolved | In Progress | SOURCE | S1 §3 BR-08.1 |

`SOURCE` — All other status transitions are prohibited.

**Source:** S1 §3 BR-08.1.

`DERIVED` — Closed has no allowed outgoing transition because it is not listed as a source state in any permitted transition, and all other transitions are explicitly prohibited.

**Source:** S1 §3 BR-08.1.

`DERIVED` — The status-changing user must be the current assignee. A Team Lead who is not the current assignee must not be allowed to change status.

**Reason:** BR-08 gives status-changing ability to the member responsible for the issue; AC-07.4 explicitly prohibits a user who is not the assignee from changing status. The Team Lead's separate assignment/priority permissions do not override this restriction.

**Sources:** S1 §3 BR-08; §5 AC-07.4.

### US-08 — View Important Open Issues

**Actor:** Team Member.  
**Goal:** Quickly see important issues that need priority attention.

**Source:** S1 §5 US-08; §3 BR-09, BR-09.1.

| Original ID | Acceptance criterion | Type | Source |
|---|---|---|---|
| AC-08.1 | An issue with priority = High and status other than Closed appears in Important Issues. | SOURCE | S1 §5 US-08, AC-08.1 |
| AC-08.2 | An issue with priority = Critical and status other than Closed appears in Important Issues. | SOURCE | S1 §5 US-08, AC-08.2 |
| AC-08.3 | Issues with priority = Low or Normal do not appear in Important Issues. | SOURCE | S1 §5 US-08, AC-08.3 |
| AC-08.4 | Issues with status = Closed do not appear, regardless of priority. | SOURCE | S1 §5 US-08, AC-08.4 |

`SOURCE` — Resolved means resolved but not yet closed. Until the issue reaches Closed, it remains active and may appear in Important Issues according to its priority.

**Source:** S1 §3 BR-09.1.

`DERIVED` — Important Issues includes High/Resolved and Critical/Resolved issues. Resolved must not be treated as Closed.

**Reason:** AC-08.1 and AC-08.2 exclude only Closed status; BR-09.1 explicitly confirms that Resolved remains active until Closed.

**Sources:** S1 §3 BR-09.1; §5 AC-08.1, AC-08.2.

`DERIVED` — An issue with priority Not Set is not Important because the only included priority values are High and Critical.

**Reason:** BR-04 defines Not Set as an unset priority; AC-08.1–AC-08.3 specify the included and excluded priority values.

**Sources:** S1 §3 BR-04, BR-09; §5 AC-08.1–AC-08.3.

---

## 4. UI-relevant Business Rules

### 4.1 Authentication and actors

| Rule | Requirement | Type | Source |
|---|---|---|---|
| BR-01 | Only authenticated team members may use the system. The first version has two Team Members and one Team Lead predefined. | SOURCE | S1 §3 BR-01 |
| BR-02 | Any authenticated team member can create an issue. | SOURCE | S1 §3 BR-02 |
| US-03 assignment restriction | Only Team Lead can assign an issue. | SOURCE | S1 §5 US-03, AC point 3; §1 Open Questions |
| BR-06 | Only Team Lead can set or change issue priority. | SOURCE | S1 §3 BR-06 |
| BR-08 + AC-07.4 | The responsible/current assignee can change status; a non-assignee cannot. | SOURCE | S1 §3 BR-08; §5 AC-07.4 |

### 4.2 Initial values and allowed values

| Property | Required value / behavior | Type | Source |
|---|---|---|---|
| New issue status | Open | SOURCE | S1 §3 BR-03; §5 AC-01.4, AC-07.1 |
| New issue priority | Not Set / unset / empty | SOURCE | S1 §3 BR-04; §5 AC-01.5 |
| Set priority values | Low, Normal, High, Critical | SOURCE | S1 §3 BR-05; §5 AC-04.1 |
| Allowed statuses | Open, In Progress, Resolved, Closed | SOURCE | S1 §3 BR-07; §5 AC-07.2 |
| Assignee count | One assignee can be selected | SOURCE | S1 §5 US-03, AC point 1 |
| Assignee eligibility | Must be a team member | SOURCE | S1 §5 US-03, AC point 2 |

`DERIVED` — Not Set is an absence of priority and must not be represented as a selectable fifth priority level.

**Sources:** S1 §3 BR-04, BR-05; §5 AC-04.1.

### 4.3 Status transitions and restrictions

| Rule | Required behavior | Type | Source |
|---|---|---|---|
| Allowed transition 1 | Open → In Progress | SOURCE | S1 §3 BR-08.1 |
| Allowed transition 2 | In Progress → Resolved | SOURCE | S1 §3 BR-08.1 |
| Allowed transition 3 | Resolved → Closed | SOURCE | S1 §3 BR-08.1 |
| Allowed transition 4 | Resolved → In Progress (reopen work) | SOURCE | S1 §3 BR-08.1 |
| Other transitions | Not allowed | SOURCE | S1 §3 BR-08.1 |
| Closed | No outgoing transition is specified or permitted | DERIVED | S1 §3 BR-08.1 |
| Status permission | Non-assignee cannot change status | SOURCE | S1 §5 AC-07.4 |
| Invalid status values | Must not be accepted | SOURCE | S1 §5 AC-07.5 |

### 4.4 Important Issues predicate

`DERIVED` — The inclusion rule is:

**Priority is High or Critical AND Status is not Closed.**

This means:

- High + Open → included.
- High + In Progress → included.
- High + Resolved → included.
- Critical + Open → included.
- Critical + In Progress → included.
- Critical + Resolved → included.
- Any priority + Closed → excluded.
- Low or Normal + any status → excluded.
- Not Set + any status → excluded because no qualifying priority is set.

**Sources:** S1 §3 BR-09, BR-09.1; §5 AC-08.1–AC-08.4.

### 4.5 Comments

| Rule | Required behavior | Type | Source |
|---|---|---|---|
| Comment text | Cannot be empty | SOURCE | S1 §5 AC-06.1 |
| Successful save | Comment is stored and shown for the issue | SOURCE | S1 §5 AC-06.2 |
| Author | Stored and displayed | SOURCE | S1 §5 AC-06.3 |
| Creation date/time | Stored and displayed | SOURCE | S1 §5 AC-06.4 |
| Failed save | No comment is created; an error is produced | SOURCE | S1 §5 AC-06.5 |

### 4.6 Prohibited actions and absent capabilities

| Prohibition / absence | Type | Source |
|---|---|---|
| Non-Team Lead cannot assign issues. | SOURCE | S1 §5 US-03, AC point 3 |
| Non-Team Lead cannot set or change priority. | SOURCE | S1 §3 BR-06; §5 AC-04.2 |
| Non-assignee cannot change issue status, including a Team Lead who is not the assignee. | SOURCE + DERIVED | S1 §5 AC-07.4; §3 BR-08 |
| Status transitions outside the four specified transitions are not allowed. | SOURCE | S1 §3 BR-08.1 |
| Invalid status values are not allowed. | SOURCE | S1 §5 AC-07.5 |
| Issues cannot be deleted. | SOURCE | S1 §3 BR-10; §1 Open Questions |
| Separate user-facing issue change history is not provided in the first version. | SOURCE | S1 §3 BR-11; §1 Open Questions |
| Attachments are not part of the first release. | SOURCE | S1 §8 Deferred |
| Automatic category and priority recommendations are not part of the first release. | SOURCE | S1 §8 Future |
| AI must not automatically change category or priority if future AI functionality is implemented. | SOURCE | S1 §3 BR-12 |

---

## 5. Relevant Non-Functional Requirements

The final list in §8 is treated as the current release NFR list.

| ID | Requirement | UX/UI relevance | Can a static wireframe verify it? | Type / Source |
|---|---|---|---|---|
| NFR-01 | Response time < 1 s | No specific screen is required. Performance is a runtime/system property. | No | SOURCE — S1 §8 Updated NFRs |
| NFR-02 | Authentication required | The design must respect the authenticated-user boundary; authentication itself is not specified in detail. | Partially: a boundary can be documented, but actual authentication cannot be verified in a wireframe. | SOURCE — S1 §8 Updated NFRs; §3 BR-01 |
| NFR-03 | HTTPS only | Technical transport/security requirement. | No | SOURCE — S1 §8 Updated NFRs |
| NFR-04 | Backup of all data | Operational/data protection requirement. | No | SOURCE — S1 §8 Updated NFRs |

### 5.1 Requirements not verifiable by static UI design

`DERIVED` — A static wireframe or clickable prototype cannot prove:

- Actual response time below one second.
- Enforcement of authentication and authorization by the running system.
- HTTPS transport.
- Backup execution, completeness or restoration.

These requirements must remain documented and must not be claimed as verified through visual design.

**Sources:** S1 §8 Updated NFRs; §3 BR-01, BR-06, BR-08.

### 5.2 Earlier NFR wording

`SOURCE` — §6 contains an earlier example NFR-04 wording: “Backup of all data + attachments”. The final §8 Updated NFRs state “Backup of all data”.

**UNRESOLVED / interpretation note:** The final release list does not include attachments because US-09 is deferred. The Pack records the final §8 wording and does not treat attachments as part of the first-release backup scope.

**Sources:** S1 §6 NFR-04; §8 Deferred and Updated NFRs.

---

## 6. Constraints and assumptions relevant to UX/UI

| ID | Statement | Type | Source |
|---|---|---|---|
| KC-01 | The system is intended for a small internal team. | SOURCE | S1 §1 KC-01 |
| KC-02 | The first release should be simple and quick to develop. | SOURCE | S1 §1 KC-02 |
| KC-03 | The system must work as a web application. | SOURCE | S1 §1 KC-03 |
| KC-04 | Users are team members, not external customers. | SOURCE | S1 §1 KC-04 |
| KC-05 | No GitHub, GitLab, Jira or other issue-tracker integration is planned for the first version. | SOURCE | S1 §1 KC-05 |
| KC-06 | AI functionality is not mandatory for the first release. | SOURCE | S1 §1 KC-06 |
| KC-07 | The solution should be suitable for future AI extensions. | SOURCE | S1 §1 KC-07 |
| A-01 | All users are assumed to belong to one team. | SOURCE — assumption | S1 §1 Assumptions |
| A-02 | The number of users is small, e.g. up to a few dozen. | SOURCE — assumption | S1 §1 Assumptions |
| A-03 | Only a small number of users are assumed to work simultaneously. | SOURCE — assumption | S1 §1 Assumptions |
| A-04 | One responsible assignee is sufficient for an issue. | SOURCE — assumption | S1 §1 Assumptions |
| A-05 | An issue has one current priority. | SOURCE — assumption | S1 §1 Assumptions |
| A-06 | Comments are sufficient for team discussion around an issue. | SOURCE — assumption | S1 §1 Assumptions |
| A-07 | A mobile application is not required for the first version. | SOURCE — assumption | S1 §1 Assumptions |
| A-08 | Future AI features are assumed to be recommendations, not automatic changes. | SOURCE — assumption | S1 §1 Assumptions |
| A-09 | There may be insufficient existing data to train an AI model. | SOURCE — assumption | S1 §1 Assumptions |

Assumptions are retained as assumptions; they are not silently promoted to confirmed implementation requirements.

---

## 7. Unresolved questions and conflicts (Q-ID)

These items require a human decision or clarification. They are not silently resolved by this Pack.

| Q-ID | Question / ambiguity | Evidence and source | Impact |
|---|---|---|---|
| Q-01 | Which authentication method is used? The specification requires authentication and three predefined users but does not define login mechanics. | S1 §1 Open Questions; §3 BR-01; §7 R-01; §8 NFR-02 | Do not invent password, SSO or other authentication screens/mechanics. |
| Q-02 | What is the initial assignee state of a newly created issue? Is it unassigned by default? | S1 §5 US-01 AC-01.4; US-02 AC-02.2/02.4; US-03 | The source says assignee may be absent in list/details, but does not explicitly define the initial assignment value. |
| Q-03 | Can Team Lead reassign an issue after an assignee has already been selected? | S1 §5 US-03 states that one assignee can be selected and only Team Lead can assign; it does not explicitly describe reassignment. | Do not assume reassignment behavior without approval. |
| Q-04 | How should the UI represent the technical value for Not Set? Is it stored as null, an enum value or another representation? | S1 §3 BR-04/BR-05; §5 AC-01.5; methodology notes | UI meaning is clear (no priority); technical representation is not. |
| Q-05 | What exact error text and presentation are required when a comment save fails? | S1 §5 AC-06.5 | The existence of an error is required; its exact wording and visual treatment are unspecified. |
| Q-06 | What are the date/time format and timezone rules for displaying issue creation time and comment creation time? | S1 §5 AC-02.4; AC-06.4 | Required data is known; display formatting is not. |
| Q-07 | Does “Important Open Issues” mean only status Open, or all statuses except Closed? | S1 §5 US-08 title/goal and AC-08.1/08.2; §3 BR-09.1 | The title/goal says “open”, but the explicit criteria include every status except Closed; BR-09.1 confirms Resolved remains active. The implementation rule is clear from AC/BR; naming remains potentially misleading. |
| Q-08 | What is the scope and measurement method for response time < 1 s? | S1 §8 NFR-01 | Cannot be tested or demonstrated by a static mockup. |
| Q-09 | What backup frequency, retention period and restore procedure are required? | S1 §8 NFR-04 | The backup requirement exists, but operational details are not specified. |
| Q-10 | Which exact predefined user identities/names are used for the two Team Members and one Team Lead? | S1 §1 Open Questions; §3 BR-01 | Do not invent real identities; sample names require a design/test-data decision. |
| Q-11 | What screen/list state follows a successful Create Issue action? | S1 §5 US-01 gives the result of creation but does not fix the navigation destination. | Navigation after success must be an explicitly decided UX behavior, not presented as SOURCE. |

### 7.1 Important rule interpretation — status permission

`SOURCE` — BR-08 states that the team member responsible for an issue should be able to change its status.

`SOURCE` — AC-07.4 states that a user who is not the issue assignee cannot change its status.

`DERIVED` — For UI permission modeling, the current assignee is the authorized status-changing user. Team Lead status permission is not implied merely by the Team Lead role. A Team Lead who is not the assignee remains restricted by AC-07.4.

**Sources:** S1 §3 BR-08; §5 AC-07.4.

### 7.2 Important rule interpretation — Important Issues

`SOURCE` — US-08 uses the phrase “Important Open Issues”, but AC-08.1 and AC-08.2 include High/Critical issues with any status other than Closed. BR-09.1 explicitly says Resolved is not yet Closed and remains active.

`DERIVED` — The predicate must be based on priority High/Critical and status not Closed, not status = Open only.

**Sources:** S1 §3 BR-09, BR-09.1; §5 AC-08.1–AC-08.4.

---

## 8. SOURCE requirements and APPROVED design decisions

### 8.1. SOURCE requirements (S1)

All product requirements remain in §§1–7 and the source traceability matrix in §9. Their origin is **S1 — SD_Spec.docx.pdf**, not the UX decision process. The final Release MVP is US-01–US-08; US-09 is Deferred, SR-10/SR-11 are Future. No original US, AC, BR, KC, A, SR or NFR identifiers have been renumbered.

The following are important SOURCE/DERIVED constraints, **not** optional design preferences:
- Team Lead alone may assign issues (US-03, AC, point 3) and set/change priority (BR-06, AC-04.2).
- Only the *current assignee* can change issue status; this also restricts a Team Lead who is not the assignee (BR-08 and AC-07.4).
- Only four transitions are permitted: Open → In Progress; In Progress → Resolved; Resolved → Closed; Resolved → In Progress (BR-08.1). Closed has no outgoing status transition.
- A newly created issue has status Open and unset priority / Not Set (BR-03/04; AC-01.4/01.5). Not Set is not a fifth selectable priority level (BR-04/05).
- Important = priority ∈ {High, Critical} AND status != Closed; High/Critical + Resolved stays included (BR-09/09.1; AC-08.1–08.4).
- Failed comment save means error and **no created comment** (AC-06.5).
- The Gherkin example provides the exact example message `Title is required`, but no universal exact wording for other validation errors (§5 US-01).

### 8.2. APPROVED design decisions (D)

**D-01 — APPROVED (2026-11-08; project developer, explicit user confirmation in ChatGPT):** Desktop grayscale low-fidelity design; one Issues List with All / Important tabs; Create Issue is a modal. Source: Methodological Guide §6, D-01. This is an approved UX decision, **not** a SOURCE/S1 requirement.

**D-02–D-08:** remain UNRESOLVED, awaiting human approval. Do not treat draft screen-map decisions as approved.

An AI-generated suggestion or a draft Screen Map is not human authorization. When a student/reviewer explicitly approves a decision, record its D-ID, exact text, approving person, date and scope in `Decision_Log_v0.1.md`, then copy that decision here without altering SOURCE requirements. Until then, keep it UNRESOLVED.

### 8.3. Decision candidates from the methodology (NOT approved)

| D-ID | Proposed decision | Current status | Source |
|---|---|---|---|
| D-01 | Desktop grayscale low-fidelity; one list with All / Important tabs; Create in a modal | APPROVED — 2026-11-08; project developer confirmation | Methodological Guide §6 |
| D-02 | S-01 represents authentication boundary only; demo starts from already authenticated S-02; no invented login method | UNRESOLVED — approval needed | Methodological Guide §6 |
| D-03 | Display unset priority as Not Set; only Low/Normal/High/Critical can be selected; do not add reset | UNRESOLVED — approval needed | Methodological Guide §6 |
| D-04 | A new issue starts unassigned; Team Lead may reassign an issue | UNRESOLVED — explicit confirmation needed because S1 does not fully specify this | Methodological Guide §6 |
| D-05 | Show role-forbidden controls disabled rather than hidden | UNRESOLVED — approval needed | Methodological Guide §6 |
| D-06 | Each assignee/priority/status change uses its own Apply; success keeps S-03 open | UNRESOLVED — approval needed | Methodological Guide §6 |
| D-07 | Return from issue details to the previously selected list tab | UNRESOLVED — approval needed | Methodological Guide §6 |
| D-08 | Use fictional demo data and predetermined simulated prototype outcomes; no real login/database | UNRESOLVED — approval needed | Methodological Guide §6 |

These are *methodology-suggested UX choices*, not additional S1 product requirements. Do not silently convert them to SOURCE or APPROVED.

### 8.4. Other unapproved implementation/UX details

Exact authentication method, visual error messages (apart from the source Gherkin example), date/time formatting, post-create navigation, technical database representation of unset priority, frame count and prototype wiring are not independently specified by S1. Treat them as UNRESOLVED or PROPOSED and do not invent product functionality.

---

## 9. Source Check

### 9.1 Included User Stories → all AC → Pack location

| Included US | Source AC count | Source criteria accounted for | Pack location |
|---|---:|---|---|
| US-01 — Create Issue | 5 | AC-01.1–AC-01.5 | §3 US-01 |
| US-02 — View Issues | 5 | AC-02.1–AC-02.5 | §3 US-02 |
| US-03 — Assign Issue | 4 | Four original unnumbered points, retained by original position | §3 US-03 |
| US-04 — Set Issue Priority | 2 | AC-04.1–AC-04.2 | §3 US-04 |
| US-05 — Track Issue Progress | 3 | AC-05.1–AC-05.3 | §3 US-05 |
| US-06 — Add Comment | 5 | AC-06.1–AC-06.5 | §3 US-06 |
| US-07 — Update Issue Status | 5 | AC-07.1–AC-07.5 | §3 US-07 |
| US-08 — View Important Open Issues | 4 | AC-08.1–AC-08.4 | §3 US-08 |
| **TOTAL** | **33** | **All 33 substantive AC accounted for** | **§3** |

`SOURCE CHECK` — The four US-03 criteria are unnumbered in S1 and have not been assigned invented AC identifiers. Gherkin examples under US-01 are alternative examples, not additional acceptance criteria.

**Sources:** S1 §5; §8 Release Scope. Methodology Control A, §5.

### 9.2 Excluded requirements and reasons

| Requirement | Status | Reason | Source |
|---|---|---|---|
| US-09 — Attach files to an issue | Deferred / excluded from Release MVP | Explicitly listed as Deferred in final Release Scope. | S1 §8 |
| SR-10 — Automatic issue categorization | Future / excluded from Release MVP | Explicitly listed as Future. | S1 §8 |
| SR-11 — Automatic priority recommendation | Future / excluded from Release MVP | Explicitly listed as Future. | S1 §8 |
| Issue deletion | Out of current release | BR-10 says issues are not deleted. | S1 §3 BR-10 |
| Separate issue change history | Out of current release | BR-11 says a separate user-facing change history is not provided in the first version. | S1 §3 BR-11 |
| Customer support portal, billing, source-code hosting, CI/CD, time tracking, full project management, mobile application | Out of scope | Explicitly listed in Initial Product Scope. | S1 §2 |
| GitHub/GitLab/Jira or other issue-tracker integrations | Out of scope for first version | KC-05. | S1 §1 KC-05 |

### 9.3 Unresolved questions

- Q-01 — Authentication method.
- Q-02 — Initial assignee state.
- Q-03 — Reassignment behavior.
- Q-04 — Technical representation of Not Set.
- Q-05 — Exact comment save-error text/presentation.
- Q-06 — Date/time format and timezone.
- Q-07 — “Important Open Issues” naming versus explicit non-Closed predicate.
- Q-08 — Response-time measurement scope.
- Q-09 — Backup frequency, retention and restore details.
- Q-10 — Names/identities for predefined sample users.
- Q-11 — Post-create navigation destination.

### 9.4 Extraction and Control A status

- Final Release MVP identified from §8: **US-01–US-08**.
- Included User Stories: **8**.
- Substantive Acceptance Criteria: **33**.
- US-03 unnumbered criteria preserved: **4**.
- Deferred: **US-09**.
- Future: **SR-10, SR-11**.
- UI-relevant BR preserved: **BR-01–BR-12 where applicable**.
- Unresolved questions recorded: **Q-01–Q-11**.

**Status: REVIEW — automated source-to-Pack completeness check completed; human decisions/review still pending. NOT APPROVED.**

---

## 10. Control A — source review record (2026-11-08)

**Source inspected:** S1, `SD_Spec.docx.pdf`, all 13 pages, especially §§1, 3, 5, 8.  
**Methodology inspected:** `Mini_Issue_Tracker_UX_UI_Methodological_Guide_UA.docx.pdf`, §§4–7 and Control A.  
**Compared draft:** `01_Input_Pack_v0.1.md` in repository `NureZinchenkoHryhorii/Mini_Issue_Tracker_UX_UI`, branch `main`.

### 10.1 Acceptance criteria verification

| Included story | Source criteria checked | Count | Located in Pack | Control A result |
|---|---|---:|---|---|
| US-01 | AC-01.1, AC-01.2, AC-01.3, AC-01.4, AC-01.5 | 5 | §3 US-01 | COVERED |
| US-02 | AC-02.1, AC-02.2, AC-02.3, AC-02.4, AC-02.5 | 5 | §3 US-02 | COVERED |
| US-03 | US-03, AC, point 1; point 2; point 3; point 4 (unnumbered in S1) | 4 | §3 US-03 | COVERED |
| US-04 | AC-04.1, AC-04.2 | 2 | §3 US-04 | COVERED |
| US-05 | AC-05.1, AC-05.2, AC-05.3 | 3 | §3 US-05 | COVERED |
| US-06 | AC-06.1, AC-06.2, AC-06.3, AC-06.4, AC-06.5 | 5 | §3 US-06 | COVERED |
| US-07 | AC-07.1, AC-07.2, AC-07.3, AC-07.4, AC-07.5 | 5 | §3 US-07 | COVERED |
| US-08 | AC-08.1, AC-08.2, AC-08.3, AC-08.4 | 4 | §3 US-08 | COVERED |
| **TOTAL** | **8 User Stories / 33 substantive AC; Gherkin not counted again** | **33** | **§3** | **COVERED** |

### 10.2 Critical rules checked against S1

| Check | Evidence | Result |
|---|---|---|
| Final Release MVP overrides Candidate MVP scope | S1 §8; §2 Pack | COVERED — US-01…US-08 only |
| Deferred/Future excluded | S1 §8; §2 and §9 Pack | COVERED — US-09, SR-10, SR-11 |
| Team Lead only Assignment/Priority | S1 §1 answers; §3 BR-06; §5 US-03/04 | COVERED |
| Current assignee only may change status, even when lead is not assignee | S1 §3 BR-08; §5 AC-07.4 | COVERED |
| All and only four transitions; Closed is terminal | S1 §3 BR-08.1 | COVERED |
| Creation default: Open, priority unset | S1 §3 BR-03/04; §5 US-01 | COVERED |
| Resolved High/Critical remains Important; Closed excluded | S1 §3 BR-09.1; §5 US-08 | COVERED |
| Failed comment save: no created comment | S1 §5 AC-06.5 | COVERED |
| Source Gherkin example `Title is required` retained | S1 §5 US-01 | COVERED |
| Four NFRs and static mockup limitation | S1 §8 | COVERED |

### 10.3 Corrections made when preparing v1.0

1. Kept all S1 requirement content and the complete original source traceability matrix.
2. Clearly separated SOURCE requirements from the **APPROVED design decisions** section (currently empty).
3. Recorded methodology's D-01–D-08 suggestions as **UNRESOLVED**, without silently treating them as approved or product SOURCE.
4. Added Q-11 for post-create navigation, identified during G2 planning.
5. Corrected document filename/version metadata and added this explicit Control A record.
6. Clarified that the source's `Title is required` Gherkin error example exists, while exact wording for other errors remains unspecified.

**No missing substantive AC was detected in v0.1.**

### 10.4 Remaining gates / approval record

- **Decision Log:** approval statuses, reviewers and dates not yet supplied. See `Decision_Log_v0.1.md`.
- **G2 readiness:** dependent on a valid Input Pack v1.0 and approved decision log; draft G2 must not be automatically promoted.
- **Control B (later stage):** another student or teacher should review requirements matrices and boundary cases, and record reviewer, date, version, accepted decisions and open blockers. Follow Methodological Guide §11.
- **Reviewer:** PENDING
- **Date of human review:** PENDING
- **Accepted D-ID:** D-01 (2026-11-08; project developer confirmation)
- **Open blockers:** D-02–D-08 approvals; Q-02/Q-03 if D-04 is not approved; Q-11 navigation choice.
- **Approval status:** **NOT APPROVED**. Do not claim Control B was performed.

