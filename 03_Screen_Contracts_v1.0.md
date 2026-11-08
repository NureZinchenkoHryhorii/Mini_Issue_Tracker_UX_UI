# Mini Issue Tracker — Developer-Verifiable Screen Contracts

**Файл:** `03_Screen_Contracts_v1.0.md`  
**Версія:** v1.0  
**Статус:** REVIEW / NOT APPROVED; developer-verifiable контракт підготовлено, але макет, прототип і реалізацію ще не тестували; жоден TEST не має статусу PASS.  
**Джерела:** S1 — `SD_Spec.docx.pdf`, §§1/3/5/8; `01_Input_Pack_v1.0.md` (REVIEW); `02_Screen_Map_v1.0.md` (REVIEW); `Decision_Log_v0.1.md`.  
**Межі:** Release MVP — US-01–US-08; US-09 Deferred, SR-10/SR-11 Future. Документ є контрактом для майбутніх макетів і реалізації, а не доказом уже створеного інтерфейсу.

## 0. Статуси доказів і UX-рішень

- `SOURCE` = оригінальні правила S1; `DERIVED` = логічний висновок, обґрунтований S1; `APPROVED D-01` = підтверджений 2026-11-08 вибір desktop grayscale low-fi, один список All/Important та Create modal.
- `APPROVED D-01`…`D-08` = погоджені UX-рішення з методички; `APPROVED D-09` = окремо погоджений маршрут Q-11: успішний Create → S-03 саме новоствореного issue (2026-11-08). Це **UX-рішення, не SOURCE S1**. `PROPOSED D-10` = ще не погоджене уточнення способу зворотного зв'язку/валідації там, де S1 не встановлює точний текст.
- `M` = перевіряється статичним макетом (наявність, вигляд, приклади станів). `P` = перевіряється клікабельним прототипом/сценарієм (симуляція послідовності). `I` = доводиться тільки реалізацією/інтеграційними перевірками (права на сервері, створення й збереження в БД, timestamps, захист, HTTPS, backup, performance).
- `НЕ ВИКОНАНО` = тест специфіковано, але результат невідомий; не підмінювати це `PASS`.
- Assignee — зв'язок **поточного користувача з конкретним issue**, а не глобальна роль. Відсутність assignee не надає права змінювати status жодному користувачу.
- `S-01` — placeholder межі автентифікації, `S-02` — один екран списку (All/Important/Empty — стани), `M-01` — modal, `S-03` — один екран деталей. Assignment/Priority/Status/Comments — області S-03, не окремі screens.
- `D-04` (Unassigned та перепризначення), `D-06` (окрема Apply), `D-07` (повернення до попередньої вкладки), `D-08` (демодані), `D-09` (після Create → S-03) **погоджені**. Зміст SOURCE від цього не змінюється.

## 1. Загальні правила даних і подання

| Поле | Обов'язковість/сутність | Вигляд за відсутності | Правило |
|---|---|---|---|
| Issue ID | Генерується системою при створенні; потрібне у списку і деталях | Для успішно створеного issue відсутність неприпустима; текст помилки не визначений | AC-01.4, AC-02.2/02.4 |
| Title | Обов'язковий при Create; потрібен у списку та деталях | У формі порожнє значення → помилка `Title is required` за Gherkin; запис не створюється | AC-01.1/01.2 |
| Description | Обов'язковий при Create, показаний у деталях | У формі порожнє значення → валідація, без створення; точний текст не визначений | AC-01.1/01.3 |
| Status | Open на Create, одне з Open/In Progress/Resolved/Closed | У створеного issue не може бути відсутнім; недопустимі значення заборонені | BR-03/07; AC-07.1/07.2/07.5 |
| Priority | При Create відсутній; після встановлення лише Low/Normal/High/Critical | Відображати `Not Set` — APPROVED D-03; це відсутність priority, а не п'ятий рівень | BR-04/05; AC-01.5/04.1 |
| Assignee | Необов'язковий до призначення; максимум один, лише член команди | Не показувати вигадану людину; початковий стан `Unassigned` — APPROVED D-04; конкретний напис `Не призначено` — PROPOSED D-10, не SOURCE | AC-02.2/02.4, US-03 AC п.1–4 |
| Author | Автоматично записується під час Create; потрібен у деталях | Відсутність у створеного issue порушує AC | AC-01.4, AC-02.4 |
| Created at | Автоматичне поле issue; потрібне у деталях | Відсутність порушує AC; формат/таймзона Q-06 | AC-01.4, AC-02.4 |
| Comment text | Непорожнє, вводить користувач | Не створювати порожній comment; точне повідомлення не задано | AC-06.1 |
| Comment author | Для кожного успішно збереженого comment | Відсутність порушує AC | AC-06.3 |
| Comment creation time | Для кожного успішно збереженого comment | Відсутність порушує AC; формат Q-06 | AC-06.4 |

**Create:** user input = лише `Title` і `Description`. System generated = `ID`, `status = Open`, `created_at`, `author`, `priority = Not Set`. Початковий assignee — **Unassigned (APPROVED D-04; Q-02 вирішено)**. Додавати controls для priority/assignee в Create як PRODUCT SOURCE заборонено.

**Important predicate (точно):** `priority ∈ {High, Critical} AND status != Closed`. Перевірні приклади: `High + Resolved → включено`; `Critical + Closed → виключено`; `Priority = Not Set → виключено`. Не створюється друга БД або незалежний список, це вкладка-фільтр одного S-02 (SOURCE BR-09/09.1; AC-08.1–08.4; APPROVED D-01).

## 2. Контракти поверхонь та станів

### S-01 — Межа автентифікації

| Атрибут | Контракт |
|---|---|
| ID / призначення | S-01; документувати, що доступ до системи мають лише автентифіковані члени команди |
| Actors | Team Member, Team Lead лише після автентифікації |
| Entry | Початок без підтвердженого контексту або пояснювальний старт демонстрації |
| Visible data | Службовий підпис про межу доступу — **APPROVED D-02**, не обов'язкове поле S1 |
| Відсутні значення | Немає визначених S1 полів login/password |
| Default / empty | S-01 placeholder, не інтерактивна форма авторизації |
| Validation / error | Не визначено в S1; не моделювати недоведені authentication errors |
| Incoming / outgoing | Пояснювальна початкова точка; T-01 → S-02-A **лише якщо автентифіковано**, без вигаданого login-кроку |
| Перевірка | M: placeholder без вигаданих полів; P: старт симуляції з авторизованого контексту — APPROVED D-02/D-08; I: фактична автентифікація, права та NFR-02 |

| C-ID | Label / type | Visible / enabled | Trigger → результат | Джерело |
|---|---|---|---|---|
| C-01 | Authentication boundary / non-interactive annotation | Видимий лише у варіанті S-01; не є активною кнопкою | Немає реальної дії | BR-01; APPROVED D-02 |

### S-02 — Список issues (спільна оболонка)

| Атрибут | Контракт |
|---|---|
| ID / призначення | S-02; показати issues та відкрити S-03 / M-01 |
| Actors / entry | Обидві ролі, лише автентифіковані; T-01, T-03, T-22, T-23 |
| Visible data | На кожному рядку обов'язкові ID, Title, Status, Priority; Assignee за наявності (AC-02.2); відсутній priority семантично Not Set; assignee без призначення не вигадувати |
| Default | Вкладка All як стартова точка демонстрації — модель G2; окремий початковий tab у S1 не визначений |
| Empty / validation / error | S-02-C залежно від фільтра; S1 не задає помилки завантаження списку чи їхній текст |
| Incoming / outgoing | T-01/T-03/T-22/T-23 → S-02; T-02/T-03 перемикають вкладки; T-04/T-05 → S-03; T-06/T-07 → M-01; T-24/T-25 → S-02-C |
| Перевірка | M: рядки, вкладки, поля, empty; P: перемикання та відкриття; I: реальне отримання спільного набору й коректна фільтрація |

| C-ID | Label / type | Visible / enabled | Trigger → результат | Джерело |
|---|---|---|---|---|
| C-02 | All Issues / tab | В обох ролей; enabled після auth | T-03 → той самий список без Important-фільтра | US-02; APPROVED D-01 |
| C-03 | Important Issues / tab | В обох ролей; enabled після auth | T-02 → `(High or Critical) AND not Closed` | US-08, BR-09/09.1; APPROVED D-01 |
| C-04 | Рядок issue / navigational item | Лише для видимого існуючого issue; enabled після auth | T-04/T-05 → S-03 конкретного issue | AC-02.3 |
| C-05 | Create Issue / button | Обидві ролі; enabled після auth | T-06/T-07 → M-01 | BR-02; APPROVED D-01 |

### S-02-A — All

| Атрибут | Контракт |
|---|---|
| ID / призначення | S-02-A; список усіх зареєстрованих issues |
| Actors / entry | Обидві ролі; T-01/T-03/T-22 |
| Visible data | ID/Title/Status/Priority кожного issue, Assignee за наявності; поля обов'язкові згідно AC-02.2 |
| Відсутні значення | Priority Not Set як відсутність; Assignee без призначення не вигадувати |
| Default / empty | Відображається загальний набір; якщо нуль issues → S-02-C (All) |
| Validation / error | Немає полів введення; помилки отримання S1 не описує |
| Incoming / outgoing | T-01/T-03/T-22; T-02 → Important, T-04 → S-03, T-06 → M-01, T-24 → Empty |
| Controls | C-02/C-03/C-04/C-05 із S-02 |
| Перевірка | M: повнота рядка й empty; P: відкриття; I: фактичні дані та актуальність списку |

### S-02-B — Important

| Атрибут | Контракт |
|---|---|
| ID / призначення | S-02-B; фільтр спільного S-02, не окремий ресурс |
| Actors / entry | Обидві ролі; T-02/T-23 |
| Visible data | Ті самі поля, що S-02-A; лише issues за predicate `priority ∈ {High, Critical} AND status != Closed` |
| Відсутні значення | Not Set/Low/Normal та будь-який Closed не відображаються |
| Default / empty | Якщо немає відповідних issues → S-02-C (Important); All може водночас бути непорожнім |
| Validation / error | Відбір не створює issue; не визначені додаткові помилки |
| Incoming / outgoing | T-02/T-23; T-03 → All, T-05 → S-03, T-07 → M-01, T-25 → Empty |
| Controls | C-02/C-03/C-04/C-05; C-03 активна вкладка |
| Перевірка | M: `High+Resolved` присутній, `Critical+Closed` та Not Set відсутні; P: перемикання; I: один data source і predicate |

### S-02-C — Empty

| Атрибут | Контракт |
|---|---|
| ID / призначення | S-02-C; порожній стан поточної вкладки S-02, не окрема сторінка |
| Actors / entry | Обидві ролі; T-24 (All) або T-25 (Important) |
| Visible data | Текстова ознака відсутності issues; точний текст — PROPOSED D-10. Системних полів issue у порожньому рядку немає |
| Відсутні значення | Нуль rows, не placeholder-фальшивий issue |
| Default / empty | All: немає зареєстрованих issues; Important: існують/не існують загальні issues, але жоден не задовольняє predicate |
| Validation / error | Empty — нормальний стан, не error |
| Incoming / outgoing | T-24/T-25; C-02/C-03 повертають до відповідної вкладки, C-05 відкриває M-01 (поточну вкладку зберігати — APPROVED D-07) |
| Controls | C-02/C-03/C-05 зі спільної оболонки |
| Перевірка | M: окремі приклади Empty All/Empty Important; P: перемикання; I: запит набору та фільтра |

### M-01 — Модальне створення issue

| Атрибут | Контракт |
|---|---|
| ID / призначення | M-01; прийняти обов'язкові Title/Description та створити issue; modal — APPROVED D-01 |
| Actors / entry | Будь-який автентифікований Team Member/Lead; T-06/T-07 із S-02 |
| Visible data | **User inputs:** Title (required), Description (required). **System-generated after success:** ID, Author, Created at, Status Open, Priority unset |
| Відсутні значення | Title або Description порожні → issue не створено; поля system-generated до успіху не є user inputs; Assignee default Unassigned (APPROVED D-04) |
| Default | Порожні Title/Description; немає UI-контролів для вибору status/priority/assignee під час Create |
| Empty / validation | Title порожній → `Title is required` (Gherkin S1); Description порожній → validation без створення; точний текст не задано |
| Error | Текст системної помилки Create у S1 не встановлено; за фактичного невдалого збереження не оголошувати створення успішним (поведінка поза конкретним AC, перевіряти реалізацією) |
| Incoming / outgoing | T-06/T-07 → M-01; T-08 Cancel → попередня вкладка без нового issue; T-09 лише при успішному Create → **S-03 саме новоствореного issue** (APPROVED D-09) |
| Перевірка | M: тільки 2 поля, валідаційні приклади, Cancel, стан S-03 нового issue; P: Cancel/required/симуляція T-09 → S-03 з тим самим створеним ID; I: реальне створення, ID/author/time, atomicity та відсутність запису після Cancel/validation |

| C-ID | Label / type | Visible / enabled | Trigger → результат | Джерело |
|---|---|---|---|---|
| C-06 | Title / single-line text input | Видимий усім auth; required | Введення Title | AC-01.1/01.2 |
| C-07 | Description / multiline text input | Видимий усім auth; required | Введення Description | AC-01.1/01.3 |
| C-08 | Create / submit button | Видимий усім auth; форма може бути submitted, але валідатор не пропускає відсутні required | T-09: лише після успішного створення → S-03 нового issue; статус Open, priority unset | BR-02/03/04; AC-01.1–01.5; APPROVED D-09 / Q-11 |
| C-09 | Cancel / button | Видимий усім auth | T-08 → закриття modal, **без створення issue** | G2, UX modal APPROVED D-01; не нова SOURCE-вимога |
| C-10 | Validation error / inline text | Лише при невалідній формі; не є кнопкою | Показати `Title is required` або Description required без створення | AC-01.2/01.3; Gherkin для Title; PROPOSED D-10 для решти текстів |

### S-03 — Деталі issue

| Атрибут | Контракт |
|---|---|
| ID / призначення | S-03; перегляд одного issue, коментарі та всі дозволені дії керування без нових сторінок |
| Actors / entry | Обидві ролі після auth; T-04 (з All), T-05 (з Important), **T-09 після успішного Create — саме новостворений issue** |
| Visible data | ID, Title, Description, Status, Priority, Author, Created at — потрібні; Assignee якщо призначений; Comments: body + author + creation date/time на кожному записі |
| Відсутні значення | Priority unset = Not Set (семантика SOURCE, текст APPROVED D-03); Assignee Unassigned не підмінювати людиною (APPROVED D-04); comments можуть бути порожнім набором, точний напис не задано; створений issue не має бути без ID/Author/Created at |
| Default | Read-only details для всіх; control permission залежить від глобальної ролі та поточного assignee, а не тільки Team Lead |
| Empty / validation | Порожній comment не зберігається; недопустиме значення priority/status не приймається; Closed не має status переходів |
| Error | Failed comment save: повідомлення про помилку, **без створеного comment**; точний текст Q-05. Не-assignee/Member не змінюють заборонені дані |
| Incoming / outgoing | T-04/T-05 → S-03; T-10–T-21 змінюють/не змінюють дані **без переходу до іншого screen**; T-22/T-23 → попередня вкладка **APPROVED D-07** |
| Перевірка | M: усі required поля, стани control, author/time comments, permission examples; P: демонстрація T-10–21/повернення, але лише імітація; I: справжні права, збереження, валідні status, consistency списку, comment transaction |

| C-ID | Label / type | Visible / enabled | Trigger → результат | Джерело |
|---|---|---|---|---|
| C-11 | Assignee / single-select team-member control | Видимий стан assignee; **редагування enabled тільки Team Lead**, для Member значення видно, але control = disabled (APPROVED D-05) | T-10 → один team member, зберігається й показується; при Member T-11 → немає переходу | US-03 AC п.1–4; APPROVED D-04/D-05/D-06 |
| C-12 | Priority / single-select control | Поточне значення видиме всім; change enabled **лише Team Lead** | T-12 → Low/Normal/High/Critical, залишається S-03; Member T-13 нічого не змінює | BR-05/06; AC-04.1/04.2; APPROVED D-03/D-05/D-06 |
| C-13 | Status / single-select allowed-next-status control | Статус видно всім; enabled лише коли user = current assignee **та** з поточного status є дозволений наступний; при Closed нікому | T-14–T-17; T-18/T-19 без виконаного переходу | BR-07/08/08.1; AC-07.1–07.5; APPROVED D-05/D-06 |
| C-14 | Comment text / multiline input | Для будь-якого auth user; введення дозволено | Ввести непорожній текст | AC-06.1 |
| C-15 | Add comment / submit button | Для auth user; фактичний save лише при непорожньому body | T-20 success → запис body/author/time; T-21 failure → error і **жодного нового comment** | AC-06.1–06.5 |
| C-16 | Back to Issues / navigation button | Для auth user; повернення до попередньої вкладки — APPROVED D-07 | T-22 → All, T-23 → Important, обидва з актуальною фільтрацією | AC-02.3; APPROVED D-07 |
| C-17 | Change confirmation / per-field Apply | Видимий біля кожного C-11/C-12/C-13; enabled лише якщо відповідний користувач має право, є дозволене вибране нове значення; APPROVED D-06 | Підтверджує обраний assignee/priority/status без нової сторінки | APPROVED D-06, не SOURCE |
| C-18 | Comment save error / message | Лише при failed save, не інтерактивний | Залишає S-03; не додає comment до списку | AC-06.5; Q-05 |


## 3. Матриця дозволів — чотири контексти

**Так** = дія дозволена лише за загальних передумов (auth, валідні дані тощо). **Так, якщо дозволений перехід** для status завжди вимагає BR-08.1. **Ні** = дія не повинна змінювати дані чи створювати navigation side effect.

| Дія | Team Member не-assignee | Team Member assignee | Team Lead не-assignee | Team Lead assignee | Джерело |
|---|---|---|---|---|---|
| View issue/list | Так | Так | Так | Так | BR-01; AC-02.1–02.4 |
| Create issue | Так | Так | Так | Так | BR-02; US-01 |
| Comment | Так | Так | Так | Так | US-06 |
| Assign assignee | Ні | Ні | Так | Так | US-03, AC, пункт 3 |
| Change priority | Ні | Ні | Так | Так | BR-06; AC-04.2 |
| Change status | Ні | Так, якщо дозволений перехід | Ні | Так, якщо дозволений перехід | BR-08/08.1; AC-07.4 |

**Примітки до перевірки:** Team Lead не отримує автоматичного права на status. Якщо assignee відсутній, ні Lead, ні Member не можуть змінювати status. Closed не має дозволених вихідних status transitions навіть для assignee. Дозвіл assign і priority стосується ролі, а не зв'язку assignee. Видимий disabled control не доводить backend authorization (M/P ≠ I).

## 4. Повна матриця status transitions

| Поточний \ цільовий | Open | In Progress | Resolved | Closed |
|---|---|---|---|---|
| **Open** | Поточний стан, не перехід | **ДОЗВОЛЕНО** T-14 | ЗАБОРОНЕНО T-19 | ЗАБОРОНЕНО T-19 |
| **In Progress** | ЗАБОРОНЕНО T-19 | Поточний стан, не перехід | **ДОЗВОЛЕНО** T-15 | ЗАБОРОНЕНО T-19 |
| **Resolved** | ЗАБОРОНЕНО T-19 | **ДОЗВОЛЕНО** T-17 | Поточний стан, не перехід | **ДОЗВОЛЕНО** T-16 |
| **Closed** | ЗАБОРОНЕНО T-19 | ЗАБОРОНЕНО T-19 | ЗАБОРОНЕНО T-19 | Поточний стан, не перехід |

**Перевірні передумови:** автентифікований current user = current assignee; from-status відповідає поточному значенню; to-status із дозволеної клітинки. При порушенні actor condition — T-18 (жодної зміни), при порушенні transition condition — T-19 (жодної зміни). `Closed` забороняє тільки вихідні **status** transitions; нової глобальної заборони comment або priority для Closed тут немає. Джерело BR-07/08/08.1, AC-07.2/07.4/07.5.

## 5. Перелік T-ID для вхідних/вихідних маршрутів

| T-ID | Звідки → куди/ефект | Перевірна умова |
|---|---|---|
| T-01 | S-01 → S-02-A | Лише за наявності автентифікованого контексту (без вигаданого login) |
| T-02 / T-03 | All ↔ Important у S-02 | Вкладки одного списку; Empty якщо немає відповідних rows |
| T-04 / T-05 | S-02-A/B → S-03 | Відкрити вибраний існуючий issue |
| T-06 / T-07 | S-02-A/B → M-01 | Лише auth user; відкрити modal |
| T-08 | M-01 → вкладка, звідки відкрили | Cancel не створює issue |
| T-09 | M-01 → S-03 нового issue (APPROVED D-09) | Лише успішний Create; S-03 показує саме новий ID, author/created_at, Open, Not Set; невдала валідація не запускає T-09 |
| T-10 / T-11 | S-03 → S-03 / без зміни | Lead вибирає одного team member → Apply; Member не може |
| T-12 / T-13 | S-03 → S-03 / без зміни | Lead вибирає рівень → Apply; Member не може; немає settings page |
| T-14–T-17 | S-03 → S-03 | Вибір next status → Apply; 4 валідні зміни, тільки assignee |
| T-18 / T-19 | S-03 → без переходу | Не-assignee або недопустимий status transition — жодної зміни |
| T-20 / T-21 | S-03 → S-03 | Comment success з author/time або failed save без запису |
| T-22 / T-23 | S-03 → All/Important | Збереження попередньої вкладки — APPROVED D-07; фільтр повторно застосовується |
| T-24 / T-25 | All/Important → S-02-C | Empty відповідного режиму, а не нова сторінка |

## 6. Traceability — 33 Acceptance Criteria

**Формат:** `Source ID/пункт | UIR-ID | Screen/State | C-ID або annotation | Test ID | Verification level`. UIR-ID та Test ID — **локальні ID цього документа**, їх не можна видавати за оригінальні S1 AC-ID. Позначення `M/P/I` означають лише потенційні рівні верифікації, **не результат тесту**.
### US-01 — 5 критеріїв

| Source ID/пункт | UIR-ID | Screen/State | C-ID або annotation | Test ID | Verification level |
|---|---|---|---|---|---|
| AC-01.1 | UIR-01.1 | M-01 | C-06/C-07 | TEST-01.1 | M/P |
| AC-01.2 | UIR-01.2 | M-01 | C-06/C-08/C-10 | TEST-01.2 | M/P/I |
| AC-01.3 | UIR-01.3 | M-01 | C-07/C-08/C-10 | TEST-01.3 | M/P/I |
| AC-01.4 | UIR-01.4 | M-01 → S-03 нового issue (D-09) | C-08/ANNOT-CREATE | TEST-01.4 | M/P/I |
| AC-01.5 | UIR-01.5 | M-01/S-03 | ANNOT-PRIORITY/C-12 | TEST-01.5 | M/P/I |

### US-02 — 5 критеріїв

| Source ID/пункт | UIR-ID | Screen/State | C-ID або annotation | Test ID | Verification level |
|---|---|---|---|---|---|
| AC-02.1 | UIR-02.1 | S-02-A | C-02/ANNOT-LIST | TEST-02.1 | M/P/I |
| AC-02.2 | UIR-02.2 | S-02-A/S-02-B | C-04/ANNOT-ROW | TEST-02.2 | M/I |
| AC-02.3 | UIR-02.3 | S-02-A → S-03 | C-04 | TEST-02.3 | M/P |
| AC-02.4 | UIR-02.4 | S-03 | ANNOT-DETAILS | TEST-02.4 | M/I |
| AC-02.5 | UIR-02.5 | S-02-C (All) | ANNOT-EMPTY | TEST-02.5 | M/P/I |

### US-03 — 4 критеріїв

| Source ID/пункт | UIR-ID | Screen/State | C-ID або annotation | Test ID | Verification level |
|---|---|---|---|---|---|
| US-03, AC, пункт 1 | UIR-03.1 | S-03 | C-11 | TEST-03.1 | M/P/I |
| US-03, AC, пункт 2 | UIR-03.2 | S-03 | C-11 | TEST-03.2 | M/P/I |
| US-03, AC, пункт 3 | UIR-03.3 | S-03 | C-11/ANNOT-PERMISSIONS | TEST-03.3 | M/P/I |
| US-03, AC, пункт 4 | UIR-03.4 | S-03/S-02 | ANNOT-ASSIGNEE | TEST-03.4 | M/P/I |

### US-04 — 2 критеріїв

| Source ID/пункт | UIR-ID | Screen/State | C-ID або annotation | Test ID | Verification level |
|---|---|---|---|---|---|
| AC-04.1 | UIR-04.1 | S-03 | C-12 | TEST-04.1 | M/P/I |
| AC-04.2 | UIR-04.2 | S-03 | C-12/ANNOT-PERMISSIONS | TEST-04.2 | M/P/I |

### US-05 — 3 критеріїв

| Source ID/пункт | UIR-ID | Screen/State | C-ID або annotation | Test ID | Verification level |
|---|---|---|---|---|---|
| AC-05.1 | UIR-05.1 | S-02/S-03 | ANNOT-STATUS | TEST-05.1 | M/I |
| AC-05.2 | UIR-05.2 | S-03 | ANNOT-DETAILS/C-13 | TEST-05.2 | M/I |
| AC-05.3 | UIR-05.3 | S-02-A/S-02-B | ANNOT-ROW | TEST-05.3 | M/I |

### US-06 — 5 критеріїв

| Source ID/пункт | UIR-ID | Screen/State | C-ID або annotation | Test ID | Verification level |
|---|---|---|---|---|---|
| AC-06.1 | UIR-06.1 | S-03 | C-14/C-15 | TEST-06.1 | M/P/I |
| AC-06.2 | UIR-06.2 | S-03 | C-14/C-15 | TEST-06.2 | M/P/I |
| AC-06.3 | UIR-06.3 | S-03 | ANNOT-COMMENTS | TEST-06.3 | M/I |
| AC-06.4 | UIR-06.4 | S-03 | ANNOT-COMMENTS | TEST-06.4 | M/I |
| AC-06.5 | UIR-06.5 | S-03 error | C-18/C-15 | TEST-06.5 | M/P/I |

### US-07 — 5 критеріїв

| Source ID/пункт | UIR-ID | Screen/State | C-ID або annotation | Test ID | Verification level |
|---|---|---|---|---|---|
| AC-07.1 | UIR-07.1 | M-01/S-03 | C-08/ANNOT-STATUS | TEST-07.1 | M/P/I |
| AC-07.2 | UIR-07.2 | S-03 | C-13/ANNOT-STATUS-MATRIX | TEST-07.2 | M/I |
| AC-07.3 | UIR-07.3 | S-03/S-02 | C-13/ANNOT-STATUS | TEST-07.3 | M/P/I |
| AC-07.4 | UIR-07.4 | S-03 | C-13/ANNOT-PERMISSIONS | TEST-07.4 | M/P/I |
| AC-07.5 | UIR-07.5 | S-03 | C-13/ANNOT-STATUS-MATRIX | TEST-07.5 | M/P/I |

### US-08 — 4 критеріїв

| Source ID/пункт | UIR-ID | Screen/State | C-ID або annotation | Test ID | Verification level |
|---|---|---|---|---|---|
| AC-08.1 | UIR-08.1 | S-02-B | C-03/ANNOT-IMPORTANT | TEST-08.1 | M/P/I |
| AC-08.2 | UIR-08.2 | S-02-B | C-03/ANNOT-IMPORTANT | TEST-08.2 | M/P/I |
| AC-08.3 | UIR-08.3 | S-02-B | C-03/ANNOT-IMPORTANT | TEST-08.3 | M/P/I |
| AC-08.4 | UIR-08.4 | S-02-B | C-03/ANNOT-IMPORTANT | TEST-08.4 | M/P/I |

## 7. Тестові сценарії — актор, передумови, дія, результат та межа доказу

Кожен `TEST-xx.y` пов'язаний рівно з одним рядком Traceability (для перехресних перевірок можливе повторне використання даних). **Усі тести: NOT RUN; PASS не встановлено.**

| Test ID | Actor/context | Передумови | Дія | Очікуваний видимий результат | Що НЕ доводить тест макета/прототипу |
|---|---|---|---|---|---|
| TEST-01.1 | Auth Member | M-01 відкрита | Увести Title і Description | Обидва поля доступні, дані відображаються | Збереження в БД |
| TEST-01.2 | Auth Member | Title порожній | Натиснути Create | Issue не створюється; приклад помилки `Title is required` | Server validation і відсутність запису |
| TEST-01.3 | Auth Member | Description порожній | Натиснути Create | Валідація required; результат створення відсутній; текст TBD | Server validation і відсутність запису |
| TEST-01.4 | Auth Member | Title і Description валідні | Успішно Create | S-03 показує саме новий issue, ID, status Open, author, created_at (APPROVED D-09) | Справжнє генерування/збереження/точний час |
| TEST-01.5 | Auth Member | Новий issue | Create | Priority не встановлено, не Normal | Значення в БД |
| TEST-02.1 | Auth Member | Є зареєстровані issues | Відкрити список | Видно список зареєстрованих issues | Фактичні результати запиту й доступ |
| TEST-02.2 | Auth Member | Є issue з assignee та без | Переглянути рядки | ID, Title, Status, Priority; Assignee за наявності | Актуальність даних |
| TEST-02.3 | Auth Member | Є видимий issue | Вибрати рядок | Відкриваються деталі саме вибраного issue | Роботу маршрутизації застосунку |
| TEST-02.4 | Auth Member | Відкритий issue | Переглянути поля | ID/Title/Description/Status/Priority/Assignee за наявності/Author/Created at | Завантаження фактичних записів |
| TEST-02.5 | Auth Member | Зареєстрованих issues 0 | Відкрити All | Порожній список / повідомлення | Чи дійсно набір порожній |
| TEST-03.1 | Lead | Відкритий issue; доступний C-11 | Вибрати одного team member → C-17 Apply | Зберігається лише один assignee, він показаний у S-03 | Constraint cardinality у БД |
| TEST-03.2 | Lead | Є predefined team members | Відкрити варіанти | Обрати можна тільки члена команди | Перевірку membership на сервері |
| TEST-03.3 | Member + Lead | Один і той самий issue | Member бачить disabled C-11/Apply; Lead вибирає assignee → Apply | Member не змінює assignee; Lead після success змінює | Server authorization |
| TEST-03.4 | Auth Member | Issue має assignee | Переглянути поточного | Поточний assignee видимий | Актуальне збережене значення |
| TEST-04.1 | Lead | Контрол priority доступний | Відкрити вибір | Тільки Low, Normal, High, Critical; Not Set — відсутнє значення | Серверне обмеження enum |
| TEST-04.2 | Member + Lead | Той самий issue | Member бачить disabled C-12/Apply; Lead вибирає допустимий priority → Apply | Member не змінює; Lead після success змінює | Server authorization |
| TEST-05.1 | Auth Member | Набір issues | Оглянути status кожного | Кожен issue показує поточний status | Чи status актуальний |
| TEST-05.2 | Auth Member | Issue відкритий | Переглянути S-03 | Поточний status видимий | Чи відповідає БД |
| TEST-05.3 | Auth Member | Є рядки issue | Оглянути список | Status видно в кожному рядку | Чи відповідає БД |
| TEST-06.1 | Auth Member | Порожнє поле comment | Submit | Коментар не додано; валідація | Server validation |
| TEST-06.2 | Auth Member | Непорожній comment; save success | Submit | Новий comment видно під issue | Запис у БД і повторне читання |
| TEST-06.3 | Auth Member | Є успішний comment | Переглянути | У коментарі видно автора | Ідентичність записаного author |
| TEST-06.4 | Auth Member | Є успішний comment | Переглянути | Видно дату/час створення | Час у БД і timezone |
| TEST-06.5 | Auth Member | Непорожній comment; симульована помилка save | Submit | Показано error, новий comment відсутній | Транзакційність і реальний failure handling |
| TEST-07.1 | Auth Member | Створюється issue | Create | Початковий status Open | Початкове значення в БД |
| TEST-07.2 | Assignee | Відомі чотири статуси | Оглянути значення | Лише Open/In Progress/Resolved/Closed | Серверне обмеження значень |
| TEST-07.3 | Поточний assignee | Валідний status transition, не Closed | Вибрати дозволений next status → C-17 Apply → повторно відкрити issue | S-03 одразу і при наступному перегляді показує новий status | Persistence і узгодженість між запитами |
| TEST-07.4 | Не-assignee, зокрема Lead | Issue має іншого assignee | Спробувати status change | Status не змінюється | Server authorization |
| TEST-07.5 | Assignee | Вибір status | Спробувати невалідний status | Не приймається значення поза чотирма | Server input validation |
| TEST-08.1 | Auth Member | Є High/Resolved | Відкрити Important | High/Resolved включено | Правильність server predicate |
| TEST-08.2 | Auth Member | Є Critical/Open або Critical/Resolved | Відкрити Important | Critical не-Closed включено | Правильність server predicate |
| TEST-08.3 | Auth Member | Є Low/Normal і Not Set | Відкрити Important | Low/Normal відсутні; Not Set також не кваліфікується за predicate | Правильність server predicate |
| TEST-08.4 | Auth Member | Є Critical/Closed | Відкрити Important | Closed виключено незалежно від priority | Правильність server predicate |

### 7.1 Додаткові граничні тести (поза підрахунком 33 AC)

| Test ID | Actor/context | Передумови | Дія | Очікуваний видимий результат | Що НЕ доводить |
|---|---|---|---|---|---|
| TEST-X01 | Auth Member | M-01 з уведеним Title/Description | Cancel (T-08) | Modal закривається; новий issue не створено; користувач не «телепортується» до іншої вкладки | Server side-effect без integration test |
| TEST-X02 | Assignee | S-03, status Open | Спроба Open → Closed | T-19: без зміни status | Server rejection |
| TEST-X03 | Assignee | S-03, status Resolved | Resolved → In Progress (T-17) | Status In Progress, S-03 залишається відкритим | Persistence |
| TEST-X04 | Assignee | S-03, status Closed | Спроба будь-якого status transition | Жодної доступної вихідної дії | Server enforcement |
| TEST-X05 | Team Lead не-assignee | S-03 чужого issue | Спроба змінити status | T-18: без зміни; Lead role не дає винятку | Server authorization |
| TEST-X06 | Auth Member | У спільному наборі High/Resolved, Critical/Closed та Not Set/Open | Перемикнути All → Important | У Important High/Resolved є, Critical/Closed та Not Set немає; ID збережені | Фактичний спільний backend data source |
| TEST-X07 | Auth Member | S-03 відкрито з Important; issue потім стає Closed законним шляхом | Повернутися (T-23) | APPROVED D-07: повернення до Important; Closed issue більше не відображається | Реальна навігація й server recomputation |
| TEST-X08 | Auth Member | У списку All нуль issues | Відкрити S-02-A | S-02-C у контексті All, а не error | Що фактичний storage порожній |
| TEST-X09 | Auth Member | У загальному списку є тільки Low/Normal/Not Set або Closed | Відкрити Important | S-02-C у контексті Important | Правильність backend filtering |
| TEST-X10 | Team Lead | S-03, priority Not Set | Вибрати High → локальний C-17 Apply | Після успіху High відображається в S-03; жодного «Priority Settings» screen | Persistence; локальний Apply — APPROVED D-06, у тесті треба натиснути |
| TEST-X11 | Auth Member | M-01 з Title/Description | Submit, успішне створення | S-03 показує **саме новостворений issue** з Open/Not Set, ID/author/time (APPROVED D-09) | Реальне збереження, ID consistency і фактичний перехід застосунку без integration test |
| TEST-X12 | Auth Member | S-03, коментар непорожній | Імітувати помилку збереження | Error; новий comment не з'являється, author/time для нього не вигадуються | Server transaction rollback |

## 8. Потрібні бізнес- та UX-рішення — окремо від SOURCE

| ID | Питання/пропозиція | Що вирішує людина | Вплив/блокер |
|---|---|---|---|
| D-02 | S-01 тільки auth boundary, демо зі вже auth S-02 | **APPROVED 2026-11-08** | Застосовано в S-01; login UI не створено |
| D-03 | Not Set як відображення відсутнього priority, без reset | **APPROVED 2026-11-08** | C-12; технічний спосіб зберігання — Q-04 |
| D-04 | Новий issue Unassigned; Lead може assign/reassign | **APPROVED 2026-11-08** | Q-02/Q-03 вирішені; C-11 |
| D-05 | Недоступні actions показувати disabled, не приховувати | **APPROVED 2026-11-08** | C-11/C-12/C-13 |
| D-06 | Вибір + локальний Apply, успіх залишає S-03 | **APPROVED 2026-11-08** | C-17, T-10/T-12/T-14–17 |
| D-07 | Back зберігає попередню вкладку | **APPROVED 2026-11-08** | T-22/T-23, повторне застосування Important predicate |
| D-08 | Умовні навчальні дані та визначені результати прототипу | **APPROVED 2026-11-08** | Демонстрація, не доказ backend |
| APPROVED D-09 / Q-11 | Після успішного Create відкрити S-03 **саме нового issue** | Погоджено розробником проєкту 2026-11-08; записано в Decision Log | **ВИРІШЕНО:** T-09 → S-03; потрібне тестування, не PASS |
| PROPOSED D-10 | Які UI-формати повідомлень/placeholder, крім Gherkin Title? | Затвердити тільки потрібні UI-тексти/стиль | Q-05/Q-06/Q-07; не змінює AC |
| Q-01 | Механізм authentication | Уточнення S1 / реалізації | Не створювати псевдо login |
| Q-04 | Технічне представлення Not Set | Архітектура/розробник | Не вгадувати null/enum |
| Q-08 | Що є вимірюваною «відповіддю < 1 s» | Розробник/викладач | Тести NFR-01, не UI |
| Q-09 | Backup frequency/retention/restore | Розробник/викладач | NFR-04, не UI |
| Q-10 | Умовні імена трьох користувачів | Розробник/викладач | Приклади даних, не нові user roles |

**Стан погодження:** D-01–D-09 **APPROVED (2026-11-08)**, у тому числі Q-11 вирішено D-09. PROPOSED D-10 ще не погоджено: конкретні довільні UI-тексти й формати не можна видавати за SOURCE або автоматично затверджені. Контроль B не проведений.

## 9. Результати підготовки й межі перевірки

- **Покриття документа:** 8 included US та 33 змістові AC, включно з чотирма вихідними ненумерованими пунктами US-03. Усі вони мають UIR-ID, Screen/State, C-ID/annotation, Test ID і Verification level.
- **Тести:** 33 специфіковані основні + 12 граничних; **усі NOT RUN**. Не присвоювати PASS, поки не проведено перевірку фактичного Figma frame, prototype або реалізації.
- **Верифікація M:** показати очікувані поля/контролі, відсутній priority, empty/error, permission contexts, Important і всі status-приклади; макет не доводить жодної серверної операції.
- **Верифікація P:** лише демонстрація дозволених і заборонених переходів, які погоджені; клікабельний прототип не доводить persistence, auth чи транзакційності.
- **Верифікація I:** перевірка server-side permissions, timestamp/author/ID, allowed status values/transitions, comment save failure без створеного запису, спільний data source, response time <1s, HTTPS та backup. Не додавати для них вигаданих screen.
- **Виключено:** US-09 attachments (Deferred), SR-10/SR-11 AI (Future), issue deletion, separate change history, integrations, portal, billing, mobile app.
- **Незавершене:** D-01–D-09 погоджені; Q-11 вирішено D-09. PROPOSED D-10 та інші технічні/візуальні уточнення залишаються відкритими. Input Pack і Screen Map мають REVIEW, не APPROVED; **це draft контрактів G3**, а не підтвердження незалежного Control B.

---

## 10. Контроль G3 — питання «що натискає користувач, за яких умов, що змінюється, де це видно і яким тестом перевіряється»

**Перевірка контенту контракту, не результат запуску тестів.** Кожен рядок нижче відповідає на п'ять запитань розробника й посилається на раніше визначені C-ID, T-ID і TEST-ID. Власне виконання сценаріїв у Figma/застосунку має статус **NOT RUN**.

| Дія / C-ID | Що натискає або вводить | За яких умов / права | Що змінюється | Де видно результат | Тести / T-ID / рівень |
|---|---|---|---|---|---|
| Відкрити All — C-02 | Вкладка **All** | Автентифікований Member/Lead | Поточний фільтр = All; дані issue не змінюються | S-02-A або S-02-C (All) | TEST-02.1, TEST-02.2, TEST-02.5; T-03/T-24; M/P/I |
| Відкрити Important — C-03 | Вкладка **Important** | Автентифікований Member/Lead | Фільтр UI = `priority ∈ {High, Critical} AND status != Closed`, **не створюється окремий список/issue** | S-02-B або S-02-C (Important); High+Resolved є, Critical+Closed та Not Set немає | TEST-08.1–08.4, TEST-X06/X09; T-02/T-25; M/P/I |
| Відкрити issue — C-04 | Рядок із конкретним ID | Issue існує в поточному результаті All/Important | Тільки навігаційний контекст, не дані | S-03 показує поля саме вибраного ID | TEST-02.3/02.4; T-04/T-05; M/P/I |
| Створити — C-05/C-06/C-07/C-08 | **Create Issue**, Title, Description, **Create** | Автентифікований користувач; Title і Description непорожні; успішне створення | Новий issue з ID/author/time, status Open, priority Not Set, assignee Unassigned (D-04) | **S-03 саме нового ID** після T-09 (APPROVED D-09) | TEST-01.1–01.5, TEST-07.1, TEST-X11; T-06/T-07/T-09; M/P/I |
| Відхилити Create — C-09 | **Cancel** | Відкрита M-01 | **Нічого не створюється** | Попередній S-02-A/B (залежно від початкової вкладки) | TEST-X01; T-08; M/P/I |
| Не заповнити required — C-06/C-07/C-08/C-10 | **Create** з порожнім Title/Description | Відсутнє хоча б одне required поле | Немає нового issue; T-09 не запускається | M-01 показує валідацію; точне `Title is required` підтверджує джерело; інші тексти PROPOSED D-10 | TEST-01.2/01.3; M/P/I |
| Призначити/перепризначити — C-11/C-17 | Вибрати одного члена команди → **Apply** поряд з assignee | Лише Team Lead; обраний user належить команді; один assignee | Assignee конкретного issue змінюється; решта полів не міняється | S-03 поле Assignee, у S-02 рядок цього issue; **залишитися S-03** | TEST-03.1–03.4; T-10/T-11; M/P/I |
| Змінити priority — C-12/C-17 | Вибрати Low/Normal/High/Critical → **Apply** поряд з priority | Лише Team Lead; вибране значення належить чотирьом доступним; Not Set не п'ятий рівень; Reset відсутній | Priority цього issue змінюється; може змінитися відповідність Important predicate | S-03 priority; S-02-A/B після повернення; **жодної Priority Settings page** | TEST-04.1/04.2, TEST-08.1–08.4, TEST-X10; T-12/T-13; M/P/I |
| Змінити status — C-13/C-17 | Обрати **лише дозволений наступний status** → **Apply** поряд зі status | Лише поточний assignee, включно з Lead **тільки коли він assignee**; BR-08.1; Closed не має виходу | Лише status issue; після зміни Resolved→Closed issue зникає з Important | S-03 status одразу після success, S-02 статус і Important при поверненні; **залишитися S-03** | TEST-07.2–07.5, TEST-X02–X05/X07; T-14–T-19; M/P/I |
| Заборонена роль/перехід — C-11/C-12/C-13/C-17 | Спроба вибору або Apply | Member не може assign/priority; не-assignee не може status; невалідний перехід заборонено | Дані залишаються незмінними; forbidden controls disabled (APPROVED D-05) | S-03 з незмінними полями; перехід/успіх не показувати | TEST-03.3, TEST-04.2, TEST-07.4/07.5, TEST-X02/X04/X05; T-11/T-13/T-18/T-19; M/P/I |
| Додати comment — C-14/C-15 | Ввести непорожній text → **Add comment** | Автентифікований Member/Lead, text непорожній, save success | Створюється comment з author і timestamp | S-03 список comments із текстом/автором/часом | TEST-06.1–06.4; T-20; M/P/I |
| Save error comment — C-14/C-15/C-18 | **Add comment**; симульована помилка | Текст непорожній, збереження не вдалося | **Comment не створюється** | S-03 показує error, але **нового comment у списку немає** | TEST-06.5, TEST-X12; T-21; M/P/I |
| Назад — C-16 | **Back to Issues** | Issue відкритий із S-02-A або S-02-B | Лише вкладка навігації; повернутися до попередньої, повторно застосувати актуальний фільтр | S-02-A або S-02-B/S-02-C; Closed issue більше немає в Important | TEST-X07; T-22/T-23; APPROVED D-07; M/P/I |

### 10.1 Конкретний приклад перевірки status — без фрази «керування працює»

**Контекст:** `Member A` — поточний assignee issue `ISS-002`; його status `In Progress`. Імена й ID — **фіктивний приклад за D-08**, не дані S1.

1. На **S-03** користувач бачить status `In Progress`, control **C-13** доступний лише йому як assignee. Для `In Progress` дозволено **тільки `Resolved`** як наступний статус.
2. Користувач обирає `Resolved`, натискає **C-17 Apply** поруч із Status (**APPROVED D-06**).
3. За успішного результату **T-15** status змінюється на `Resolved`. Користувач **залишається на S-03**, де значення стає видимим; під час повторного перегляду status має зберігатися (SOURCE AC-07.3).
4. У прототипі перевіряються enabled state, вибір/Apply, зміна видимого значення та відсутність переходу на іншу сторінку. У реалізації — право assignee, допустимість transition, збереження та повторне отримання з БД.
5. **Тести:** TEST-07.2, TEST-07.3, TEST-07.4, TEST-07.5, TEST-X03 (окремо Resolved → In Progress), а також permission matrix §3 і status matrix §4. **Статус: NOT RUN.**

**Негативний приклад:** якщо Team Lead **не** assignee того самого issue, C-13/C-17 для status є **disabled**; T-18 не змінює status (TEST-07.4/TEST-X05). Якщо issue Closed, жодного дозволеного наступного status немає (TEST-X04).

### 10.2 Готовність перед G4

| Критерій контролю | Результат перевірки *тексту документа*, не запуску UI |
|---|---|
| Кожна основна дія має C-ID, передумови, результат та T-ID | ОПИСАНО — §2/§5/§10 |
| Місце появи результату в UI вказане | ОПИСАНО — §2/§10 |
| Для кожного з 33 AC є UIR-ID та Test ID | ОПИСАНО — §6/§7 |
| Чотири permission contexts (assignee як relation) | ОПИСАНО — §3 |
| Матриця всіх 16 комбінацій status | ОПИСАНО — §4 |
| S-03, а не вигадана settings-сторінка для priority | ОПИСАНО — C-12/C-17 і §10 |
| Cancel та невдалий comment save без нових записів | ОПИСАНО — T-08/T-21 |
| Згода D-01–D-09 не замінює фактичних тестів | Усі основні 33 й 12 додаткових тести: **NOT RUN** |
| Явний відкритий UX-вибір | `PROPOSED D-10` — необов'язкові деталі текстів/форматів, що S1 не регламентує |
| Незалежний review | Control B ще не проведено; **не позначати APPROVED** |

**Висновок:** текст Screen Contracts v1.0 готовий до **G4 Critical Review**, але не є підтвердженим Figma-прототипом або системною реалізацією. G4 може знайти нові дефекти, які треба виправити перед Control B.
