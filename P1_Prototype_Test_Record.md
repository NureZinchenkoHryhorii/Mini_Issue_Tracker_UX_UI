# Mini Issue Tracker — P1 Prototype Test Record

**Артефакт:** `P1_Prototype_Test_Record.md`  
**Версія протоколу:** v1.0 — первинна систематизація наявних доказів, **2026-11-21**. Це дата складання документа, **не** дата кожного ручного тесту.  
**Прототип:** [Figma Design / P1](https://www.figma.com/design/S1oyc2GzQYRCKYfuuWnVf6/Untitled--Copy-?node-id=0-1)  
**Версія макета:** WORKING F1/P1, точний Figma revision/timestamp фінального стану не надано.  
**Команда:** **Григорій Зінченко та Тимофій Кадигроб**. За словами команди, обидва брали участь на всіх етапах. Спільний ChatGPT-діалог не встановлює, **хто саме** проводив окремий Present-тест.  
**Тестовий оператор:** для історичних повідомлених перевірок — **учасник команди, персонально не ідентифікований**; індивідуальний підпис ще не отримано.  
**Рецензент джерел:** ChatGPT порівняв методичку, звіт G6 і доступні зображення, **але не спостерігав final live Present**.  
**Підстава:** Методичні рекомендації, §21, с.22, T-01–T-10; §20, с.21 для Important test data; §22, с.23 щодо `Prototype + test record`. [Screen Contracts](03_Screen_Contracts_v1.0.md), [Screen Map](02_Screen_Map_v1.0.md), [Decision Log](Decision_Log_v0.1.md), [G6 Review](06_Review_Report.md), [Defect / Change Log](Defect_Change_Log.md).  

## 1. Мета й рівень доказовості

Мета — зафіксувати *що конкретно перевіряли* в P1, очікуваний стан і результат, не підміняючи статичний UI, прототип і реалізацію. Мова інтерфейсу Figma — англійська; записи протоколу — українською.

- **VISUAL EVIDENCE** — наданий раніше screenshot показує потрібний UI state. У [G6 Review](06_Review_Report.md) він ідентифікований як **E1–E8**; це **посилання на описи скриншотів**, не гарантовані PNG у GitHub.
- **STUDENT-REPORTED PASS** — учасник у спільному чаті сказав, що перевірив у Figma Present; це реальний звіт людини, але без ідентифікації конкретного оператора та без незалежного прямого replay.
- **UI EXAMPLE VISIBLE / INTERACTION NOT RECORDED** — відповідний error/default приклад намальовано, проте конкретного натискання в доступному протоколі немає.
- **PARTIAL / NOT VERIFIED** — потрібні додаткові дії чи доступ до актуальної версії. **AGENT REPORT не використано як доказ** працюючих connections.
- **Implementation NOT VERIFIED** — це wireframes / demo: без backend, login, DB persistence, реального server role enforcement, HTTPS/backup/performance. Статична disabled кнопка не доводить авторизацію.

**Умови запуску:** демо починається в уже authenticated контексті на S-02-A (не SSO/login). Ролі лише умовні: Member A, Member B, Lead C. У P1 використано prepared states і наперед визначені результати без реальної зміни набору даних. Current assignee належить конкретному issue.

## 2. Ручні тести T-01–T-10 (джерело: методичка, сторінка 22)

| Test / requirement | Source | Screen / State | Expected behavior | Actual observed / reported evidence | P1 test result | Remaining verification |
|---|---|---|---|---|---|---|
| T-01 — Create | US-01; D-04/D-09 | S-02-A/B → M-01 → S-03 ISS-007 | Заповнити лише Title і Description; Create показує нову заявку з ID, author, created_at, Status Open, Priority Not Set та Unassigned | G6 E3/E5/E6: показані поля й підготовлений стан ISS-007. Учасник повідомив проходження Create → ISS-007, Back. Пізніше скопійовані старі comments прибрано й повторно перевірено | STUDENT-REPORTED PASS для навігації та prepared state; UI частково видно | Немає незалежного live replay, автоматичної генерації ID, справжньої БД/часу або persistence |
| T-02 — Validation | AC-01.1–01.3; D-09 | M-01 / Title missing / Description missing | Порожні Title чи Description → помилка поряд із полем, **без** Create success і без нового issue | Два скриншоти Local components від 2026-11-21: порожній Title + `Title is required` і порожній Description + `Required field`; член команди підтвердив, що інтерактивна валідація у Present **не реалізована (обмеження симуляції)** | **VISUAL PASS / SIMULATION LIMITATION — STUDENT-REPORTED**; відсутній functional submit test | Не стверджувати, що Create реально блокується; можливий окремий runtime/server тест лише при реалізації |
| T-03 — Assignment | US-03 AC пп.1–4; D-04/D-05/D-06 | S-03 ISS-002 / REF permission matrix | Member не може призначати; Team Lead вибирає рівно одного члена команди → Apply; current assignee відображається | G6 E3/E4: disabled Member і enabled Lead; у чаті повідомлено, що Lead Assignee → Apply демонстрація працює | STUDENT-REPORTED PASS для Lead Apply; права лише візуальні | Перевірити final hotspot для Member/неassignee та UI-відображення нового assignee; реальне членство й server access поза прототипом |
| T-04 — Priority | US-04; BR-04/05/06; D-03/D-05/D-06 | S-03 ISS-002 / REF priority values | Member не змінює priority; Lead обирає лише Low/Normal/High/Critical → Apply; Not Set не selectable | G6 E4/E5: чотири опції та disabled Member; у чаті повідомлено, що Lead Priority → Apply працює | STUDENT-REPORTED PASS для demo Apply; UI options visible | Окремо повторити відмову Member, переконатися, що Not Set недоступний для встановлення; server check не перевірявся |
| T-05 — Status | US-07; BR-08.1; D-05/D-06 | REF legal-next states / P1 status examples | Дозволені тільки 4 переходи: Open→In Progress; In Progress→Resolved; Resolved→Closed; Resolved→In Progress. Решта між різними статусами — заборонена | G6 E4 показує матрицю. У чаті підтверджено проходження всіх 4 дозволених переходів і обмежень Closed. Після F1-UX-01 окремо повторно перевірено обидва виходи Resolved | STUDENT-REPORTED PASS для 4 legal transitions; exhaustive negative coverage NOT RECORDED | Перевірити всі інші заборонені різні статуси без успішних переходів; native demo не доводить persistence |
| T-06 — Lead restriction | AC-07.4; BR-08; D-05 | S-03 ISS-002 / REF Team Lead non-assignee | Lead, який **не** current assignee ISS-002, бачить disabled Status / Apply; Team Lead не обходить правило assignee | G6 E3/E4: canonical Lead C бачить ISS-002, assigned Member B, Status disabled; у чаті повідомлено, що обмеження перевірено в Present | STUDENT-REPORTED PASS; visual disabled evidence | Повторний контроль, що заборонений hotspot не спрацьовує; actual server authorization не перевірявся |
| T-07 — Comments | US-06 AC-06.1–06.5 | S-03 / empty validation / success / failed save | Empty → validation і 0 comments; success → text+author+time; failure → error і 0 нових saved entries | G6 E3/E5: три приклади. У чаті повідомлено, що Add comment success, empty і failure працюють. Окремо підтверджено, що фокус поля не викликає помилку сам по собі | STUDENT-REPORTED PASS для demo, три UI states visible | Новий запис має належати **тільки** своєму issue; серверне збереження, атомарність помилки й час не доведені |
| T-08 — Important | US-08; BR-09.1; D-01/D-07 | S-02-A All / S-02-B Important / S-02-C empty | Порівняти однакові issue IDs за predicate (High/Critical) AND status != Closed. Resolved залишається; Low/Normal/Not Set і всі Closed не входять | Використано **еквівалентний 6-issue dataset**, не 8-issue приклад методички: All ISS-001..ISS-006; Important ISS-001, ISS-002, ISS-003, ISS-006. E1/E2: ISS-003 High/Resolved і ISS-006 Critical/Resolved включені; ISS-004 Critical/Closed та ISS-005 Not Set виключені. У чаті повідомлено про роботу перемикання вкладок | STATIC PREDICATE VISUAL PASS — новий screenshot 2026-11-21; DYNAMIC FILTER NOT IMPLEMENTED/NOT VERIFIED | Окремо показати виключення Low/Normal на репрезентативних даних (у dataset їх немає) і демонстрацію зникнення issue після Resolved→Closed або чітко залишити це як несимульовану динаміку |
| T-09 — Navigation | US-02; D-01/D-07/D-09 | S-02-A/B ↔ S-03 ISS-002; S-02 → M-01 → ISS-007 | Відкрити issue зі списку, Back повертає початковий All/Important; Create відкриває overlay; Cancel без issue; успішний Create показує деталі нової заявки | У чаті студент повідомив PASS двох маршрутів: All→Important→ISS-002→Back→Important→Create→Cancel→Important та Important→Create→Create→ISS-007→Back→Important. Підтверджено в Present, не незалежним спостереженням | STUDENT-REPORTED PASS для вказаних маршрутів | Незалежний replay final P1 і screenshot конфігурації overlay/Back; backend-навігація/створення поза межами |
| T-10 — Scope | §8 release scope; D-01/D-02/D-08; G5 exclusions | Усі product frames та reference panels | Немає Delete, attachments, AI-функцій, change-history, непогодженого bulk control / checkbox, page icon placeholders та вигаданого login; notes зовні product UI | G6 E1–E7: заборонені product controls не видно в представлених кадрах; S-01 лише boundary, notes окремо. Повний актуальний canvas після фінальних правок не оглянуто незалежно | PARTIAL — supplied-image check only | Фінальний огляд усього Figma file, усіх product frames і Layers на предмет зайвих кнопок; зберегти evidence |

## 3. Звірка даних Important — **еквівалентний набір**, не зразок 8 issues

Методичка (§20, с.21) пропонує 8 записів, **або еквівалентні тестові дані**. У нашій Figma baseline **6 записів** (ISS-001–ISS-006), а `ISS-007` створюється як окремий ілюстративний результат Create, не як сьомий запис базового списку. Тому **не слід помилково очікувати** ISS-007 у фіксованому baseline Important цього прототипу.

| Issue у baseline | Status | Priority | Assignee | Expected Important | Підстава |
|---|---|---|---|---|---|
| ISS-001 | Open | Critical | Member A | YES | High/Critical, не Closed |
| ISS-002 | In Progress | High | Member B | YES | High/Critical, не Closed |
| ISS-003 | Resolved | High | Member A | YES | Resolved **не** Closed |
| ISS-004 | Closed | Critical | Member B | NO | Closed виключається завжди |
| ISS-005 | Open | Not Set | Unassigned | NO | Not Set не належить High/Critical |
| ISS-006 | Resolved | Critical | Member B | YES | Critical/Resolved включається |

**Expected Important baseline:** **ISS-001, ISS-002, ISS-003, ISS-006**. Це відповідає раніше наданому скриншоту S-02-B. **Відкритий evidence gap:** немає Low і Normal окремими issue у цьому baseline; live re-filter після Closed **не реалізовано** (за звітом Agent і описом демо), не заявляти його PASS.

## 4. Зведений результат і що саме протестовано

**Reported as working by a student in shared conversation:** позитивні Create/Cancel/Back маршрути (T-01, T-09); Lead Assignee / Priority Apply (T-03, T-04); **чотири дозволені статусні переходи** та обмеження Lead non-assignee / Closed (T-05, T-06); comment success, empty, failed-save приклади (T-07); All/Important navigation (частина T-08).

**Shown in earlier screenshots:** поля й порожні/error states, role/context matrix, status values, два empty-list states, six-row All та four-row Important baseline (T-01–T-08, T-10). Це **не** означає, що всі їхні interactions запущено.

**Немає достатнього підтвердження, щоб написати `10/10 PASS`:** T-02 (обидва validation UI states підтверджені; студент уточнив, що робочу інтерактивну валідацію у прототипі не реалізовано), T-05 (усі заборонені статусні переходи, крім перевірених прикладів), T-08 (Low/Normal і live filter), T-10 (огляд усього final canvas). У частини інших тестів зафіксоване **лише** student-reported виконання.

**Після G6-виправлень:** F1-DEF-01 (ISS-007 не успадковує коментарі ISS-002) та F1-UX-01 (два окремі варіанти після Resolved) мають **FIXED / RETEST PASS — STUDENT-REPORTED** у [журналі](Defect_Change_Log.md), але **нові screenshots фінального стану ще не надано**.

### Додатковий доказ T-02 — 2026-11-21

Учасник команди надав новий скриншот із **Local components** (файл, завантажений у спільний чат: `image(20261121-131811).png`). На ньому видно **порожній Title** і повідомлення **`Title is required`** під полем, тоді як Description заповнено. Це **VISUAL PASS для UI-прикладу missing-Title**, але **не** підтверджує роботу обробника Create або заборону переходу до ISS-007 при помилці. Другий новий скриншот із **Local components** (`image(20261121-132043).png`, завантажений у спільний чат) показує **заповнений Title**, **порожній Description** та текст **`Required field`** під ним. **Обидва required-field UI-приклади T-02 підтверджені зображеннями — VISUAL PASS.** Учасник команди **2026-11-21** уточнив: це **обмеження симуляції**, а не інтерактивно реалізована валідація в Present. Тому перевірка негативного Create-submit **не може бути позначена як виконана**; її відсутність не є новим дефектом вимог до статичного low-fi прототипу. Обидва PNG надані в чаті, але ще **не завантажені в GitHub**. Підсумок T-02: **VISUAL PASS / SIMULATION LIMITATION (student-reported)**, не повний functional PASS.

### Додатковий доказ T-08 — 2026-11-21

У спільний чат надано новий screenshot `image(20261121-133345).png` екрану **`S-02-B — Important`**. У таблиці прямо видно **ISS-001 Open/Critical, ISS-002 In Progress/High, ISS-003 Resolved/High, ISS-006 Resolved/Critical**; ISS-004 відсутній, тоді як у раніше наданому All screenshot він був **Closed/Critical**. Отже для **фіксованого 6-issue набору** inclusion/exclusion та `Resolved != Closed` отримали **VISUAL PASS**. Окремих Low/Normal записів у поточному baseline немає. **Динамічне переміщення issue після зміни status не реалізоване й не перевірене** — це симуляція. Скріншот надано в чаті, не завантажено в GitHub як файл. Особистий оператор у спільному чаті не визначений.

## 5. Граничні негативні сценарії для остаточної перевірки

| ID | Що потрібно натиснути у Present | Очікуваний результат | Поточний evidence |
|---|---|---|---|
| NEG-01 | M-01 → порожній Title → Create | Валідація Title, ISS-007 не відкривається | Підтверджено скриншотом `image(20261121-131811).png`; **інтеракція не реалізована, reported simulation limitation** |
| NEG-02 | M-01 → порожній Description → Create | Валідація Description, ISS-007 не відкривається | Підтверджено скриншотом `image(20261121-132043).png`; **інтеракція не реалізована, reported simulation limitation** |
| NEG-03 | Member non-assignee → Assignee/Priority Apply | Заборонені / disabled, жодних змін | Disabled у G6 E4; **hotspot окремо не підтверджений** |
| NEG-04 | Lead non-assignee ISS-002 → Status Apply | Disabled / без успішного переходу | Скриншот + student-reported check |
| NEG-05 | Closed → будь-який інший status | Відсутній наступний вибір / Apply disabled | Скриншот + student-reported check |
| NEG-06 | З різних current statuses спробувати інші незаконні переходи, окрім чотирьох дозволених | Жоден не показує success route | **повний exhaustive test не записаний** |
| NEG-07 | Empty comment → Add comment | Помилка, нуль нових comments | Student-reported check |
| NEG-08 | Failed comment save example | Error, старі коментарі лишаються, новий не доданий | Student-reported check |
| NEG-09 | Issue із High/Resolved → Closed → Important | Issue не повинен з'явитися в Important | Вихідне правило й статичні приклади є; **динамічний demo після зміни не підтверджено** |
| NEG-10 | Огляд усіх product frames / layers | Немає зайвих Delete/AI/attachment/bulk дій і page placeholders | Частина старих screenshot перевірена; **цілий final file — не перевірений** |

## 6. Короткий тест з одногрупником без підказок (методичка, с.22)

У методичці окремо запропоновано мінітест: (1) створити заявку, (2) знайти Important + Resolved, (3) пояснити неможливість зміни status неуповноваженим користувачем.

**Стан: NOT RECORDED AS AN INDEPENDENT UNPROMPTED TEST.** Обидва учасники виконували спільну роботу, але відсутній запис конкретного окремого проходження **без підказок** з маршрутом, місцями вагання та незрозумілими написами. Не заднім числом приписувати його Тимофію або Григорію. За бажанням додати фактичний запис після проведення.

## 7. Поля остаточного підпису й evidence pack

| Field | Стан |
|---|---|
| **Хто реально запускав історичні P1 тести** | Учасник спільного діалогу — особа **не ідентифікована**; жодної персональної заяви не додано |
| **Григорій Зінченко — особисте підтвердження сценарію** | PENDING — потрібен реальний приклад і дата; не вигадувати |
| **Тимофій Кадигроб — особисте підтвердження сценарію** | PENDING — потрібен реальний приклад і дата; не вигадувати |
| **Фінальна Figma revision/date** | NOT PROVIDED |
| **Post-fix screenshot (ISS-007 empty Comments)** | NOT PROVIDED |
| **Post-fix screenshot (Resolved distinct choices)** | NOT PROVIDED |
| **P1 direct screen-recording / independent reviewer** | NOT PROVIDED |
| **Доступ викладача до Figma** | Link available; фактичне право доступу викладача ще не перевірене |
| **Control B** | SKIPPED by team choice; **не** independent approval |
| **Overall outcome** | **P1 core scenarios STUDENT-REPORTED PASS; T-02 validation UI states VISUAL PASS but interaction simulation-only; full T-01–T-10 coverage PARTIAL; implementation tests NOT VERIFIED** |

**Порядок закриття:** пройти непротестовані негативні сценарії; записати фактичного оператора і дату; зробити скриншоти актуальних post-fix states; зазначити остаточну версію Figma; оновити [G6 Review](06_Review_Report.md) і [Defect / Change Log](Defect_Change_Log.md) лише після отримання доказів. Не робити вигляд, що симуляція є real persistence.
