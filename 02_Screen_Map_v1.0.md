# 02_Screen_Map_v1.0 — Mini Issue Tracker

**Версія:** v1.0 (перевірена редакція; НЕ APPROVED)  
**Статус:** REVIEW — маршрут Create і D-01–D-09 погоджено; повна перевірка G4 та Control B ще попереду  
**Основа:** SD_Spec.docx.pdf §1/§3/§5/§8, 01_Input_Pack_v1.0.md (REVIEW), методичка G2.  
**Журнал рішень:** D-01–D-09 погоджено 2026-11-08, зокрема D-09 для Q-11 (успішний Create → S-03 нового issue). Це UX-рішення, не SOURCE S1.

---

## 1. Межі системи екранів

### 1.1. Призначення

Mini Issue Tracker — внутрішній вебзастосунок для реєстрації, перегляду та відстеження задач (issues) невеликої команди розробки. Користувачі можуть створювати issues, переглядати їх, коментувати та відстежувати статус. Team Lead додатково може призначати відповідальних і змінювати пріоритет.

### 1.2. Актори

| Актор | Доступні дії |
|---|---|
| Team Member | Створення issue, перегляд, коментарі. Зміна статусу лише для issue, де він є поточним assignee. |
| Team Lead | Усі можливості Team Member; додатково призначення assignee та зміна priority. Зміна статусу — лише якщо Team Lead є поточним assignee. |

### 1.3. Release MVP

У межах G2 враховуються тільки US-01–US-08:

- US-01 Create Issue
- US-02 View Issues
- US-03 Assign Issue
- US-04 Set Issue Priority
- US-05 Track Issue Progress
- US-06 Add Comment
- US-07 Update Issue Status
- US-08 View Important Open Issues

Не включати до Screen Map:

- US-09 Attachments — Deferred.
- SR-10 Automatic issue categorization — Future.
- SR-11 AI priority recommendation — Future.
- Інтеграції, видалення issue, change history та інші функції поза Release MVP.

### 1.4. Запропонована інструкцією G2 структура (D-01 погоджено; D-02 не погоджено)

| ID | Тип | Назва |
|---|---|---|
| S-01 | Screen / placeholder | Authentication boundary |
| S-02 | Screen | Issues List |
| S-02-A | State | All |
| S-02-B | State | Important |
| S-02-C | State | Empty |
| M-01 | Modal / overlay | Create Issue |
| S-03 | Screen | Issue Details |

Assignment, Priority, Status та Comments — це функції та контролі всередині S-03, а не окремі сторінки.

---

## 2. Перелік екранів і станів

### S-01 — Межа автентифікації

| Поле | Опис |
|---|---|
| ID екрана/стану | S-01 |
| Назва | Authentication boundary |
| Призначення | Позначити межу доступу до системи: користуватися нею можуть лише автентифіковані учасники команди. |
| Актори | Team Member, Team Lead |
| Умови входу | Перехід до системи без підтвердженого автентифікованого контексту або початок демонстрації системи. |
| Видимі дані | У межах цього артефакту конкретні дані не визначені. |
| Поля введення | Не визначені. |
| Дії | Не визначені. |
| Умови ролі/стану | Доступ до функцій системи дозволений лише автентифікованим учасникам команди. |
| Помилки/порожні стани | Не визначені. |
| Вихід | Перехід до S-02 після отримання автентифікованого контексту. |
| Джерело/D-ID | SD_Spec §8 — authentication requirement; G2 instruction. D-ID: не присвоєно. |

**Важливо:** S-01 — placeholder. Не створювати вигадану login-сторінку, форму входу, поля пароля, реєстрацію або конкретний механізм автентифікації.

### S-02 — Список issues

| Поле | Опис |
|---|---|
| ID екрана/стану | S-02 |
| Назва | Issues List |
| Призначення | Переглядати issues та переходити до потрібного issue. |
| Актори | Team Member, Team Lead |
| Умови входу | Після S-01; повернення із S-03; відкриття списку після завершення створення issue. |
| Видимі дані | ID, title, status, priority, assignee (якщо призначений). |
| Поля введення | Вибір режиму All або Important; вибір issue; запуск створення issue. |
| Дії | Відкрити issue details; відкрити M-01; перемкнути All / Important. |
| Умови ролі/стану | Обидва актори можуть переглядати список. |
| Помилки/порожні стани | Якщо немає issues для поточного режиму, відображається S-02-C. |
| Вихід | S-03 або M-01. |
| Джерело/D-ID | US-02, US-08; BR щодо складу списку та Important predicate. G2 instruction. D-ID: не присвоєно. |

#### S-02-A — All

| Поле | Опис |
|---|---|
| ID екрана/стану | S-02-A |
| Назва | All Issues |
| Призначення | Показати всі доступні issues. |
| Актори | Team Member, Team Lead |
| Умови входу | Початковий стан списку; повернення до режиму All; перемикання з Important. |
| Видимі дані | Для кожного issue: ID, title, status, priority, assignee, якщо призначений. |
| Поля введення | Вибір issue; перемикання на Important. |
| Дії | Відкрити S-03; відкрити M-01. |
| Умови ролі/стану | Однакові правила перегляду для обох ролей. |
| Помилки/порожні стани | Якщо список не містить issues — S-02-C. |
| Вихід | S-03, M-01 або S-02-B. |
| Джерело/D-ID | US-02; BR щодо полів Issue List. D-ID: не присвоєно. |

#### S-02-B — Important

| Поле | Опис |
|---|---|
| ID екрана/стану | S-02-B |
| Назва | Important Issues |
| Призначення | Показати важливі незакриті issues. |
| Актори | Team Member, Team Lead |
| Умови входу | Перемикання з All у Important; повернення до раніше відкритого режиму Important. |
| Видимі дані | Ті самі поля, що й у S-02-A, але лише для issues, які відповідають Important predicate. |
| Поля введення | Вибір issue; перемикання на All. |
| Дії | Відкрити S-03; перемкнутися на S-02-A. |
| Умови ролі/стану | Доступний обом ролям. |
| Помилки/порожні стани | Якщо жоден issue не відповідає умові Important — S-02-C у контексті Important. |
| Вихід | S-03 або S-02-A. |
| Джерело/D-ID | US-08; BR Important Issues. D-ID: не присвоєно. |

**Important predicate:**

`Priority = High OR Critical` AND `Status != Closed`.

Наслідки:

- High + Open → Important.
- Critical + In Progress → Important.
- High + Resolved → Important.
- Critical + Resolved → Important.
- Critical + Closed → не Important.
- Priority Not Set → не Important.
- Priority Low або Normal → не Important.

Important — це фільтр того самого набору issues, а не окремий незалежний набір даних.

#### S-02-C — Empty

| Поле | Опис |
|---|---|
| ID екрана/стану | S-02-C |
| Назва | Empty List State |
| Призначення | Показати, що в поточному режимі немає issues для відображення. |
| Актори | Team Member, Team Lead |
| Умови входу | S-02-A, якщо немає жодного issue; S-02-B, якщо немає Important issues. |
| Видимі дані | Порожній стан відповідного режиму. |
| Поля введення | Не визначені окремі поля введення. |
| Дії | Перемикання режиму All / Important; створення issue — якщо доступна відповідна дія списку. |
| Умови ролі/стану | Однакові правила для обох ролей. |
| Помилки/порожні стани | Це штатний empty state, а не помилка. |
| Вихід | S-02-A, S-02-B або M-01. |
| Джерело/D-ID | US-02, US-08; G2 instruction. D-ID: не присвоєно. |

S-02-C — стан S-02, а не окрема продуктова сторінка.

---

### M-01 — Створення issue

| Поле | Опис |
|---|---|
| ID екрана/стану | M-01 |
| Назва | Create Issue Modal |
| Призначення | Створити новий issue. |
| Актори | Team Member, Team Lead |
| Умови входу | Натискання дії створення issue у S-02. |
| Видимі дані | Форма з Title та Description. |
| Поля введення | Title — обов'язкове; Description — обов'язкове. |
| Дії | Submit / Create; Cancel. |
| Умови ролі/стану | Будь-який автентифікований учасник може створювати issues. |
| Помилки/порожні стани | Не можна створити issue без обов'язкових Title та Description. Конкретні тексти помилок не визначені. |
| Вихід | Cancel повертає до попереднього стану S-02 без створення issue. У разі успіху issue створюється з початковими значеннями: Status = Open, Priority = Not Set. |
| Джерело/D-ID | US-01; BR щодо створення та початкових значень. D-ID: не присвоєно. |

**Правила створення:**

- Title і Description обов'язкові.
- Cancel не створює issue.
- Новий issue отримує Status = Open.
- Новий issue отримує Priority = Not Set.
- Not Set — відсутність встановленого пріоритету, а не окремий рівень Low / Normal / High / Critical.

**Погоджений маршрут після успішного створення (D-09 / Q-11):** S1 визначає результат створення, але не ціль навігації. За окремим погодженим UX-рішенням після успішного Create відкривається **S-03 з деталями саме новоствореного issue**. При невалідних Title/Description новий issue не створюється та M-01 не переходить у S-03. Навігація — **APPROVED D-09, не SOURCE S1**.

---

### S-03 — Деталі issue

| Поле | Опис |
|---|---|
| ID екрана/стану | S-03 |
| Назва | Issue Details |
| Призначення | Переглядати issue та виконувати дозволені дії з ним на одному екрані. |
| Актори | Team Member, Team Lead |
| Умови входу | Вибір issue у S-02-A або S-02-B. |
| Видимі дані | ID, title, description, status, priority, assignee (якщо призначений), author, created_at; коментарі з автором і датою/часом. |
| Поля введення | Поля для дозволеного редагування assignee та priority; поле введення comment. |
| Дії | Перегляд; призначення assignee; зміна priority; зміна status; додавання comment; повернення до списку. |
| Умови ролі/стану | Assignment і Priority — лише Team Lead. Status — лише поточний assignee. Comment — будь-який автентифікований учасник. |
| Помилки/порожні стани | Невдале збереження comment показує помилку; comment не створюється. Недозволені дії не виконуються. |
| Вихід | Повернення до попереднього list state — S-02-A або S-02-B, з якого було відкрито issue. |
| Джерело/D-ID | US-02–US-07; відповідні BR щодо ролей, статусів, коментарів та переходів. D-ID: не присвоєно. |

#### Розміщення функцій усередині S-03

**1. Assignment**

- Дія доступна тільки Team Lead.
- Team Member не може призначати або змінювати assignee.
- Окрема сторінка Assignment не створюється.
- Якщо поточний користувач не Team Lead, контрол призначення не повинен дозволяти зміну.

Source: US-03; BR щодо permissions.

**2. Priority**

- Дія доступна тільки Team Lead.
- Дозволені значення: Low, Normal, High, Critical.
- Not Set використовується як початкове значення нового issue, а не як один із рівнів пріоритету.
- Окрема сторінка Priority не створюється.

Source: US-04; BR щодо priority.

**3. Status**

Дозволені статуси:

- Open
- In Progress
- Resolved
- Closed

Дозволені переходи:

| Current status | Allowed next status |
|---|---|
| Open | In Progress |
| In Progress | Resolved |
| Resolved | Closed |
| Resolved | In Progress |
| Closed | Немає дозволених переходів |

Додаткові правила:

- Статус може змінювати лише поточний assignee.
- Team Lead не має спеціального права змінювати статус, якщо він не є поточним assignee.
- Closed — кінцевий статус.
- Повернення з Resolved до In Progress дозволене.
- Не можна переходити безпосередньо з Open до Resolved або Closed.
- Окрема сторінка Status не створюється.

Source: US-05, US-07; BR щодо status transitions.

**4. Comments**

- Будь-який автентифікований учасник може додати comment.
- Текст comment обов'язковий і не може бути порожнім.
- Comment відображається разом з автором і датою/часом створення.
- Якщо збереження не вдалося, система показує помилку.
- У разі помилки comment не створюється.
- Окрема сторінка Comments не створюється.

Source: US-06; BR щодо comments.

---

## 3. Таблиця переходів

| T-ID | From | Actor | Trigger | Preconditions | To | Visible result | Requirement / D-ID |
|---|---|---|---|---|---|---|---|
| T-01 | S-01 | Team Member / Team Lead | Отримання автентифікованого контексту | Користувач автентифікований | S-02-A | Відкривається список усіх issues | Authentication requirement; US-02 |
| T-02 | S-02-A | Team Member / Team Lead | Вибір Important | Користувач має доступ до системи | S-02-B або S-02-C | Показуються issues, що відповідають Important predicate, або empty state | US-08; Important BR |
| T-03 | S-02-B | Team Member / Team Lead | Вибір All | Користувач має доступ до системи | S-02-A або S-02-C | Показуються всі issues або empty state | US-02; US-08 |
| T-04 | S-02-A | Team Member / Team Lead | Вибір issue | Issue існує у списку | S-03 | Відображаються деталі вибраного issue | US-02 |
| T-05 | S-02-B | Team Member / Team Lead | Вибір Important issue | Issue відповідає Important predicate | S-03 | Відображаються деталі вибраного issue | US-08; US-02 |
| T-06 | S-02-A | Team Member / Team Lead | Натискання Create Issue | Користувач автентифікований | M-01 | Відкривається форма створення | US-01 |
| T-07 | S-02-B | Team Member / Team Lead | Натискання Create Issue | Користувач автентифікований | M-01 | Відкривається форма створення; попередній list state зберігається як контекст повернення | US-01; навігаційне рішення потребує підтвердження |
| T-08 | M-01 | Team Member / Team Lead | Cancel | Форма відкрита | Попередній стан S-02-A або S-02-B | Modal закривається; новий issue не створюється; введені дані не стають issue | US-01; G2 instruction |
| T-09 | M-01 | Team Member / Team Lead | Create / Submit | Title і Description заповнені; issue успішно створено | S-03 нового issue | Modal закривається; S-03 показує ID, author, created_at, status Open, priority Not Set і деталі саме новоствореного issue | US-01 AC-01.1–01.5; BR-03/04; **APPROVED D-09 (Q-11), не SOURCE** |
| T-10 | S-03 | Team Lead | Зміна assignee | Поточний користувач — Team Lead | S-03 | Issue має нового assignee | US-03; permission BR |
| T-11 | S-03 | Team Member | Спроба змінити assignee | Користувач не Team Lead | Перехід відсутній | Assignee не змінюється | US-03; permission BR |
| T-12 | S-03 | Team Lead | Зміна priority | Поточний користувач — Team Lead; вибрано дозволене значення | S-03 | Priority оновлюється | US-04; permission BR |
| T-13 | S-03 | Team Member | Спроба змінити priority | Користувач не Team Lead | Перехід відсутній | Priority не змінюється | US-04; permission BR |
| T-14 | S-03 | Поточний assignee | Open → In Progress | Поточний користувач є assignee; поточний status = Open | S-03 | Status змінюється на In Progress | US-05; US-07; transition BR |
| T-15 | S-03 | Поточний assignee | In Progress → Resolved | Поточний користувач є assignee; поточний status = In Progress | S-03 | Status змінюється на Resolved | US-05; US-07; transition BR |
| T-16 | S-03 | Поточний assignee | Resolved → Closed | Поточний користувач є assignee; поточний status = Resolved | S-03 | Status змінюється на Closed | US-05; US-07; transition BR |
| T-17 | S-03 | Поточний assignee | Resolved → In Progress | Поточний користувач є assignee; поточний status = Resolved | S-03 | Issue повертається в роботу зі статусом In Progress | US-05; US-07; transition BR |
| T-18 | S-03 | Не-assignee, включно з Team Lead | Спроба змінити status | Поточний користувач не є assignee | Перехід відсутній | Status залишається без змін | US-07; permission BR |
| T-19 | S-03 | Поточний assignee | Спроба недозволеного переходу | Перехід не входить до дозволеної таблиці | Перехід відсутній | Status залишається без змін | US-07; transition BR |
| T-20 | S-03 | Будь-який автентифікований учасник | Submit comment | Текст comment не порожній; збереження успішне | S-03 | Comment з'являється з автором і датою/часом | US-06 |
| T-21 | S-03 | Будь-який автентифікований учасник | Submit comment | Збереження comment не вдалося | S-03 | Відображається помилка; comment не створюється | US-06; failed-save AC |
| T-22 | S-03 | Будь-який автентифікований учасник | Повернення до списку | Issue було відкрито з S-02-A | S-02-A або S-02-C | Повернення до All; відображення актуального стану списку | US-02; навігаційне рішення потребує підтвердження |
| T-23 | S-03 | Будь-який автентифікований учасник | Повернення до списку | Issue було відкрито з S-02-B | S-02-B або S-02-C | Повернення до Important; issue може більше не відповідати Important predicate | US-08; навігаційне рішення потребує підтвердження |
| T-24 | S-02-A | Team Member / Team Lead | Відкриття списку без issues | У наборі немає issues | S-02-C | Показується empty state для All | US-02 |
| T-25 | S-02-B | Team Member / Team Lead | Відкриття Important без відповідних issues | Жоден issue не відповідає Important predicate | S-02-C | Показується empty state для Important | US-08 |

**Примітка до T-11, T-13, T-18, T-19:** недозволена дія не є переходом. Вона не змінює дані issue і не відкриває новий екран.

**Примітка до T-22 і T-23:** повернення має зберігати контекст списку, з якого користувач відкрив issue. Якщо після змін issue більше не відповідає фільтру Important, він не повинен залишатися у S-02-B лише через те, що користувач повернувся назад.

---

## 4. Сценарії користувача

### Сценарій 1 — Створення issue

`S-01 → S-02-A → M-01 → Create success (T-09) → S-03 нового issue`

Очікуваний результат:

1. Користувач відкриває All Issues.
2. Натискає Create Issue.
3. Заповнює обов'язкові Title та Description.
4. Натискає Submit.
5. Створюється issue зі Status Open і Priority Not Set.

**Рішення Q-11 прийнято (APPROVED D-09, 2026-11-08):** після успішного створення відкривати S-03 новоствореного issue.

Якщо користувач натискає Cancel:

`S-02-A → M-01 → Cancel → S-02-A`

Issue не створюється.

### Сценарій 2 — Перегляд issue

`S-01 → S-02-A → S-03 → S-02-A`

Очікуваний результат:

1. Користувач відкриває All Issues.
2. Вибирає issue.
3. Переглядає деталі, статус, пріоритет, assignee, автора, дату створення та коментарі.
4. Повертається до All Issues.

### Сценарій 3 — Призначення issue Team Lead

`S-02-A → S-03 → Assignment action → S-03`

Очікуваний результат:

1. Team Lead відкриває issue.
2. Виконує дію призначення assignee.
3. Issue відображає нового assignee.

Team Member не може виконати цю зміну. Окремий екран Assignment не відкривається.

### Сценарій 4 — Зміна priority Team Lead

`S-02-A → S-03 → Priority action → S-03`

Очікуваний результат:

1. Team Lead відкриває issue.
2. Вибирає один із дозволених рівнів: Low, Normal, High, Critical.
3. Priority оновлюється у деталях issue.

Team Member не може змінювати priority. Окремий екран Priority не відкривається.

### Сценарій 5 — Дозволені зміни status

`S-02-A → S-03 → Status action → S-03`

Очікувані маршрути:

- `Open → In Progress`
- `In Progress → Resolved`
- `Resolved → Closed`

У кожному випадку дія дозволена лише поточному assignee.

### Сценарій 6 — Повернення Resolved issue у роботу

`S-02-A → S-03 → Resolved → In Progress → S-03`

Очікуваний результат:

1. Поточний assignee відкриває Resolved issue.
2. Вибирає дозволений перехід назад у роботу.
3. Status змінюється на In Progress.

Це дозволений виняток із послідовного руху до Closed. Resolved не прирівнюється до Closed.

### Сценарій 7 — Успішне додавання comment

`S-02-A → S-03 → Enter comment → Submit → S-03`

Очікуваний результат:

1. Автентифікований учасник вводить непорожній comment.
2. Надсилає його.
3. Після успішного збереження comment відображається з автором і датою/часом.

### Сценарій 8 — Помилка збереження comment

`S-02-A → S-03 → Enter comment → Submit → Error state on S-03`

Очікуваний результат:

1. Користувач надсилає comment.
2. Збереження не вдається.
3. Система показує помилку.
4. Comment не створюється.

Не можна демонструвати помилку так, ніби comment уже успішно доданий.

### Сценарій 9 — Перегляд Important Issues

`S-02-A → S-02-B → S-03 → S-02-B`

Очікуваний результат:

1. Користувач перемикається на Important.
2. Система показує лише issues із Priority High або Critical та Status, відмінним від Closed.
3. Користувач може відкрити issue.
4. Повернення відбувається до Important, а не до довільного списку.

### Сценарій 10 — Заборонена дія

Приклад: Team Member намагається змінити priority.

`S-02-A → S-03 → prohibited action → S-03`

Очікуваний результат:

- Priority не змінюється.
- Немає переходу на іншу сторінку.
- Заборонена дія не створює нового стану issue.

Інший приклад: Team Lead не є assignee, але намагається змінити status. Дія також заборонена.

### Сценарій 11 — Порожній список

All:

`S-02-A → S-02-C`

Important:

`S-02-B → S-02-C`

Очікуваний результат:

- Якщо немає жодного issue, All показує empty state.
- Якщо issues існують, але жоден не відповідає Important predicate, Important показує empty state.
- Empty state не є помилкою.
- Користувач може перемкнути режим списку.

---

## 5. Кадри Figma для демонстрації

Кількість продуктових екранів не дорівнює кількості Figma frames. Один screen може мати декілька frames для демонстрації різних станів і ролей.

**Попередній демонстраційний набір: 11 Figma frames (PROPOSED, а не затверджений мінімум).**

| Frame | Назва | Що демонструє |
|---|---|---|
| F-01 | Authentication Boundary | Placeholder S-01 без вигаданої форми входу |
| F-02 | Issues — All | S-02-A зі списком issues |
| F-03 | Issues — Important | S-02-B із відфільтрованими issues |
| F-04 | Issues — Empty All | S-02-C для порожнього All |
| F-05 | Issues — Empty Important | S-02-C для порожнього Important |
| F-06 | Create Issue Modal | M-01 із заповнюваними Title та Description |
| F-07 | Issue Details — Team Member | S-03 із дозволеними для Team Member діями |
| F-08 | Issue Details — Team Lead | S-03 із Assignment і Priority controls |
| F-09 | Issue Details — Status Transitions | S-03 із прикладом дозволеного переходу status |
| F-10 | Issue Details — Comment Success | S-03 з успішно доданим comment |
| F-11 | Issue Details — Comment Error | S-03 з помилкою збереження comment |

Frames F-07–F-11 не є новими продуктовими сторінками. Це демонстраційні варіанти одного S-03.

Для повної перевірки статусних переходів потрібно показати щонайменше окремі стани Open, In Progress, Resolved і Closed. Якщо F-09 не демонструє всі ці стани, кількість frames слід збільшити.

---

## 6. Три приклади того, чого НЕ слід додавати

1. **Окрема сторінка Assignment або Priority Settings.**  
   Призначення та зміна priority — контролі всередині S-03. Вони не повинні створювати окремі сторінки.

2. **Delete Issue або Change History.**  
   Видалення issue та користувацька історія змін не входять до Release MVP.

3. **AI-панель автоматичної категоризації або рекомендації priority.**  
   SR-10 та SR-11 віднесені до Future. Не можна додавати ці функції до поточного Release MVP або автоматично змінювати priority без дії користувача.

---

## 7. Мінімальний перелік екранів

| ID | Назва | Тип | Основне призначення |
|---|---|---|---|
| S-01 | Authentication boundary | Placeholder screen | Межа автентифікації |
| S-02 | Issues List | Screen | Перегляд issues |
| S-02-A | All | State | Усі issues |
| S-02-B | Important | State | Важливі незакриті issues |
| S-02-C | Empty | State | Немає issues у поточному режимі |
| M-01 | Create Issue | Modal | Створення issue |
| S-03 | Issue Details | Screen | Перегляд та дозволене керування issue |

**Підсумок:** 2 робочі продуктові screens (S-02, S-03), 1 службова межа S-01 (placeholder, не вигаданий login), 3 стани S-02, 1 modal M-01. Assignment, Priority, Status і Comments залишаються функціями всередині S-03.

---

## 8. Невирішені рішення та питання для журналу

| Q-ID | Питання | Чому важливо |
|---|---|---|
| Q-01 | Який саме механізм автентифікації використовується? | S-01 залишається placeholder, доки рішення не визначено. |
| Q-02 | Який початковий стан assignee для нового issue? | Впливає на відображення assignee і можливість змінювати status. |
| Q-03 | Чи дозволене повторне призначення issue іншому assignee? | Впливає на Assignment control у S-03. |
| Q-04 | Як технічно представляється Not Set? | Впливає на відображення початкового priority. |
| Q-05 | Який точний текст помилки при невдалому збереженні comment? | Впливає на F-11. |
| Q-06 | Який формат дати/часу та timezone використовуються? | Впливає на відображення comments і created_at. |
| Q-07 | Яке остаточне формулювання Important Open Issues? | Потрібно підтвердити назву режиму та його відображення. |
| Q-08 | Як вимірюється вимога response time < 1 sec? | Не можна перевірити її лише за макетом. |
| Q-09 | Які частота та строк зберігання резервних копій? | Не визначає UI, але потребує уточнення для повної специфікації. |
| Q-10 | Які імена трьох predefined users? | Потрібні для узгоджених демонстраційних даних. |
| Q-11 | **ВИРІШЕНО D-09:** успішний Create → S-03 з деталями новоствореного issue | Погоджене UX-рішення 2026-11-08; S1 не задає ціль post-submit. |
| Q-12 | Чи підтверджено повернення з S-03 до попереднього list state? | Визначає, чи потрібно зберігати All/Important як navigation context. |

Q-11 вирішено погодженим D-09, Q-12 (повернення до попередньої вкладки) — D-07. Ці рішення не є вимогами SOURCE S1.

---

## 9. Критерії, які Screen Map ще не покриває повністю

Screen Map описує структуру екранів і маршрути, але сам по собі не підтверджує:

1. Усі 33 Acceptance Criteria з G1 Input Pack.
2. Точний вигляд кожного контролу та його поведінку.
3. Повну permission matrix для кожної дії.
4. Усі можливі комбінації status і ролей.
5. Точні тексти validation та error messages.
6. Реальне збереження даних.
7. Реальну автентифікацію та захист доступу.
8. Виконання NFR: response time, HTTPS та backup.
9. Повну відповідність Figma prototype всім AC.

Ці аспекти потрібно деталізувати на наступних етапах: Screen Contracts, permission matrix, status transition matrix, traceability matrix та тестові сценарії.

---

## 10. Перевірка джерела

| Requirement group | Screen Map coverage |
|---|---|
| US-01 Create Issue | M-01; T-06–T-09 |
| US-02 View Issues | S-02-A, S-02-C, S-03; T-01, T-03–T-05, T-22, T-24 |
| US-03 Assign Issue | S-03 Assignment; T-10, T-11 |
| US-04 Set Issue Priority | S-03 Priority; T-12, T-13 |
| US-05 Track Issue Progress | S-03 Status; T-14–T-17 |
| US-06 Add Comment | S-03 Comments; T-20, T-21 |
| US-07 Update Issue Status | S-03 Status; T-14–T-19 |
| US-08 View Important Open Issues | S-02-B; T-02, T-05, T-23, T-25 |

**Excluded:**

- US-09 Attachments — Deferred.
- SR-10, SR-11 — Future.
- Issue deletion, change history, integrations, customer support portal, billing, CI/CD, time tracking, full project management, mobile app — Out of Scope.

**Перевірка повноти AC:** ця таблиця підтверджує наявність маршруту для кожної з восьми User Stories, але не є повною перевіркою всіх 33 AC. Для цього потрібна окрема звірка кожного AC з G1 Input Pack і Screen Contracts.

**Статус документа:** v1.0 REVIEW — НЕ APPROVED. Маршрут Q-11 вирішено D-09; D-01–D-09 погоджено, але це не замінює перевірку всіх 33 AC і незалежний Control B.

---

## 11. Перевірка G2 для редакції v1.0 (2026-11-08)

**Метод перевірки:** зіставлено наявні screen/state і T-01–T-25 із US-01–US-08, BR-03/04/06/08/08.1/09/09.1, AC-01.1–01.5, AC-02.1–02.5, AC-06.1–06.5, AC-07.1–07.5 та AC-08.1–08.4. Повні UI-контракти й тестову простежуваність кожного з 33 AC готують у G3, тому тут не заявлено про повну перевірку реалізації.

| Контроль методички | Доказ у v1.0 | Результат |
|---|---|---|
| Усі 8 MVP-сценаріїв мають маршрут | US-01: T-06–T-09; US-02: T-01/T-03–05/T-22–24; US-03: T-10–11; US-04: T-12–13; US-05: T-14–17; US-06: T-20–21; US-07: T-14–19; US-08: T-02/T-05/T-23/T-25 | **МАРШРУТИ ОПИСАНО** — T-09 завершено через APPROVED D-09; реальну поведінку ще не протестовано |
| Зміна priority не веде на вигадану сторінку налаштувань | S-03 Priority; T-12 залишається в S-03 | **ПРОЙДЕНО** |
| Important — той самий набір даних, а не незалежний список | S-02-A / S-02-B; спільні ID; predicate `(High OR Critical) AND status != Closed` | **ПРОЙДЕНО** |
| Cancel не створює issue | M-01; T-08; user flow 1 | **ПРОЙДЕНО** |
| Повернення не «телепортує» на довільну сторінку | T-22 до попередньої вкладки All, T-23 до Important, S-02-C зберігає контекст фільтра | **ЛОГІКА ОПИСАНА; ПОГОДЖЕННЯ D-07 ОЧІКУЄТЬСЯ** |
| Заборонена дія не створює переходу | T-11, T-13, T-18, T-19 | **ПРОЙДЕНО** |
| Тільки assignee змінює status, навіть якщо Team Lead не є assignee | S-03, T-14–19 | **ПРОЙДЕНО** |
| Всі чотири status transitions; Closed без вихідних | S-03 Status, T-14–17 | **ПРОЙДЕНО** |
| Resolved High/Critical залишається Important | S-02-B, predicate | **ПРОЙДЕНО** |
| Comment save error не створює запис | S-03 Comments, T-21 | **ПРОЙДЕНО** |
| Empty state не є окремою сторінкою | S-02-C, T-24/T-25 | **ПРОЙДЕНО** |

### 11.1 Важливі розмежування

- **Screen:** S-02, S-03; **службова межа / placeholder:** S-01 (без login UI); **стани одного screen:** S-02-A, S-02-B, S-02-C; **modal:** M-01; **component states:** помилка коментаря, валідатор Title/Description, недоступний control, успішне створення без визначеної навігації; **annotation:** таблиця дозволів/переходів і пояснення для Figma reviewer, не продуктова панель.
- D-01 (desktop grayscale low-fi, All/Important, Create modal) **APPROVED 2026-11-08**.
- D-01–D-09 **APPROVED** як UX-рішення. T-22/T-23 спираються на D-07, T-09 — на D-09; жоден із цих маршрутів не є новою вимогою SOURCE S1.
- При відкритті S-03 з Important після закриття issue повернення до Important повторно застосовує predicate: щойно Closed issue не відображається, а не залишається помилково у списку.
- T-09 веде саме до S-03 новоствореного issue за D-09. Неуспішний Create та валідація порожнього Title/Description не створюють issue; приклад `Title is required` є в Gherkin S1 §5.
- **D-04 APPROVED:** початковий assignee = Unassigned; Team Lead може призначати та перепризначати. Це окреме погоджене UX-рішення, не початкова вимога S1.
- Приклад Figma frames є кількістю демонстраційних станів, а не кількістю продуктових screens. Повний перелік ролей і статусів належить до G3.

### 11.2 Відкриті питання й готовність

| Питання | Вплив |
|---|---|
| Q-11 — ціль навігації після Create | **ВИРІШЕНО D-09:** T-09 → S-03 нового issue; перевірка в прототипі ще попереду |
| D-07 — зберігати попередню вкладку після S-03 | **ПОГОДЖЕНО:** T-22/T-23 повертають до All/Important та повторно застосовують фільтр; макет/прототип ще не перевірені |
| D-01–D-08 | **Погоджено**; прийняті UX-рішення треба відобразити в наступних артефактах |
| Q-02/Q-03 і D-04 | Початковий assignee і повторне призначення |
| Перевірка G3/G4 | Потрібні матриці, покриття всіх 33 AC і незалежний Control B |

**Підсумок:** структурна перевірка маршрутів виконана, D-01–D-09 і Q-11 погоджено. Файл лишається `v1.0 REVIEW` до G4 та незалежного Control B, а не автоматично APPROVED.
