# 04_Plan_Review_v0.1 — G4 Critical Review до Figma

**Дата:** 2026-11-08  
**Reviewer:** AI у ролі критичного рецензента — **не незалежний Control B**  
**Результат:** **PLAN READY (рекомендація для переходу до Control B, НЕ дозвіл на Figma)** після внесених мінімальних виправлень; фактичні Figma/UI/backend тести **NOT RUN**. Остаточне рішення — за розробником та незалежним рецензентом.  
**Джерело перевірене:** `SD_Spec.docx.pdf`, усі 13 сторінок: §1 Open Questions, §3 Business Rules, §5 US/AC, §8 Release MVP/NFR.  
**Артефакти:** `01_Input_Pack_v1.0.md`, `Decision_Log_v0.1.md` (D-01–D-09 APPROVED), `02_Screen_Map_v1.0.md`, `03_Screen_Contracts_v1.0.md`, зокрема §6 Traceability і §7 Tests.  
**Увага:** `PLAN READY` тут означає лише рекомендацію про логічну готовність плану **для незалежної перевірки**. За методичкою G4/Control B перед Figma потребує людського затвердження, а не самосхвалення AI.

## Вихід 1 — Coverage matrix: усі 33 included AC

Правило оцінювання: COVERED = конкретні contract/screen/TEST-ID й узгодження з S1; це **не PASS тесту**. AMBIGUOUS = для формального відтворення бракує істотної логіки; MISSING = у плані немає вимоги. Не позначати анотації чи mock як backend evidence.

| Included US | Source AC / пункт | Coverage | Доказ у S1 та плані | Висновок |
|---|---|---|---|---|
| US-01 | AC-01.1 | COVERED | S1 §5 с.7; G3 §2 M-01 C-06/C-07, §6 UIR-01.1, TEST-01.1 | Два user inputs: Title, Description; інших продуктових полів Create немає. |
| US-01 | AC-01.2 | COVERED | S1 §5 с.7–8; G3 M-01 C-06/C-08/C-10, TEST-01.2 | Required Title; `Title is required` є в Gherkin; без створення. |
| US-01 | AC-01.3 | COVERED | S1 §5 с.7; G3 M-01 C-07/C-08/C-10, TEST-01.3 | Required Description; точний текст помилки не визначено (UX detail). |
| US-01 | AC-01.4 | COVERED | S1 §5 с.7–8; G3 M-01/S-03, T-09, UIR-01.4/TEST-01.4 | ID, Open, created_at, author; D-09 визначає UX-ціль S-03 нового ID. |
| US-01 | AC-01.5 | COVERED | S1 §5 с.7; G3 §1 Priority, UIR-01.5/TEST-01.5 | Priority відсутній (Not Set), не Normal; D-03 лише про UI-подання. |
| US-02 | AC-02.1 | COVERED | S1 §5 с.8; G3 S-02-A C-02, TEST-02.1 | Автентифіковані учасники бачать список. |
| US-02 | AC-02.2 | COVERED | S1 §5 с.8; G3 S-02 Visible data, UIR-02.2/TEST-02.2 | ID, Title, Status, Priority, Assignee за наявності. |
| US-02 | AC-02.3 | COVERED | S1 §5 с.8; G2 T-04/T-05; G3 C-04, TEST-02.3 | Відкрити S-03 конкретного рядка. |
| US-02 | AC-02.4 | COVERED | S1 §5 с.8–9; G3 S-03 Visible data, TEST-02.4 | ID, Title, Description, Status, Priority, Assignee за наявності, Author, Created at. |
| US-02 | AC-02.5 | COVERED | S1 §5 с.9; G3 S-02-C, T-24/TEST-02.5 | Порожній стан All; Important Empty — похідне від фільтра. |
| US-03 | US-03, AC, пункт 1 | COVERED | S1 §5 с.9; G3 C-11/C-17, TEST-03.1 | Рівно один assignee, вибір + Apply за D-06. |
| US-03 | US-03, AC, пункт 2 | COVERED | S1 §5 с.9; G3 C-11, TEST-03.2 | Кандидат у assignee є членом команди. |
| US-03 | US-03, AC, пункт 3 | COVERED | S1 §5 с.9; G3 §3, TEST-03.3 | Призначає тільки Lead; Member має disabled control (D-05). |
| US-03 | US-03, AC, пункт 4 | COVERED | S1 §5 с.9; G3 S-03 Assignee, TEST-03.4 | Поточний assignee видно; Unassigned на Create і reassign — D-04, не S1. |
| US-04 | AC-04.1 | COVERED | S1 §5 с.9; G3 C-12, TEST-04.1 | Чотири варіанти: Low, Normal, High, Critical; Not Set — відсутність. |
| US-04 | AC-04.2 | COVERED | S1 §5 с.9 / BR-06; G3 §3, C-12/C-17, TEST-04.2 | Лише Lead може встановлювати/змінювати priority. |
| US-05 | AC-05.1 | COVERED | S1 §5 с.9; G3 S-02/S-03, TEST-05.1 | Поточний status доступний для кожного issue. |
| US-05 | AC-05.2 | COVERED | S1 §5 с.9; G3 S-03 C-13, TEST-05.2 | Status відображається в деталях. |
| US-05 | AC-05.3 | COVERED | S1 §5 с.9; G3 S-02 rows, TEST-05.3 | Status відображається у списку. |
| US-06 | AC-06.1 | COVERED | S1 §5 с.10; G3 C-14/C-15, TEST-06.1 | Порожній comment не додається; формат required error не зафіксовано. |
| US-06 | AC-06.2 | COVERED | S1 §5 с.10; G3 S-03 Comments, T-20/TEST-06.2 | Після success comment збережений і показаний для issue; persistence тільки I. |
| US-06 | AC-06.3 | COVERED | S1 §5 с.10; G3 S-03 Comments, TEST-06.3 | Автор comment показаний; реальне записування тільки I. |
| US-06 | AC-06.4 | COVERED | S1 §5 с.10; G3 S-03 Comments, TEST-06.4 | Дата/час comment видимі; формат/таймзона відкладені. |
| US-06 | AC-06.5 | COVERED | S1 §5 с.10; G3 C-18, T-21/TEST-06.5, TEST-X12 | Failed save → error і **жодного** нового comment. |
| US-07 | AC-07.1 | COVERED | S1 §5 с.10; G3 M-01/S-03, TEST-07.1 | Новий issue Open. |
| US-07 | AC-07.2 | COVERED | S1 §5 с.10; G3 §4, C-13/TEST-07.2 | Лише Open, In Progress, Resolved, Closed. |
| US-07 | AC-07.3 | COVERED | S1 §5 с.10; G3 C-13/C-17, TEST-07.3 | Apply → status видимий зараз і при повторному відкритті; persistence перевіряти на I. |
| US-07 | AC-07.4 | COVERED | S1 §5 с.10 / BR-08; G3 §3, TEST-07.4, TEST-X05 | **Lead non-assignee теж не може** змінювати status. |
| US-07 | AC-07.5 | COVERED | S1 §5 с.10 / BR-08.1; G3 §4, TEST-07.5, TEST-X02/X04 | Не приймати значення поза переліком і переходи поза чотирма; Closed без виходу. |
| US-08 | AC-08.1 | COVERED | S1 §5 с.10; G3 S-02-B/TEST-08.1 | High з будь-яким status, крім Closed, включено; High+Resolved включено. |
| US-08 | AC-08.2 | COVERED | S1 §5 с.10; G3 S-02-B/TEST-08.2 | Critical з будь-яким status, крім Closed, включено; Critical+Resolved включено. |
| US-08 | AC-08.3 | COVERED | S1 §5 с.11; G3 S-02-B/TEST-08.3 | Low/Normal виключено; Not Set випливає з predicate, не дослівний AC. |
| US-08 | AC-08.4 | COVERED | S1 §5 с.11; G3 S-02-B/TEST-08.4 | Closed виключено за будь-якого priority. |

**Підсумок:** **33/33 COVERED, 0 MISSING, 0 AMBIGUOUS** за критерієм наявності *специфікованих* UI-контрактів, простежуваності та тестів після G4-виправлень. Усі 45 тестів ще **NOT RUN**; описаний тест не доводить реального збереження або серверного доступу.

## Особливі перевірки джерела й scope

- **BR-08 / AC-07.4:** Team Lead, який не є поточним assignee, **не змінює status**. G3 §3, T-18, TEST-X05; у UI C-13/C-17 disabled; для реального API перевірка окрема.
- **Create:** лише Title/Description як user inputs; ID/author/created_at/Open/Not Set генерує система. Assignee Unassigned — APPROVED D-04, а не вимога S1 про початкове значення.
- **BR-08.1:** рівно `Open→In Progress`, `In Progress→Resolved`, `Resolved→Closed`, `Resolved→In Progress`; 16-коміркова матриця G3 §4. `Closed` не має вихідних status transitions. **Не переносити** заборону status на коментарі/priority.
- **BR-09/09.1:** `(High OR Critical) AND status != Closed`, у тому числі High/Resolved та Critical/Resolved; Not Set не кваліфікується. Resolved ≠ Closed.
- **Джерельні ID:** US-01–US-08 включені, US-09 Deferred; SR-10/SR-11 Future. У US-03 AC не мають номерів: написання `US-03, AC, пункт 1–4` коректне. `UIR-xx`, `TEST-xx`, `C-ID`, `T-ID`, `D-ID`, `Q-ID` — локальні ID, а не AC з S1.
- **Дублювання/зайві controls:** S-02-A/B/C — стани одного списку; M-01 — modal; S-03 — єдиний detail screen, без окремих Priority Settings/Assignment/Comments pages. S-01 — annotation, не вигаданий Login. Немає deletion, history, attachment upload, AI, bulk controls.
- **NFR:** `NFR-03 HTTPS only` та `NFR-04 Backup of all data` із фінального §8 не стають екранами. `NFR-01 <1s`, real auth і persistence не перевіряються в статичному макеті. Зазначення attachments у ранньому NFR не скасовує фінальний scope.
- **Empty/error:** Empty All і Empty Important описані, Title/Description required, comment empty, save failed → error без comment. Точний UI-copy для частини випадків **не задано S1**, окреме D-10 лише proposal.

## Вихід 2 — Defect Log (вимогові/документаційні та необов'язкові UX)

Severity: **BLOCKER** — некоректний/неповний контракт, що заважає генерації; **MAJOR** — суперечність, яку слід виправити до G5; **MINOR** — несуттєва неточність або неузгоджений текст. `FIXED` означає виправлений **текст артефакту**, не PASS в UI.

| DEF-ID | Severity | Тип / source | Plan location | Проблема | Мінімальне виправлення | Статус |
|---|---|---|---|---|---|---|
| DEF-01 | MAJOR | документаційний дефект (D-01–D-09) | G3 v1.0 §8 (після таблиці) | Фраза «погоджено тільки D-01» суперечила реальному Decision Log; могла зупинити Figma без підстав. | Змінити лише status-підсумок на D-01–D-09 APPROVED; D-10 PROPOSED. | FIXED |
| DEF-02 | MAJOR | контракт навігації, D-09/Q-11 | G3 v1.0 §2 S-03 Actors/entry | S-03 описував лише входи T-04/T-05, пропускаючи затверджений T-09 після Create. | Додати T-09 як вхід S-03 саме нового issue. | FIXED |
| DEF-03 | MAJOR | G2/G3 action consistency, D-06 | G2 §3 T-10/T-12/T-14–17; G3 §5/§7 тести | Тригери та тести подекуди казали лише «вибрати», хоча D-06 вимагає явного Apply. | Додати Apply у тригери та релевантні тести, не змінюючи прав або SOURCE. | FIXED |
| DEF-04 | MINOR | UX-рішення D-07/D-09 | G2 §3 T-22/T-23; §11; G3 §2 S-03 | Back після успішного Create не був явно прив'язаний до вкладки, з якої відкрили modal; також лишилася застаріла позначка D-07 pending. | Прив'язати контекст повернення до джерела відкриття Create, виправити pending текст. | FIXED |
| DEF-05 | MINOR | Decision Log D-02/D-04 та Q-02/Q-03 | G2 §1.4, §8 | Застарілий заголовок «D-02 не погоджено» та Q-02/Q-03 без позначки resolved, хоча D-02/D-04 APPROVED. | Змінити лише відповідні рядки і заголовок. | FIXED |
| DEF-06 | MINOR | невизначені UI-деталі (не S1 defect) | G3 §2 S-02-C/M-01/S-03, C-10/C-18; §8 D-10 | Повідомлення для Description required, пустого comment, failed comment save та empty state не мають точного тексту/стилю. S1 задає лише обов'язковість/результат; для Title містить текст `Title is required`. | Для brief використати generic annotation без видавання довільного тексту за SOURCE або окремо погодити D-10, якщо Figma вимагає точні copy/format. | OPEN — UX NON-BLOCKING для логіки; уточнити до генерації копірайту |
| DEF-07 | MINOR | демонстраційна модель / D-08 | G2 §1 S-01 → S-02; G3 §2 S-02 Default | Стартова вкладка All є робочою домовленістю G2, але S1 її не визначає; позначено як модель, не SOURCE. Для Figma brief треба зберегти це розмежування. | У G5 назвати All початковим станом **демонстрації**, а не обов'язковою поведінкою системи. | OBSERVATION — NON-BLOCKING |

**Вимогових розбіжностей, які вимагали б зміни S1, під час звірки не виявлено.** DEF-01–05 — суперечності/пропуски в **плані**, виправлені без зміни бізнес-правил. DEF-06–07 — окремі UX-деталі/ризик помилкового тлумачення, не підстава додавати нову функцію.

## Вихід 3 — Blocker Q-ID та відкладені питання

| ID | Тема | Рішення для G4/G5 |
|---|---|---|
| Q-01 | Спосіб реальної автентифікації | DEFER для Figma; BR-01 обов'язкове, але D-02 дозволяє auth boundary; необхідно перед реалізацією. |
| Q-02/Q-03 | Unassigned та reassign | RESOLVED D-04; не блокують. |
| Q-04 | null/enum для Not Set | DEFER для backend; Figma виводить Not Set за D-03. |
| Q-05 | Дослівний текст failed comment save | DEFER за умови generic error/annotation; **сам error і no comment** обов'язкові. |
| Q-06 | Формат часу та timezone | DEFER, але в UI мають бути author+date/time; не вигадувати SOURCE формат. |
| Q-07 | Назва Important Open Issues | NON-BLOCKING: D-01 погодив вкладку Important; predicate береться з BR-09/09.1. Не змінювати значення слова «open» на `Open` status. |
| Q-08/Q-09 | <1 s, HTTPS, backup frequency | DEFER backend/verification; не створювати UI screens. |
| Q-10 | Імена трьох predefined users | DEFER; D-08 дозволяє фіктивні Member A/B, Lead для макета. |
| Q-11/Q-12 | Після Create та Back | RESOLVED D-09 / D-07; не блокують. |
| D-10 | Конкретні тексти/формат empty/error | OPTIONAL UX proposal; точні візуальні copy потрібні лише якщо brief їх визначає, не можна самовільно затверджувати. |

**Невирішених Q-ID, що блокують саме логіку low-fi Figma generation, після внесених виправлень немає**, за умови що не затверджені точні тексти не видаються за SOURCE, а позначаються generic error/placeholder. Якщо brief вимагає конкретний текст error/empty state, погодити відповідну частину D-10 **до запуску Figma**. Для реальної реалізації Q-01/Q-04/Q-08/Q-09 потребуватимуть окремих рішень/тестів.

## Вихід 4 — PLAN READY / NOT READY

**PLAN READY — умовна рекомендація рецензента на рівні структури та логіки, після мінімальних виправлень.** Відповідність 33 included AC задокументована й звірена із S1; не виявлено відкритих логічних BLOCKER для створення низькодеталізованих макетів. Це **не** рішення про фактичний запуск Figma та **не** твердження, що тести пройдені.

**Перед Figma обов'язково:** незалежний **Control B** (інша людина/викладач) перевіряє permission/status матриці та кілька edge cases, записує `Reviewer`, `Date`, `Version`, `Accepted decisions`, `Open blockers` і приймає/відхиляє рекомендацію. Якщо є unresolved blocker — **не запускати Figma**. Тільки після підтвердження людиною можна позначати Pack/Contracts `APPROVED` і переходити до G5 brief.

## Список змінених пунктів (не переписані непорушені розділи)

1. `03_Screen_Contracts_v1.0.md`: §2 S-03 Actors/entry — додано T-09; §5 — уточнено Apply у T-10/T-12/T-14–17; §7 — виправлено кроки TEST-03.1, TEST-03.3, TEST-04.2, TEST-07.3 і TEST-X10; §8 — застарілий статус D-01 замінено на D-01–D-09.
2. `02_Screen_Map_v1.0.md`: §1.4 — актуальний D-02; §3 — T-07/T-10/T-12/T-14–17/T-22/T-23 з Apply та контекстом повернення з Create; §8 — Q-02/Q-03/Q-12 позначені resolved; §11 — прибрано застарілий pending D-07.
3. `SD_Spec.docx.pdf` **не змінено**; непорушені частини Input Pack, Decision Log і Traceability залишено без переписування.

**Контроль B:** PENDING — reviewer/date/decision мають бути внесені реальною незалежною людиною. AI не імітує її підпис чи APPROVED.