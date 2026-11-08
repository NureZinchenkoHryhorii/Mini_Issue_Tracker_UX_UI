# Mini Issue Tracker — UX/UI Decision Log

**File:** `Decision_Log_v0.1.md`  
**Version:** v0.1  
**Status:** IN PROGRESS — D-01 approved by project developer; D-02–D-08 pending  
**Date initialized:** 2026-11-08  
**Inputs:** S1 `SD_Spec.docx.pdf`; Methodological Guide §6; `01_Input_Pack_v1.0.md`.

## Decision candidates

| D-ID | Proposed decision | Source | Status | Approved by | Approval date |
|---|---|---|---|---|---|
| D-01 | Desktop grayscale low-fi; one Issues List with All / Important tabs; Create modal | Guide §6 | APPROVED | Project developer (user confirmation in ChatGPT) | 2026-11-08 |
| D-02 | S-01 is an authentication boundary placeholder; demo begins in authenticated S-02; do not invent login/SSO | Guide §6 | PROPOSED — NOT APPROVED | — | — |
| D-03 | Show unset priority as Not Set; only Low/Normal/High/Critical selectable; no reset action | Guide §6 | PROPOSED — NOT APPROVED | — | — |
| D-04 | New issue is unassigned; Team Lead may reassign | Guide §6; S1 gap | PROPOSED — NOT APPROVED; explicit decision needed | — | — |
| D-05 | Display role-dependent forbidden controls disabled (not hidden) | Guide §6 | PROPOSED — NOT APPROVED | — | — |
| D-06 | Assignee/priority/status use choice + local Apply; successful update remains in S-03 | Guide §6 | PROPOSED — NOT APPROVED | — | — |
| D-07 | Back from details preserves previous All / Important list tab | Guide §6 | PROPOSED — NOT APPROVED | — | — |
| D-08 | Fictional data and predefined prototype outcomes; no actual login/database | Guide §6 | PROPOSED — NOT APPROVED | — | — |

These entries are **not** S1 requirements. A student/teacher/reviewer must explicitly agree or reject each relevant design choice. Record the actual actor and date; never invent a sign-off.

## Extra unresolved questions

| Q-ID | Open question | Needed before |
|---|---|---|
| Q-01 | What login/authentication mechanism, if any, will be modeled beyond the boundary? | Detailed authentication design (not required for S-01 placeholder) |
| Q-02 | Is a new issue initially unassigned? | G2/G3 assignee states; see D-04 |
| Q-03 | Can the Team Lead reassign? | G2/G3 assignment behavior; see D-04 |
| Q-04 | How is Not Set stored technically? | Implementation, not wireframe |
| Q-05 | Exact comment-save-error wording/presentation? | Screen Contracts / Figma |
| Q-06 | Date-time display format and timezone? | Screen Contracts / Figma |
| Q-07 | Confirm user-facing name for Important Open Issues; rule remains non-Closed | Screen Contracts / Figma |
| Q-08 | Performance response-time measurement scope? | Implementation tests |
| Q-09 | Backup retention, frequency, restore method? | Implementation |
| Q-10 | Fictional predefined user names? | Demo test data; see D-08 |
| Q-11 | After successful issue creation, stay on list or open created issue details? | Final G2 transition table |

## Approval record template

| Date | Reviewer/decision maker | D-ID | Final decision | Status (APPROVED / REJECTED / DEFERRED) | Reason / source impact |
|---|---|---|---|---|---|
| 2026-11-08 | Project developer (user confirmation in ChatGPT) | D-01 | Desktop grayscale low-fidelity; one Issues List with All / Important tabs; Create modal | APPROVED | Confirmed explicitly in project conversation; methodology §6 UX choice, not S1 requirement |

## Rules for using this log

- Enter **APPROVED** only after an actual human decision with name and date.
- Do not override S1 acceptance criteria or business rules with UX choices.
- If a decision changes, preserve the original entry in history rather than disguising it as an S1 requirement.
- Copy only APPROVED D-IDs to `01_Input_Pack_v1.0.md` §8.2.
- Until approvals are recorded, do not present `02_Screen_Map_v0.1.md` as an agreed plan.
