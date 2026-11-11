# Mini Issue Tracker — 06 Review Report

**Artifact:** `06_Review_Report.md`  
**Review type:** G6 — static evidence audit and student-reported P1 prototype testing  
**Review date:** 2026-11-11  
**Reviewer:** ChatGPT — document/screenshot comparison; independent human reviewer: **not assigned**  
**Project:** [Figma working file](https://www.figma.com/design/S1oyc2GzQYRCKYfuuWnVf6/Untitled--Copy-?node-id=0-1)  
**Design version:** WORKING F1/P1 draft; Figma file version/hash **not provided**. Control B **SKIPPED by developer decision**; no independent approval claimed.  
**Requirements basis:** S1 `SD_Spec.docx.pdf` (US-01–US-08; 33 included AC, with the 4 US-03 points originally unnumbered); `03_Screen_Contracts_v1.0.md` (REVIEW); `02_Screen_Map_v1.0.md`; `Decision_Log_v0.1.md` (APPROVED D-01–D-09); `05_Figma_Brief_v1.0.md` (working draft).

## 0. Evidence boundary and observed IDs

**Direct Figma inspection:** the supplied Figma URL could not be loaded for visual/canvas inspection in this review environment. No access to the live Figma layer tree, prototype links, or current version history was obtained. Therefore **the report does not claim direct observation of the final live file**.

**Readable earlier screenshots provided in this conversation** (screenshots of the initial F1 work; **not new screenshots of the subsequently AI-edited final P1 version**):

- **E1:** `S-02-A — Issues List · All.png` — readable All list with ISS-001–ISS-006; fields ID, Title, Status, Priority, Assignee. The new live P1 connections are not evidenced by this still image.
- **E2:** `Reference — S-02 list states.png` — readable **S-02-B Important**, **S-02-C Empty All**, **S-02-C Empty Important**. S-02-B was later promoted to a separate top-level frame according to the student's account; the new live frame was not directly inspected in this review.
- **E3:** `S-03 — Issue Details · ISS-002.png` — readable Issue Details, Member B assignee, Lead C demonstration context, Status In Progress disabled, two comments (author/time), three field-level Apply controls.
- **E4:** `Reference — Permissions and status.png` — readable all four role/assignee contexts, exactly four status values, allowed-next-state examples, Closed/Unassigned and status before/after example.
- **E5:** `Reference — Reusable UI and validation.png` — readable Title/Description validation, empty-comment validation, failed-save error, successful-comment example, priority values, ISS-007 creation result.
- **E6:** `S-03 — Issue Details · ISS-007.png` from subsequent conversation — readable new issue ID, Title/Description, Author Lead C, Created at, Status Open, Priority Not Set, Assignee Unassigned; the screenshot shows an intermediate editable draft (see defect DEF-01).
- **E7:** `Reference — Scope, sources and navigation.png` — readable non-interactive S-01 boundary, Important predicate, T-01–T-25 annotations, scope/exclusions and process status.
- **E8:** screenshot of Figma Layers and Prototype interaction showing `On click → Back` on ISS-002, plus a screenshot of Figma Starter upgrade prompt for variables. These confirm the **presence of the shown UI controls at screenshot time**, not all final routes.

**Visible Screen/State IDs:** S-01 (annotation), S-02-A, S-02-B, S-02-C (All and Important), M-01, S-03 (ISS-002 and ISS-007), status contexts (Member non-assignee, Member assignee, Lead non-assignee, Lead assignee), and error/success references. The main text in E1–E6 is legible. Fine-print provenance text in the tall E7 reference is small; its existence and main headings can be read, but a final legibility assessment at normal Figma zoom is **not verified**. Final P1 screenshots and full live frame coverage are not provided. Unseen content is **not** presumed absent.

**P1 — STUDENT-REPORTED, not independently observed:** the student reported testing in Figma Present: All ↔ Important; Create/Cancel/Back and correct return context; ISS-002 from both tabs; Team Lead Assignee and Priority Apply demonstrations; four legal status transitions and blocked Lead non-assignee/Closed actions; comment success/empty/failure demonstrations. The Figma Agent's textual completion report was **not** used as proof of completion. Some intermediate navigation screenshots predate the final Agent edits.

**Result meanings:** PASS = the expected *visible UI evidence* is present in supplied screenshots; PARTIAL = only an illustrated or student-reported portion is supported, or a key precondition/effect remains unverified; FAIL = a contradiction is visible; NOT VERIFIABLE = no adequate evidence or implementation-only verification. **A screenshot PASS is not an implementation PASS.**

## A. Requirements audit — 33 included AC

| Source | Expected | Screen/State | Observed evidence | Result | Remaining test |
|---|---|---|---|---|---|
| AC-01.1 | Title і Description — обидва required | M-01 | E3: обидва поля з Required | PASS | Перевірити реальну валідацію у застосунку |
| AC-01.2 | Порожній Title → помилка, без issue | M-01 / validation | E5: `Title is required`, примітка no issue; не підтверджено дію кнопки на пустому полі | PARTIAL | Пройти негативний шлях у Present та server validation |
| AC-01.3 | Порожній Description → валідація, без issue | M-01 / validation | E5: Required field, без нового issue; negative path у Present не спостерігався | PARTIAL | Перевірити негативний шлях і server validation |
| AC-01.4 | Після створення — ID, author, created_at, Open | M-01 → S-03 ISS-007 | E5: ISS-007 / Lead C / час / Open; P: студент повідомив успішний Create | PARTIAL | Унікальність ID, автоматичне створення та persistence |
| AC-01.5 | Після Create priority відсутній | S-03 ISS-007 | E6: `Not Set`, не `Normal` | PASS | Backend default |
| AC-02.1 | Авторизований член команди бачить список | S-02-A | E1: 6 issues; S-01 boundary у E7; auth лише задекларовано | PARTIAL | Перевірити auth і actual data loading |
| AC-02.2 | У рядку ID, Title, Status, Priority, Assignee за наявності | S-02-A/B | E1/E2: потрібні колонки та рядки, для ISS-005 відсутній Assignee | PASS | Звірити з фактичною базою |
| AC-02.3 | З рядка відкриваються деталі того самого issue | S-02-A/B → S-03 ISS-002 | E1/E3: ISS-002 збігається; P: студент перевірив обидва маршрути | PARTIAL | У Present перевірити інші issue IDs, actual routing |
| AC-02.4 | Деталі: ID/Title/Description/Status/Priority/Assignee/Author/Created at | S-03 ISS-002 | E3: всі вказані поля присутні | PASS | Джерело фактичних даних |
| AC-02.5 | Нуль issues → порожній All | S-02-C Empty All | E2: Empty All зі збереженими tabs і Create Issue | PASS | Фактичне нульове dataset |
| US-03 AC п.1 (UIR-03.1) | Призначити не більш як одного assignee | S-03 / role examples | E4: одиночне поле Assignee; P: студент підтвердив Apply demo | PARTIAL | One-assignee persistence/cardinality |
| US-03 AC п.2 (UIR-03.2) | Assignee — тільки team member | S-03 / role examples | E4/E7: три фіксовані користувачі зазначені; dropdown options у скриншотах не розкрито | PARTIAL | Оглянути вибір, перевірити server membership |
| US-03 AC п.3 (UIR-03.3) | Лише Lead змінює assignee | S-03 / permissions reference | E4: Member disabled, Lead enabled; P: студент перевірив Lead Apply | PARTIAL | Серверний role-denial |
| US-03 AC п.4 (UIR-03.4) | Поточний assignee відображається | S-03 / S-02 | E1/E3: Member B для ISS-002; E6: Unassigned для ISS-007 | PASS | Persistence та оновлення після перепризначення |
| AC-04.1 | Priority лише Low/Normal/High/Critical | S-03 / priority reference | E5: чотири selectable values, `Not Set` окремо як absence | PASS | Backend enum і недійсні значення |
| AC-04.2 | Лише Lead може змінювати priority | S-03 / permissions | E4: Lead enabled, Member disabled; P: студент перевірив Apply | PARTIAL | Server permission |
| AC-05.1 | Для кожного issue є видимий статус | S-02-A/B / S-03 | E1/E2: кожен рядок має Status | PASS | Actual status consistency |
| AC-05.2 | Статус видно в деталях | S-03 ISS-002/ISS-007 | E3/E6: In Progress/Open | PASS | Actual database status |
| AC-05.3 | Статус видно в рядках списку | S-02-A/B | E1/E2: стовпець Status заповнений | PASS | Updated list state після зміни |
| AC-06.1 | Порожній comment заборонено | S-03 / empty comment | E5: `Comment body required`, примітка no new comment; P: студент повідомив перевірку | PARTIAL | Серверне блокування порожнього comment |
| AC-06.2 | Успішний nonempty comment показано під issue | S-03 / success example | E5: приклад нового comment; P: студент перевірив Add comment demo | PARTIAL | Реальне save/reload |
| AC-06.3 | Коментар зберігає та показує автора | S-03 / success example | E5: Lead C у success example (демо), E3: Member A/B у history | PARTIAL | Persistence фактичного автора |
| AC-06.4 | Коментар зберігає та показує час | S-03 / success example | E5: дата/час успішного прикладу, E3: timestamp попередніх | PARTIAL | Точний час, timezone, DB |
| AC-06.5 | Save failure → помилка й жодного нового коментаря | S-03 / failed save | E5: `Comment could not be saved`, два старі comments, нуль нових; P: студент повідомив demo | PARTIAL | Реальний save-failure + atomicity |
| AC-07.1 | Новий issue починається Open | S-03 ISS-007 | E6: Open; P: студент перевірив Create route | PARTIAL | DB initial value |
| AC-07.2 | Рівно чотири статуси | S-03 / status reference | E4/E5: Open / In Progress / Resolved / Closed | PASS | Server enum |
| AC-07.3 | Після дозволеної зміни статус зберігається і видний при повторному відкритті | S-03 / status sequence | E4: In Progress → Resolved, перед/після статичні приклади; P: студент повідомив усі 4 demo transitions | PARTIAL | Reopen + persisted value + list consistency |
| AC-07.4 | Тільки current assignee змінює status | S-03 / permission contexts | E4: Member-assignee та Lead-assignee enabled; Lead non-assignee disabled; P: студент повідомив перевірку | PARTIAL | Серверне enforce і повторне призначення |
| AC-07.5 | Недопустиме значення статусу не приймається | S-03 / status matrix | E4: лише законні переходи; відсутність довільного input, Closed disabled; P: студент повідомив check | PARTIAL | Спробувати невалідне значення у реалізації |
| AC-08.1 | High + не Closed входить в Important, включно з Resolved | S-02-B | E2: ISS-002 High/In Progress і ISS-003 High/Resolved | PASS | Actual predicate on live data |
| AC-08.2 | Critical + не Closed входить в Important | S-02-B | E2: ISS-001 Critical/Open, ISS-006 Critical/Resolved | PASS | Actual predicate on live data |
| AC-08.3 | Low/Normal/Not Set відсутні в Important | S-02-B / priority reference | E2: ISS-005 Not Set немає; E7 predicate explicitly excludes Low/Normal; немає Low/Normal issues у E1 sample | PARTIAL | Позитивний All-семпл Low/Normal і live filter |
| AC-08.4 | Closed завжди виключається з Important | S-02-A/B | E1: ISS-004 Critical/Closed в All; E2: ISS-004 відсутній в Important | PASS | Live filtering після переходу to Closed |

### A.1 UI-relevant business rules and approved UX decisions

| Source | Expected | Screen/State | Observed evidence | Result | Remaining test |
|---|---|---|---|---|---|
| BR-01 / D-02 | Only predefined authenticated team members; S-01 non-login boundary | S-01, S-02 | E7 shows boundary; no login UI | PARTIAL | Actual auth/NFR-02 |
| BR-02 | Auth team member or Lead may Create | S-02/M-01 | E1/E3 shows Create action; no live role-based auth | PARTIAL | Auth/role integration |
| BR-03 / BR-04 | Create → Open and unset priority | M-01, S-03 ISS-007 | E6 Open / Not Set | PASS | DB defaults |
| BR-05 / D-03 | Low/Normal/High/Critical only; Not Set not fifth priority or reset | S-03 / values reference | E5 four selectable levels, separate Not Set | PASS | Backend validation |
| BR-06 | Only Team Lead edits priority | S-03 / role examples | E4 enabled vs disabled; student tested Apply | PARTIAL | Server roles |
| BR-07 | Exactly 4 status values | S-03 / status reference | E4 four values | PASS | Backend enum |
| BR-08 / BR-08.1 | Only current assignee and four allowed transitions; Closed no outgoing | S-03 / role/status reference | E4 correct contexts and allowed transitions; student reported P1 checks | PARTIAL | Authorization, invalid transitions at API |
| BR-09 / BR-09.1 | Important=(High OR Critical) AND not Closed; Resolved included | S-02-B / E7 | E2 exact records; E7 predicate | PASS | Real filtered query/update |
| BR-10 / BR-11 | Remaining BR conditions defined in S1 | Cross-cutting | No complete implementation evidence presented | NOT VERIFIABLE | Verify original S1 source clauses and implementation against them |
| D-01 | Desktop grayscale; shared All/Important; modal Create | S-02, M-01 | E1/E2/E3 consistent | PASS | Native frame structure in final file |
| D-04 | Initial Unassigned and Lead reassign may be shown | S-03 ISS-007 / role ref | E6 Unassigned; E4 Lead enabled | PARTIAL | One-assignee assignment integration |
| D-05 | Denied controls visible but disabled | S-03 / permission contexts | E4 shows all contexts | PASS | Verify no unauthorized interactive hotspots in final file |
| D-06 | Local Apply next to Assignee/Priority/Status; stay in details | S-03 | E3/E4 field Apply controls; student reported two Apply paths | PARTIAL | Final clickable controls and outcomes |
| D-07 | Back to originating All/Important with filter reapplied | S-02 ↔ S-03 | Student reported Back from both origins; E7 describes rule | PARTIAL | Independently replay final P1; closed issue disappears |
| D-08 | Fictional static sample data, simulated results | E1–E7 | Sample IDs and source annotation; student confirms simulation | PASS | Distinguish demo from persistence in deliverable |
| D-09 | Successful Create → S-03 of newly created issue | M-01 → S-03 ISS-007 | E6 ISS-007; student reported flow | PARTIAL | Independently replay; ensure failures do not use success route |
| D-10 | Optional copy wording not approved | Error references | E5 explicitly labels non-source strings illustrative | PASS | No new binding copy rules without approval |

**Specific checks:** Current assignee is issue-specific (not a third global role); E4 demonstrates that Lead C cannot change ISS-002 status while Member B is assignee. Resolved remains distinct from Closed, including both Resolved/High and Resolved/Critical in Important. The sample list excludes ISS-004 Critical/Closed and ISS-005 Not Set. No prohibited page-icon placeholders, row-selection checkboxes, bulk operations, new features, or login forms are visible **in supplied product frames**. Their absence from the entire live Figma file is **not independently verified**. Drawn disabled fields do not establish server permissions; timestamp display does not establish persistence.

**Non-UI/NFR exclusions from evidence PASS:** actual login/auth, HTTP(S)/TLS, backup restoration, actual response latency (<1s), server authorization, DB persistence, correct auto-generated timestamps and consistency under reload are **NOT VERIFIABLE** from screenshots and student-reported demo transitions. They must not be marked implementation PASS.

## B. UX review — evidence-backed observations (not user research)

1. **UX-01 — Medium, ambiguous status destination choice.** E4 renders `Closed or In Progress` in one input-like rectangle for Resolved. This can look like a single literal value or free-text input, despite two mutually exclusive legal targets. **Minimal correction:** render the two choices as distinct selectable options within the same approved Status control; retain adjacent Apply and unchanged transition set. Recheck in the final frame; issue is evidenced in the earlier screenshot.
2. **UX-02 — Low/Medium, selection affordance is visually weak.** E3/E6 Assignee and Priority appear as plain bordered fields without a visible dropdown/selection cue. A reviewer may mistake a single-select for editable text. **Minimal correction:** visually distinguish a single-choice control using native dropdown styling (no new product action); do not alter permissions.
3. **UX-03 — Medium, comment-validation path clarity needs live verification.** The Agent reported that clicking the **comment field** opens the empty-comment example. The intended violation is **submitting an empty comment** (AC-06.1), not merely focusing its field. **Observed evidence:** Agent statement only, NOT a verified live fault. **Minimal correction if reproduced:** trigger validation from **Add comment on empty input**, and keep focus in comment field non-error-producing. Record as conditional, not confirmed defect.
4. **UX-04 — Low, provenance/annotation readability.** E7 is a tall, dense reference panel with small source and transition notes. It is permitted to place notes outside product frames, but legibility at 100% zoom and for a reviewer is not established. **Minimal correction:** check normal-zoom legibility; increase note text size/spacing only if unreadable.

No accessibility certification or real-user usability testing was conducted.

## C. Defect / change recommendations for a human

| ID | Severity | Location | Source | Evidence | Minimal correction / disposition |
|---|---|---|---|---|---|
| **DEF-01** | **Major** | Earlier E6 `S-03 ISS-007`, Comments section | US-01 / D-09, sample new-issue state | E6 showed **two ISS-002 historical comments** inside newly created ISS-007. A previous assistant asked for removal, but the image still displayed them. It is unknown whether the final Agent-edited P1 file has them. | Inspect **current final ISS-007**. If inherited comments remain, remove them from *new-issue baseline* without removing the comment input; document actual correction and rescreenshot. **Status: OPEN — requires final verification.** |
| **UX-01** | Minor/Medium | E4 Resolved status chooser | BR-08.1 | Single `Closed or In Progress` value-like field | Render distinct choices within approved Status control; keep Apply. **Status: proposed** |
| **UX-02** | Minor | S-03 Assignee/Priority editors | D-06 / usability clarity | E3/E6 fields resemble free text | Clarify single-select visual cue, do not add workflow. **Status: proposed** |
| **UX-03** | Minor/Medium if reproduced | S-03 comment input | AC-06.1 | Agent report suggested clicking field opens empty-validation state; no live observation | In Present verify that validation occurs on **empty submission**, not mere field focus. **Status: needs reproduction** |
| **DEF-02** | Evidence gap | Final P1 version and final screenshot package | G6 verification method | Earlier F1 stills exist; no fresh final P1 screenshots or direct live Figma inspection | Capture legible final screenshots with Screen/State IDs, Figma version link, and signed manual test record; do not relabel as functional defect. **Status: OPEN evidence gap** |

### Verification and disposition procedure

The student reviews each row, accepts or rejects it with a reason, applies only accepted minimal corrections, and repeats the relevant Present/manual check. **No canvas changes were made by ChatGPT in this audit.** Until final screenshots confirm DEF-01 is absent or fixed, the evidence set is **not complete**.

## Final assessment

1. **UI design coverage: PARTIAL.** Most required visual states and source rules are shown, but a visible **ISS-007 inherited-comments contradiction (DEF-01)** requires a current-state check; some AC also require interactions/implementation not directly witnessed. Do **not** state that all 33 AC have passed.
2. **Prototype evidence: REPORTED.** The student reported working navigation, controls, four legal transitions, disabled restrictions, and comment examples after using Figma Present. The reviewer has **not** watched the final live prototype nor verified its current interaction bindings.
3. **Implementation tests outstanding:** authentication and server-side role checks, exact status transition authorization, field/enum validation, database creation/uniqueness/persistence, comment failure/no-save behavior, timestamp generation, actual dynamic Important filtering and reappearance/disappearance, data consistency after reopening, HTTPS/TLS, backup, and response time. These are not evidenced by Figma.
4. **Control B:** explicitly **SKIPPED**, not accepted/approved.

**Evidence requested to close G6:** current final P1 screenshots (legible S-02-A/B, M-01 and validation, S-03 ISS-002/ISS-007, reference role/status and comment states), demonstration test log with operator/date/expected/observed outcomes, final Figma version or share link with appropriate access, and human disposition of DEF-01/UX findings.
