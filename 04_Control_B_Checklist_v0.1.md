# Mini Issue Tracker — Control B: протокол незалежної перевірки

**Версія плану для перевірки:** Input Pack v1.0 (REVIEW), Screen Map v1.0 (REVIEW), Screen Contracts v1.0 (REVIEW), Decision Log D-01–D-09; G4 `04_Plan_Review_v0.1.md`  
**Джерело:** `SD_Spec.docx.pdf`, §1/§3/§5/§8  
**Стан Control B:** PENDING — **не виконано й не затверджено**. Файл є бланком перевірки, а не свідченням її проходження.

## A. Журнал рецензента (заповнює реальна незалежна людина)

| Поле | Значення |
|---|---|
| Reviewer (інший студент/викладач) | **PENDING — не вказано** |
| Date (фактична дата перевірки) | **PENDING** |
| Version | `01_Input_Pack_v1.0.md`; `02_Screen_Map_v1.0.md`; `03_Screen_Contracts_v1.0.md` |
| Accepted decisions | **PENDING**; D-01–D-09 погоджені розробником, але ще не прийняті незалежним рецензентом |
| Open blockers | **PENDING — результат перевірки не відомий** |
| Review result | **PENDING** (Accept / Changes required) |
| Confirmation from reviewer | **PENDING**; не підставляти підтвердження AI за людину |

## B. Контрольні сценарії для незалежного рецензента

У кожному пункті перевірити оригінальне правило S1, відповідний рядок матриці у Screen Contracts §3/§4/§6, маршрут Screen Map §3 та TEST-ID. Позначити **PASS / FAIL / QUESTION** лише після фактичної перевірки; не плутати перевірку плану з виконанням UI/backend-тесту.

| ID | Контрольне питання / сценарій | Очікуване правило S1 чи погоджене D-рішення | Доказ у плані | Фактична оцінка рецензента |
|---|---|---|---|---|
| CB-01 | Team Lead **не є assignee**: чи може змінювати status? | **Ні**; AC-07.4, BR-08; status control disabled, нічого не збережено | G3 §3, C-13/C-17, T-18, TEST-X05 | **NOT CHECKED** |
| CB-02 | Team Member **є assignee**, issue = Open: який дозволений перехід? | **Лише Open → In Progress**, за Apply (D-06) | G3 §4, T-14, TEST-07.3 | **NOT CHECKED** |
| CB-03 | Issue = Resolved: які наступні statuses? | **Closed або In Progress**, а не Open | G3 §4, T-16/T-17, TEST-X03 | **NOT CHECKED** |
| CB-04 | Issue = Closed, користувач його assignee | **Немає вихідних status transitions**; не запроваджувати глобальну заборону comments/priority | G3 §4, T-19, TEST-X04 | **NOT CHECKED** |
| CB-05 | Create відкрито: які user inputs? | **Лише Title і Description**; status Open, priority Not Set, ID/author/time генеруються; Unassigned за D-04 | G3 §2 M-01, TEST-01.1–01.5 | **NOT CHECKED** |
| CB-06 | Create без Title / без Description | **Не створювати issue**; для Title є SOURCE-приклад `Title is required` | G3 C-10, TEST-01.2/01.3 | **NOT CHECKED** |
| CB-07 | Create успішний | **S-03 нового issue** за D-09; не додавати це до SOURCE S1 | G2 T-09; G3 S-03, TEST-X11 | **NOT CHECKED** |
| CB-08 | Відсутній priority: чи є Not Set п'ятим значенням? | **Ні**, це відсутність; тільки чотири значення для встановлення, без reset (D-03) | G3 §1, C-12, TEST-04.1 | **NOT CHECKED** |
| CB-09 | Important: High/Resolved, Critical/Resolved, Critical/Closed, Not Set/Open | Перші **два входять**; Closed і Not Set **не входять**. Resolved ≠ Closed | G3 §1, S-02-B, TEST-X06, TEST-08.1–08.4 | **NOT CHECKED** |
| CB-10 | Comment save failed | **Error і 0 нових comments**; не вигадувати успішне збереження | G3 C-18, T-21, TEST-06.5 | **NOT CHECKED** |
| CB-11 | Empty All та empty Important | Окремі стани **одного** S-02; без фальшивого issue чи нової продуктової сторінки | G3 S-02-C, TEST-02.5/TEST-X09 | **NOT CHECKED** |
| CB-12 | Назви і scope: US-03 AC, US-09, SR-10/11, NFR-03/04 | US-03 AC — ненумеровані пункти; US-09 Deferred; SR-10/11 Future; HTTPS/backup **не UI-екрани** | S1 §5/§8, G3 §6/§9 | **NOT CHECKED** |
| CB-13 | Чи може Member assign/reassign або priority, чи може Lead? | Лише Lead може assign/reassign (друга частина D-04) і priority (BR-06). Member controls disabled (D-05) | G3 §3, C-11/C-12/C-17, TEST-03.3/04.2 | **NOT CHECKED** |
| CB-14 | Return із S-03, відкритого з Important, після Closed | Повернення в Important (D-07), фільтр актуальний, Closed issue не видно | G2 T-23; G3 TEST-X07 | **NOT CHECKED** |

## C. Реєстр результатів незалежного контролю

| Finding | Source / evidence | Severity (BLOCKER/MAJOR/MINOR) | Required correction | Status |
|---|---|---|---|---|
| **PENDING** | — | — | — | NOT REVIEWED |

## D. Умова затвердження

1. Рецензент незалежно звірив S1, permission matrix, status matrix та кілька edge cases і **заповнив реальні** Reviewer, Date, Version, Accepted decisions, Open blockers, Result.
2. **Немає відкритих BLOCKER.** Якщо знайдено проблему, виправити мінімально, перевірити повторно і занести в журнал.
3. Лише **після фактичного прийняття плану людиною** змінити статус `01_Input_Pack_v1.0.md` і `03_Screen_Contracts_v1.0.md` на **APPROVED**, зазначивши посилання на протокол Control B.
4. Якщо незалежний рецензент недоступний, залишити **REVIEW / NOT APPROVED** і **не запускати Figma** за умовою методички.

**Примітка:** рецензування AI в цьому чаті не становить незалежного Control B. 45 сценаріїв G3 є test specifications і залишаються NOT RUN; Control B перевіряє план, не реалізацію.
