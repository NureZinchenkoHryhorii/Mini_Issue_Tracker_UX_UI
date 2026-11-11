# Mini Issue Tracker — AI Interaction Log

**Версія:** v1.0 (журнал відтворюваності, 2026-11-11)  
**Проєкт:** Mini Issue Tracker UX/UI; [GitHub-репозиторій](https://github.com/NureZinchenkoHryhorii/Mini_Issue_Tracker_UX_UI); [робоча Figma](https://www.figma.com/design/S1oyc2GzQYRCKYfuuWnVf6/Untitled--Copy-?node-id=0-1).  
**Команда:** **два учасники; обидва працювали над усіма етапами**. Цей **спільний ChatGPT-діалог** використовувався для синхронізації. Авторство конкретних натискань, редагувань, перевірок і повідомлень **не встановлюється з самого чату**. У таблицях `оператор — учасник команди (не ідентифікований)` не означає, що працював тільки один учасник загалом.  
**Модель/план:** ChatGPT використовувався для планування, текстів, перевірок та оформлення; конкретні назви режимів і моделей на момент **кожної** взаємодії не зафіксовані — **NOT RECORDED**. Figma Design Agent використовувався для генерації F1 та спроб прототипування; точна назва моделі Agent та тариф/кредитний баланс за кожним зверненням **NOT RECORDED**. Під час ручної спроби зі змінними Figma показала upgrade/paywall; після цього обрано доступні статичні/прототипні інструменти.  
**Джерела:** `SD_Spec.docx.pdf` (S1), методичні рекомендації, [Input Pack](01_Input_Pack_v1.0.md), [Screen Map](02_Screen_Map_v1.0.md), [Screen Contracts](03_Screen_Contracts_v1.0.md), [Decision Log](Decision_Log_v0.1.md), [G4](04_Plan_Review_v0.1.md), [Figma Brief](05_Figma_Brief_v1.0.md), [G6](06_Review_Report.md), [Defect/Change Log](Defect_Change_Log.md).

## 1. Призначення журналу та межі доказів

Цей журнал відтворює **етапи, типи звернень, використаний контекст, рішення людей, фактичні повідомлені результати та обмеження**. Це **не повний дослівний експорт діалогу**: лише фрагменти, дійсно наявні в спільній історії, можна цитувати дослівно. Для повного журналу треба додати доступний викладачу експорт / посилання на розмову окремо; URL експорту зараз не надано. Невідомі дату/час конкретної дії, ім'я оператора, назву моделі або виконаний Figma-action не вгадувати.

**Рівні доказів:** `DOCUMENT` — текст/commit у GitHub; `IMAGE` — скриншот, наданий у спільному чаті; `STUDENT REPORT` — твердження учасника про ручну дію/Present-тест; `AGENT REPORT` — текстова відповідь Figma Agent, **не доказ**, що зв'язки реально створено; `NOT OBSERVED` — незалежне виконання або стан UI не бачили.

**Права та відповідальність:** обидва члени команди залучені до всіх етапів; для захисту кожен повинен показати **власні перевірені приклади** й пояснити рішення. Не стверджувати, що один створив усі документи, а другий — увесь прототип, або що спільний чат автоматично доводить участь кожного в кожній операції.

## 2. Журнал взаємодій за етапами

| ID / дата або період | Оператор / інструмент / режим | Контекст і запит / дія | Вихід AI або інструмента | Рішення та перевірка людьми | Обмеження / доказ |
|---|---|---|---|---|---|
| **AI-01 / 2026-11-08, G1** | Спільний чат; ChatGPT, модель/режим NOT RECORDED | Відібрати включені US-01–US-08, всі 33 змістові AC, BR/NFR та відкласти Deferred/Future; зберегти зв'язки з S1 | `01_Input_Pack_v1.0.md` | Команда використовувала документ як основу; фінальне незалежне затвердження не документовано | DOCUMENT; `REVIEW / NOT APPROVED` |
| **AI-02 / 2026-11-08, G2** | Спільний чат; ChatGPT | Побудувати S-01/S-02/M-01/S-03, S-02-A/B/C та маршрути T-01–T-25; відокремити SOURCE від UX-рішень | `02_Screen_Map_v1.0.md`, `Decision_Log_v0.1.md` | UX-рішення **D-01–D-09 погоджені** в проєкті; D-10 не погоджено | DOCUMENT; статус G2 REVIEW |
| **AI-03 / 2026-11-08, G3** | Спільний чат; ChatGPT | Конкретизувати C-01–C-18, role/assignee matrix, legal status transitions і тестові сценарії для 33 AC | `03_Screen_Contracts_v1.0.md`; тести описані, але тоді NOT RUN | Команда використовувала Screen Contracts як контрольний документ | DOCUMENT; немає доказу серверної авторизації |
| **AI-04 / 2026-11-08, G4** | Спільний чат; ChatGPT як **AI critical reviewer** | Звірити G2/G3 із S1; знайти пропуски, неправильні статуси рішень, Apply та T-09; не додавати нові функції | `04_Plan_Review_v0.1.md` з G4-DEF-01–07; виправлені тексти G2/G3 | G4-DEF-01–05 зафіксовані як виправлення **документів**; DEF-06/07 відкриті/спостереження | DOCUMENT; AI review **не** незалежний Control B |
| **AI-05 / 2026-11-08, Control B** | Спільний чат; ChatGPT + рішення команди | Створити незалежний чеклист і перевірити правила; пізніше команда явно вирішила Control B не проводити | `04_Control_B_Checklist_v0.1.md` як незаповнений протокол; тестові питання в діалозі | **Control B: SKIPPED** за рішенням команди. Відсутні reviewer/date/explicit independent acceptance | DOCUMENT/STUDENT REPORT; **не APPROVED** |
| **AI-06 / 2026-11-08, G5 / Control C** | Спільний чат; ChatGPT | Скомпілювати self-contained англомовний brief за D-01–D-09; перевірити повноту, 4 statuses, Important predicate, ролі, .md, відсутність відсилань до чату | `05_Figma_Brief_v1.0.md`, 12 секцій; перевірено файл у GitHub; після блокування Agent статус змінено на «WORKING DRAFT / Control B SKIPPED» | Команда вирішила перейти до F1, усвідомлюючи пропущений Control B | DOCUMENT; не підтверджує незалежне погодження |
| **AI-07 / 2026-11-08, F1, перше звернення** | Оператор не ідентифікований; Figma Design Agent | Прикріплений brief спочатку містив «DO NOT RUN FIGMA GENERATION YET» | **Дослівна сутність відповіді Agent:** не змінив canvas, попросив Control B acceptance та approved Input Pack/Screen Contracts | За рішенням команди brief виправлено: не фальсифікувати approval, дозволити робочий F1 draft | AGENT REPORT + DOCUMENT; початкове звернення нічого не згенерувало |
| **AI-08 / 2026-11-08, F1, генерація** | Оператор не ідентифікований; Figma Design Agent | Вкладено оновлений brief; запит на editable Figma-native grayscale wireframes, S-01/S-02/M-01/S-03, reference states, no decorative icons/extra functions | Результати F1 — основні кадри/референси й локальні компоненти; скриншоти надані у спільному чаті | AI/команда звірили візуальні приклади з Screen Contracts; учасник повідомив, що frames редагуються | IMAGE/STUDENT REPORT; native component/Auto Layout не повністю інспектовані автором G6 |
| **AI-09 / 2026-11-08–09, P1, ручне налаштування** | Оператор не ідентифікований; ChatGPT-консультації + ручна Figma Prototype | Налаштування All↔Important, Create modal, Cancel, Create→ISS-007, Back; попередні спроби створити зайві копії та використати boolean variable `commentAdded` | У спільному чаті дані покрокові інструкції; створені деякі демонстраційні копії пізніше прибрано; Figma Starter показала upgrade prompt для платних змінних | Команда відмовилась від зайвих дублювань та платних умовних функцій; частину маршрутів повідомлено як робочі в Present | IMAGE/STUDENT REPORT; кроки не означають незалежно перевірені переходи |
| **AI-10 / 2026-11-09–11, P1, повторний Agent-запит** | Оператор не ідентифікований; Figma Design Agent | Після копії старого чату brief додано повторно; запит «Complete Interactive Prototype» вимагав збереження UI, навігації, Apply, чотирьох status transitions, коментарів, без variables/backend | **Отримано текстовий звіт Agent:** «I added native interactions while preserving the existing UI, text, layout, and sample data.» Далі Agent заявив навігацію, компактні Assignee/Priority/Status/Comment demonstrations та відсутність persistence/dynamic filtering | Не сприймали AGENT REPORT як тест; у наступних повідомленнях один із учасників **повідомив перевірку** в Figma Present: два основні маршрути, Apply, чотири переходи, blocked cases, comment success/empty/failure | AGENT REPORT + STUDENT REPORT; прямого live P1 спостереження AI немає |
| **AI-11 / 2026-11-11, G6 аудит** | Спільний чат; ChatGPT | Користувацький запит вимагав таблицю Source/Expected/Screen/Evidence/Result/Remaining Test для всіх 33 AC, окремо BR/D і до 5 UX-issues | [`06_Review_Report.md`](06_Review_Report.md) — 33 AC, UX issues, DEF/Change recommendations, UI PARTIAL; prototype REPORTED; implementation outstanding | Команда отримала перелік для ручних виправлень; звіт не вважає текст Agent доказом виконання | DOCUMENT + попередні IMAGE; живий приватний файл Figma не перевірено напряму |
| **AI-12 / 2026-11-11, G6, DEF-01** | Оператор не ідентифікований; ручна Figma + ChatGPT як журнал | У ISS-007 були випадково скопійовані два коментарі ISS-002; запропоновано видалити тільки ці записи | Команда повідомила видалення та Present retest нового ISS-007, збереження двох коментарів ISS-002 | **FIXED / RETEST PASS — student-reported**; оновлено `06_Review_Report.md` | STUDENT REPORT / DOCUMENT; післяправковий screenshot не надано |
| **AI-13 / 2026-11-11, G6, UX-01** | Оператор не ідентифікований; ручна Figma + ChatGPT | `Resolved` містив нерозділену фразу `Closed or In Progress`; запропоновано показати два окремі next-value options з Apply | Команда повідомила про розділення та тестування Resolved→Closed і Resolved→In Progress та blocked transitions | **FIXED / RETEST PASS — student-reported**; оновлено `06_Review_Report.md` | STUDENT REPORT / DOCUMENT; новий screenshot не надано |
| **AI-14 / 2026-11-11, G6, UX-02/03** | Оператор не ідентифікований; спільний чат + ручний Figma Present | UX-02: Assignee/Priority selection clarity; UX-03: чи виникає empty comment error лише після submit | Повідомлено: UX-02 зрозумілий без зміни; UX-03 валідний, бо помилка після порожнього submit | **UX-02 ACCEPTED WITHOUT CHANGE; UX-03 NOT REPRODUCED / CHECK PASS — reported** | STUDENT REPORT; незалежних usability-test чи запису Present немає |
| **AI-15 / 2026-11-11, документація** | Спільний чат; ChatGPT із GitHub connector | Зафіксувати source-linked G6 follow-ups, облік дефектів і командну участь | `06_Review_Report.md` оновлено; `Defect_Change_Log.md` створено; цей `AI_Interaction_Log.md` | Підтверджено спільний характер роботи обох учасників на всіх етапах, але конкретні автори окремих змін не вгадувалися | DOCUMENT; журнал не є підписаним персональним таймшитом |

## 3. Відомі приклади промптів і відповідей з діалогу

### A. Запит до ChatGPT на створення G5 (зміст, наявний у діалозі)

> «Скомпілюй один self-contained англомовний Figma Design implementation brief з погоджених Screen Contracts. Це не новий UX-дизайн і не переказ усієї специфікації.»

У тому ж запиті перелічені обов'язкові секції, заборона незатверджених UX-рішень, вимога editable native layers, local components, Auto Layout, grayscale, no icon placeholders, а також Prototype annotations only. Вихід — [G5 brief](05_Figma_Brief_v1.0.md).

### B. Початкова реакція Figma Agent (фрагмент, наявний у діалозі)

> «The attached brief is marked “DRAFT / NOT APPROVED — DO NOT RUN FIGMA GENERATION YET.” ... so I haven’t changed the canvas.»

Вихід: виправлено **не фальсифікуючи статусу незалежної перевірки**; `Control B: SKIPPED` та `working draft`, а не `approved`.

### C. Наступний звіт Figma Agent про прототип (фрагмент, наявний у діалозі)

> «I added native interactions while preserving the existing UI, text, layout, and sample data.»

Agent окремо заявив: All↔Important, ISS-002 navigation, Back, Create overlay, Cancel, Create→ISS-007, compact Apply demos, status restrictions, comment examples. Обмеження зі звіту: змінені значення видимі **у компактних демонстраціях**, але не переписують записи деталей/списків; приклади скидаються після повторного відкриття; live typing, persistence і dynamic Important filtering відсутні. **Це лише AGENT REPORT;** далі команда повідомила окремі ручні Present-тести.

### D. Промпти, які не слід помилково вважати виконаними

У спільному діалозі ChatGPT формулював інструкції для Figma Agent і для ручного Prototype. **Наявність тексту такого промпта не доводить, що його надсилали**, якщо немає відповіді Agent чи підтвердження оператора. Перший Agent відмовився змінювати canvas; окремий повторний Agent-прохід описаний лише за отриманою відповіддю.

## 4. Людські рішення, відхилені варіанти й обмеження

| Рішення | Прийнято / відхилено | Підстава / наслідок |
|---|---|---|
| D-01–D-09 | APPROVED UX decisions | Перенесені до G2/G3/G5 з чіткими Source/D-ID |
| Незалежний Control B | **SKIPPED**, не APPROVED | Рішення команди; ризик для відповідності процесу методички не приховувати |
| Блокування Figma за `DRAFT` | Замінено на дозвіл **working F1 draft** | Не створювати неправдиву independent acceptance |
| Реальна backend/auth/persistence | OUT OF SCOPE для F1/P1 | Статичні макети й прототипні переходи не доводять реалізацію S1 NFR/BR серверного рівня |
| Variables / conditional logic у Figma Starter | Не використано в кінцевому сценарії | Paywall показано під час ручної спроби; без потреби купувати тариф |
| Масове копіювання повних frames | Відхилено як надмірне | Основні frames + compact examples; для повернення використано native `Back`, де доступно |
| UX-02 selection affordance | Без змін, команда вважає зрозумілим | Не видавати це за зовнішнє user study |
| UX-03 empty-comment focus issue | Не відтворено за повідомленням команди | Повідомлено, що error лише після empty submit, не після focus |

## 5. Докази й незавершені пункти для здачі

**Доступні артефакти:** GitHub G1–G6 документи, Figma share URL, скриншоти станів у спільному діалозі, повідомлені результати Figma Present, журнали змін із прив'язкою до source. **Відсутні або не підтверджені:** публічний/доступний викладачу експорт чату; індивідуальні імена операторів кожної дії; точна модель/режим кожного виклику; версія Figma після останньої правки; оновлені післяправкові screenshots і незалежний replay; backend/integration test evidence.

**Для командного захисту:** кожен учасник показує свій **реально виконаний або особисто перевірений** кейс (наприклад, один — permission/status і traceability, інший — Create/comment/prototype), пояснює конкретний Source → Screen Contract → Figma state → Test → correction. Це **план презентації**, а не ретроспективне приписування авторства. Учасники можуть додати власні приклади/операції за фактичними даними.

**Статус результату:** це **відтворюваний підсумковий журнал** на основі відомої історії, не proof-of-execution для всіх AI-промптів і не звіт про повністю виконані 33 AC.
