# UX/UI Input Pack — Mini Issue Tracker

**Файл:** `01_Input_Pack_v0.1.md`  
**Версія:** v0.1  
**Статус:** ЧЕРНЕТКА — не затверджено  
**Вихідна специфікація:** `SD_Spec.docx.pdf` (S1)  
**Призначення:** перевірена вибірка вимог для планування UX/UI. Цей документ витягує вимоги, а не визначає екрани чи затверджує нові UX-рішення.

---

## 0. Джерело та стан опрацювання

### Прочитаний вихідний файл

**S1 — `SD_Spec.docx.pdf`**

Повна специфікація обсягом 13 сторінок була доступна та прочитана. Доступні розділи:

- §0 — Початковий запит замовника.
- §1 — Аналіз проблеми.
- §2 — Бачення продукту та початковий обсяг.
- §3 — Потреби й вимоги зацікавлених сторін, включно з BR-01–BR-12.
- §4 — Пріоритизація потреб і попередній MVP.
- §5 — Детальні функціональні вимоги / User Stories та Acceptance Criteria.
- §6 — Вимоги до якості та безпеки.
- §7 — Здійсненність, оцінювання та аналіз ризиків.
- §8 — MVP / остаточний обсяг релізу й оновлені NFR.
- §9 — UX/UI та дизайн взаємодії (доступний заголовок; у наданих сторінках немає додаткових детальних вимог).

**Правило вибірки:** §8 визначає остаточний Release MVP. Попередню пріоритизацію з §4 збережено як контекст, але не використано для зміни §8. Суперечності та прогалини зафіксовано серед невирішених питань.

**Класифікація:**
- `SOURCE` — прямо зазначено в S1.
- `DERIVED` — випливає з однієї або кількох вимог джерела; наведено обґрунтування.
- `PROPOSED` — можливе дизайнерське рішення, не обов'язкова вимога.
- `UNRESOLVED` — потребує уточнення або рішення людини.

---

## 1. Мета продукту, актори та межі релізу

### 1.1 Мета продукту

`SOURCE` — Mini Issue Tracker є внутрішнім вебзастосунком для невеликої команди розробників програмного забезпечення. Він дає змогу реєструвати issues, відстежувати їхній життєвий цикл, призначати відповідальних, визначати пріоритети та обговорювати issues. Також він допомагає команді визначати важливі невирішені issues.

**Джерело:** S1 §1 — Problem Statement і Product Business Goal; §2 — Product Vision.

### 1.2 Основні актори

| Актор | Опис | Джерело |
|---|---|---|
| Team Member | Автентифікований учасник внутрішньої команди. Може створювати й переглядати issues, додавати коментарі та керувати статусом, якщо призначений виконавцем issue. | S1 §1 Primary Users; §3 BR-01, BR-02, BR-08; §5 US-01, US-02, US-05, US-06, US-07 |
| Team Lead | Автентифікований керівник команди. Може виконувати дії учасника, а також призначати issues та встановлювати/змінювати priority. | S1 §1 Primary Users, Open Questions; §3 BR-01, BR-06; §5 US-03, US-04 |

`SOURCE` — У першій версії є три наперед визначені користувачі: два Team Member та один Team Lead.

**Джерело:** S1 §1 Open Questions; §3 BR-01.

### 1.3 Другорядні зацікавлені сторони

`SOURCE` — Product Owner / замовник і System Administrator — другорядні зацікавлені сторони. Вони зацікавлені в результатах або належній роботі системи, але не є основними користувачами головних сценаріїв MVP.

**Джерело:** S1 §1 Stakeholders.

### 1.4 Межі релізу

`SOURCE` — Продукт є вебзастосунком для внутрішніх учасників команди, а не зовнішнім порталом клієнтів. Перший реліз обмежено остаточним переліком із §8.

**Джерело:** S1 §1 KC-01–KC-07; §8 Release Scope.

---

## 2. Обсяг релізу

### 2.1 Включено до Release MVP

`SOURCE` — Остаточний Release MVP включає **US-01–US-08**.

| User Story | Назва | Можливість у релізі | Джерело |
|---|---|---|---|
| US-01 | Створити issue | Зареєструвати заявку з назвою й описом. | S1 §5 US-01 |
| US-02 | Переглянути issues | Перегляд списку й деталей окремих issues. | S1 §5 US-02 |
| US-03 | Призначити відповідального | Призначити одного учасника команди виконавцем issue. | S1 §5 US-03 |
| US-04 | Установити пріоритет issue | Установити або змінити priority. | S1 §5 US-04 |
| US-05 | Відстежувати прогрес issue | Переглянути поточний status. | S1 §5 US-05 |
| US-06 | Додати коментар | Додавати коментарі до issue. | S1 §5 US-06 |
| US-07 | Оновити статус issue | Змінити status відповідно до встановлених правил. | S1 §5 US-07; §3 BR-07, BR-08 |
| US-08 | Переглянути важливі незакриті issues | Знайти High/Critical issues зі статусом, відмінним від Closed. | S1 §5 US-08; §3 BR-09, BR-09.1 |

**Джерело:** S1 §8 MVP / Release Scope.

### 2.2 Відкладено (Deferred)

`SOURCE` — **US-09 — Прикріплення файлів до issue** відкладено; це не частина першого релізу.

У специфікації згадано додаткові потреби для вкладень: сховище файлів, обмеження розміру, перевірка на шкідливі програми та резервне копіювання.

**Джерело:** S1 §5 US-09; §7 рекомендоване коригування обсягу; §8 Deferred.

### 2.3 Майбутні вимоги (Future)

`SOURCE` — Наступні вимоги зацікавлених сторін заплановані на майбутнє й не входять до поточного Release MVP:

- `SR-10` — Автоматична категоризація issue.
- `SR-11` — Автоматична рекомендація priority.

**Джерело:** S1 §3 SR-10, SR-11; §4 Future / Deferred; §8 Future.

`SOURCE` — Якщо AI-функції будуть реалізовані пізніше, вони мають лише рекомендаційний характер. Система не повинна автоматично змінювати category або priority без дії користувача.

**Джерело:** S1 §3 BR-12.

### 2.4 Явно поза обсягом

`SOURCE` — До поточного обсягу продукту не належать:

- Портал підтримки клієнтів.
- Білінг.
- Хостинг вихідного коду.
- Безперервна інтеграція та доставка (CI/CD).
- Облік часу.
- Повне керування проєктами.
- Мобільний застосунок.
- Інтеграції з GitHub, GitLab, Jira або іншими issue trackers у першій версії.
- Прикріплення файлів до issues у першому релізі.
- Автоматична категоризація й автоматична рекомендація priority у першому релізі.
- Видалення issue.
- Окрема видима користувачеві історія змін.

**Джерела:** S1 §1 KC-05, KC-06; §2 Out of Scope; §3 BR-10, BR-11; §8 Release Scope.

`DERIVED` — UX/UI-дизайн не повинен представляти екрани, елементи керування чи сценарії відкладених/майбутніх функцій як доступні в поточному релізі.

**Обґрунтування:** Остаточний Release MVP включає лише US-01–US-08; US-09 відкладено, а SR-10/SR-11 — майбутні вимоги.

**Джерело:** S1 §8.

---

## 3. Включені User Stories та Acceptance Criteria

Усі наведені нижче критерії приймання зберігають вихідні ідентифікатори. Чотири критерії US-03 у S1 не пронумеровані; посилання на них збережено за початковим порядком, без вигаданих AC-ID.

### US-01 — Створити issue

**Актор:** Team Member (будь-який автентифікований учасник команди).  
**Мета:** Створити issue з назвою й описом, щоб зафіксувати проблему для відстеження.

**Джерело:** S1 §5 US-01; §3 BR-01, BR-02.

| Вихідний ID | Критерій приймання | Тип | Джерело |
|---|---|---|---|
| AC-01.1 | Користувач може ввести Title та Description. | SOURCE | S1 §5 US-01, AC-01.1 |
| AC-01.2 | Title є обов'язковим. | SOURCE | S1 §5 US-01, AC-01.2 |
| AC-01.3 | Description є обов'язковим. | SOURCE | S1 §5 US-01, AC-01.3 |
| AC-01.4 | Після створення issue отримує ID, status = Open, created_at та author. | SOURCE | S1 §5 US-01, AC-01.4 |
| AC-01.5 | Після створення priority issue не встановлено. | SOURCE | S1 §5 US-01, AC-01.5; §3 BR-04 |

**Додаткові приклади з джерела — не додаткові AC:**

- Gherkin-приклад успішного створення показує, як автентифікований користувач вводить назву й опис і натискає Create. У результаті створюється issue зі статусом Open, унікальним ID та поточним користувачем як автором.
- Gherkin-приклад порожньої назви показує: issue не створюється, система відображає `Title is required`.

**Джерело:** S1 §5, Gherkin-сценарії для AC-01 і AC-02.

`DERIVED` — Для успішного створення потрібні і Title, і Description, оскільки AC-01.2 та AC-01.3 окремо визначають їх як обов'язкові.

**Джерело:** S1 §5 AC-01.2, AC-01.3.

`SOURCE` — Будь-який автентифікований учасник команди може створити issue; створення не обмежено роллю Team Lead.

**Джерело:** S1 §1 Open Questions; §3 BR-02.

### US-02 — Переглянути issues

**Актор:** Team Member.  
**Мета:** Переглядати зареєстровані issues та поточні деталі.

**Джерело:** S1 §5 US-02; §3 BR-01.

| Вихідний ID | Критерій приймання | Тип | Джерело |
|---|---|---|---|
| AC-02.1 | Автентифікований учасник команди може переглянути список зареєстрованих issues. | SOURCE | S1 §5 US-02, AC-02.1 |
| AC-02.2 | Для кожного issue у списку відображаються принаймні ID, Title, Status, Priority і Assignee, якщо його призначено. | SOURCE | S1 §5 US-02, AC-02.2 |
| AC-02.3 | Користувач може вибрати issue зі списку та відкрити сторінку деталей. | SOURCE | S1 §5 US-02, AC-02.3 |
| AC-02.4 | Сторінка деталей показує ID, Title, Description, Status, Priority, Assignee (якщо призначено), Author та Created at. | SOURCE | S1 §5 US-02, AC-02.4 |
| AC-02.5 | Якщо зареєстрованих issues немає, система показує порожній список або повідомлення про їхню відсутність. | SOURCE | S1 §5 US-02, AC-02.5 |

`SOURCE` — Assignee показується умовно: якщо його призначено.

**Джерело:** S1 §5 AC-02.2 і AC-02.4.

### US-03 — Призначити issue відповідальному члену команди

**Актор:** Team Lead.  
**Мета:** Призначити issue учаснику команди, щоб було зрозуміло, хто відповідає за його виконання.

**Джерело:** S1 §5 US-03; §1 Open Questions.

**Критерії приймання 03 — чотири вихідні ненумеровані пункти:**

| Вихідне посилання | Критерій приймання | Тип | Джерело |
|---|---|---|---|
| US-03, AC, пункт 1 | Можна вибрати одного assignee. | SOURCE | S1 §5 US-03, Acceptance Criteria 03, пункт 1 |
| US-03, AC, пункт 2 | Assignee має бути членом команди. | SOURCE | S1 §5 US-03, Acceptance Criteria 03, пункт 2 |
| US-03, AC, пункт 3 | Призначати issue може лише Team Lead. | SOURCE | S1 §5 US-03, Acceptance Criteria 03, пункт 3; §1 Open Questions |
| US-03, AC, пункт 4 | Поточний assignee відображається в issue. | SOURCE | S1 §5 US-03, Acceptance Criteria 03, пункт 4 |

`DERIVED` — Елемент призначення не повинен дозволяти вибирати більше одного assignee для issue.

**Обґрунтування:** Пункт 1 критеріїв US-03 прямо передбачає вибір одного assignee.

**Джерело:** S1 §5 US-03, Acceptance Criteria 03, пункт 1.

### US-04 — Установити priority issue

**Актор:** Team Lead.  
**Мета:** Визначити пріоритет issue, щоб команда могла визначити порядок роботи.

**Джерело:** S1 §5 US-04; §3 BR-05, BR-06.

| Вихідний ID | Критерій приймання | Тип | Джерело |
|---|---|---|---|
| AC-04.1 | Допустимі значення встановленого Priority: Low, Normal, High, Critical. | SOURCE | S1 §5 US-04, AC-04.1 |
| AC-04.2 | Установлювати та змінювати priority може лише Team Lead. | SOURCE | S1 §5 US-04, AC-04.2; §3 BR-06 |

`SOURCE` — До встановлення пріоритету issue може мати невстановлене/порожнє значення. `Not Set` означає відсутність пріоритету, а не п'ятий рівень.

**Джерело:** S1 §1 Open Questions; §3 BR-04, BR-05.

### US-05 — Відстежувати прогрес issue

**Актор:** Team Member.  
**Мета:** Бачити поточний статус issue, щоб розуміти прогрес роботи.

**Джерело:** S1 §5 US-05.

| Вихідний ID | Критерій приймання | Тип | Джерело |
|---|---|---|---|
| AC-05.1 | Поточний status відображається для кожного issue. | SOURCE | S1 §5 US-05, AC-05.1 |
| AC-05.2 | Status відображається на сторінці issue. | SOURCE | S1 §5 US-05, AC-05.2 |
| AC-05.3 | Status відображається у списку issues. | SOURCE | S1 §5 US-05, AC-05.3 |

### US-06 — Додати коментар

**Актор:** Team Member.  
**Мета:** Додавати коментарі до issue для обговорення проблеми.

**Джерело:** S1 §5 US-06.

| Вихідний ID | Критерій приймання | Тип | Джерело |
|---|---|---|---|
| AC-06.1 | Текст коментаря не може бути порожнім. | SOURCE | S1 §5 US-06, AC-06.1 |
| AC-06.2 | Доданий коментар зберігається та відображається для issue. | SOURCE | S1 §5 US-06, AC-06.2 |
| AC-06.3 | Автор коментаря зберігається та відображається. | SOURCE | S1 §5 US-06, AC-06.3 |
| AC-06.4 | Дата й час створення коментаря зберігаються та відображаються. | SOURCE | S1 §5 US-06, AC-06.4 |
| AC-06.5 | Якщо збереження не вдалося, коментар не створюється, виникає помилка. | SOURCE | S1 §5 US-06, AC-06.5 |

`DERIVED` — Невдало збережений коментар не можна представляти як успішно доданий або показувати серед збережених коментарів.

**Обґрунтування:** AC-06.5 прямо визначає, що за невдалого збереження коментар не створюється.

**Джерело:** S1 §5 AC-06.5.

### US-07 — Оновити статус issue

**Актор:** Team Member, який відповідає за issue (поточний assignee).  
**Мета:** Змінити status, щоб команда бачила поточний етап роботи.

**Джерело:** S1 §5 US-07; §3 BR-07, BR-08, BR-08.1.

| Вихідний ID | Критерій приймання | Тип | Джерело |
|---|---|---|---|
| AC-07.1 | Новий issue створюється зі статусом Open. | SOURCE | S1 §5 US-07, AC-07.1; §3 BR-03 |
| AC-07.2 | Допустимі статуси: Open, In Progress, Resolved, Closed. | SOURCE | S1 §5 US-07, AC-07.2; §3 BR-07 |
| AC-07.3 | Після зміни статусу система зберігає нове значення та показує його за наступного перегляду issue. | SOURCE | S1 §5 US-07, AC-07.3 |
| AC-07.4 | Користувач, який не є assignee цього issue, не може змінити його статус. | SOURCE | S1 §5 US-07, AC-07.4 |
| AC-07.5 | Система не допускає значення статусу поза визначеним переліком. | SOURCE | S1 §5 US-07, AC-07.5 |

**Дозволені переходи статусів:**

| Звідки | Куди | Тип | Джерело |
|---|---|---|---|
| Open | In Progress | SOURCE | S1 §3 BR-08.1 |
| In Progress | Resolved | SOURCE | S1 §3 BR-08.1 |
| Resolved | Closed | SOURCE | S1 §3 BR-08.1 |
| Resolved | In Progress | SOURCE | S1 §3 BR-08.1 |

`SOURCE` — Усі інші переходи статусів заборонені.

**Джерело:** S1 §3 BR-08.1.

`DERIVED` — Closed не має дозволених вихідних переходів, оскільки не вказаний як початковий стан жодного дозволеного переходу, а решту переходів прямо заборонено.

**Джерело:** S1 §3 BR-08.1.

`DERIVED` — Змінювати статус може лише поточний assignee. Team Lead, який не є поточним assignee, також не має права змінити статус.

**Обґрунтування:** BR-08 надає право відповідальному учасникові, AC-07.4 забороняє зміни всім не-assignee. Окремі права Team Lead на призначення та priority не скасовують цього обмеження.

**Джерела:** S1 §3 BR-08; §5 AC-07.4.

### US-08 — Переглянути важливі незакриті issues

**Актор:** Team Member.  
**Мета:** Швидко бачити важливі issues, які потребують першочергової уваги.

**Джерело:** S1 §5 US-08; §3 BR-09, BR-09.1.

| Вихідний ID | Критерій приймання | Тип | Джерело |
|---|---|---|---|
| AC-08.1 | Issue з priority = High і status, відмінним від Closed, відображається в Important Issues. | SOURCE | S1 §5 US-08, AC-08.1 |
| AC-08.2 | Issue з priority = Critical і status, відмінним від Closed, відображається в Important Issues. | SOURCE | S1 §5 US-08, AC-08.2 |
| AC-08.3 | Issues із priority Low або Normal не відображаються в Important Issues. | SOURCE | S1 §5 US-08, AC-08.3 |
| AC-08.4 | Issues зі статусом Closed не відображаються, незалежно від priority. | SOURCE | S1 §5 US-08, AC-08.4 |

`SOURCE` — Resolved означає вирішений, але ще не закритий issue. До переходу в Closed він лишається активним та може відображатися серед Important Issues за відповідного priority.

**Джерело:** S1 §3 BR-09.1.

`DERIVED` — Important Issues включає High/Resolved і Critical/Resolved. Resolved не можна прирівнювати до Closed.

**Обґрунтування:** AC-08.1 та AC-08.2 виключають лише Closed, а BR-09.1 прямо підтверджує, що Resolved залишається активним до Closed.

**Джерела:** S1 §3 BR-09.1; §5 AC-08.1, AC-08.2.

`DERIVED` — Issue з priority Not Set не є Important, оскільки для включення потрібні лише High або Critical.

**Обґрунтування:** BR-04 визначає Not Set як відсутність priority, а AC-08.1–AC-08.3 встановлюють включені та виключені значення priority.

**Джерела:** S1 §3 BR-04, BR-09; §5 AC-08.1–AC-08.3.

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

## 8. PROPOSED items — not binding requirements

No proposed UX decisions are approved by this Input Pack.

The following items are intentionally **not** treated as source requirements:

- Exact screen count or screen names.
- Desktop-only layout.
- Grayscale or low-fidelity visual style.
- Tabs for All Issues / Important Issues.
- A modal rather than a separate page for Create Issue.
- Disabled versus hidden controls for unavailable actions.
- Exact placement or wording of validation messages, except the source Gherkin example `Title is required`.
- An Apply button or any specific save interaction.
- Default assignee behavior.
- Navigation behavior after closing issue details.
- Figma frame count, component names or prototype connections.

**Type:** PROPOSED / not approved.  
**Reason:** These are UX/design decisions, not explicit source requirements. They belong in a separate Decision Log and must be approved before being treated as binding.

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

### 9.4 Final extraction status

- Final Release MVP identified from §8: **US-01–US-08**.
- Included User Stories: **8**.
- Substantive Acceptance Criteria: **33**.
- US-03 unnumbered criteria preserved: **4**.
- Deferred: **US-09**.
- Future: **SR-10, SR-11**.
- UI-relevant BR preserved: **BR-01–BR-12 where applicable**.
- Unresolved questions recorded: **Q-01–Q-10**.

**Status: DRAFT — awaiting human source check and decisions. Not approved.**
