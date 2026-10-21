# Repository Guidelines

## Project Structure & Module Organization

This repository is a Russian-language Markdown course for 1С development. The root [README.md](README.md) contains the course overview and the lesson program of roughly 120 lessons, grouped into 10 stages. All lessons 1–120 are filled; the program is complete.

Each written lesson uses its own numbered directory, for example `01-platform/` or `25-mini-project/`, containing exactly:

- `README.md` — lesson goal, outcome, and study route;
- `theory.md` — concepts and terminology;
- `practice.md` — beginner-friendly steps, result check, and final control questions.

Do not create directories for lessons 121 and later unless the user explicitly requests new lessons. There is currently no application source code, generated asset directory, or automated test suite.

## Content and Naming Conventions

Write in clear Russian for readers with no 1С experience. Introduce a term before using it, explain both the action and its purpose, and give exact UI paths such as **Конфигурация → Обновить конфигурацию базы данных**. Write keys in backticks: `F5`, `F7`, `F9`, `F11`.

Address lessons as «Занятие N», never «День N». Lesson links must be relative, for example `[Занятие 1](01-platform/README.md)`.

Use two-digit, lowercase, hyphenated directory names: `11-bsl-syntax/`; from lesson 100 the number has three digits: `100-project-repository/`. Keep lesson filenames lowercase and fixed as `README.md`, `theory.md`, and `practice.md`.

A lesson `README.md` has exactly five sections: `# Занятие N. Название`, `## Цель`, `## Результат занятия`, `## Маршрут`, `## Ключевые термины`.

A `practice.md` always carries three things: the practical task, a result check, and control questions.

Use Markdown headings, ordered lists for procedures, and fenced code blocks only for actual code or commands — never for ordinary prose. Tag fences by language: ```bsl for the 1С built-in language and for query text, ```bash for Git commands, ```powershell for PowerShell, ```text for a data-flow diagram (see the applied standard below).

Put `## Контрольные вопросы` at the end of every `practice.md`. The one exception is a checkpoint lesson (lesson 25 and the lesson closing each later stage), whose `practice.md` uses this fixed order instead:

1. `## Самостоятельная задача`
2. `## Критерии готовности`
3. `## Чек-лист проверки`
4. `## Контрольные вопросы`
5. `## Типичные ошибки`
6. `## Разбор и эталонный вариант`

**Disclosed-concepts rule.** The practice of lesson N may use only concepts explained in lessons 1..N. Documents, tabular sections, registers, posting, movements, queries, and the data composition system must not appear in the practices of lessons 1–25 at all — those topics belong to stages 3–6. Registers, posting and movements must not appear in the practices of lessons 26–38 either: stage 3 is documents only. Queries, temporary tables, register virtual tables and the data composition system must not appear anywhere in lessons 26–52 — balances in stage 4 are checked through the register’s standard list form, never a query. Stage 5 (53–68) introduces the query language one construct at a time: the practice of lesson N uses only query constructs introduced in lessons 53..N, and register virtual tables start at lesson 64. The data composition system, reports, templates, event subscriptions and roles must not appear in the practices of lessons 53–68. Stage 6 (69–80) introduces reports and the data composition system one capability at a time: the practice of lesson N uses only capabilities introduced in lessons 69..N, and report code (`ПриКомпоновкеРезультата`, the template composer and composition processors) starts at lesson 79. Tabular-document templates and print forms (`ПолучитьМакет`, `ПолучитьОбласть`), event subscriptions and roles must not appear in the practices of lessons 69–80; report code reaches its schema through the report object's `СхемаКомпоновкиДанных` property. Stage 7 (81–90) introduces form behavior and print forms one mechanism at a time: the practice of lesson N uses only form and printing mechanisms introduced in lessons 81..N, and tabular-document templates and print forms (`ПолучитьМакет`, `ПолучитьОбласть`, `ТабличныйДокумент`) start at lesson 87. Roles, access rights, event subscriptions and configuration extensions must not appear in the practices of lessons 81–90 — they belong to stage 8. Dialogs are non-modal only: `ПоказатьВопрос` with `ОписаниеОповещения`, never `Вопрос(` or `Предупреждение(`. Stage 8 (91–98) introduces administration one mechanism at a time: users and roles from lesson 91, rights checks in code from lesson 93, session parameters from lesson 94, record-level restrictions from lesson 95, the event log from lesson 96, configuration files and extensions from lesson 97. Every stage 8 practice that changes roles, users or structure starts with a `.dt` backup. Training passwords stay empty, and the lessons say so explicitly as technical debt. Stage 9 (99–110) introduces team development and testing one practice at a time: the project repository and configuration dumps from lesson 100, task branches from lesson 101, the shared bare repository, `push`, `fetch`, `pull` and `merge` from lesson 102, pull requests, the configuration **Версия** property and `git tag` from lesson 103, the configuration repository (хранилище конфигурации) only from lesson 105, explicit transactions (`НачатьТранзакцию`, `ОтменитьТранзакцию`) and the test processing from lesson 108, conditional breakpoints and stop-on-error from lesson 109. The second developer, Орлов Дмитрий, is played by the learner in a second clone. GitHub is optional, as in lesson 10: every stage 9 practice works offline, and GitHub steps are marked as an additional part. Every stage 9 practice that loads configuration from files or changes structure starts with a `.dt` backup. Stage 10 (111–120) introduces no new platform mechanisms: exam tickets (111–116) ask only about concepts taught in lessons 1–98, every answer key row names the lesson that teaches the fact, the questions are written for the course and never copied from the official 1С exam materials, the correct answers in a ticket are spread over different letters, and the answer key comes after the questions and before `## Контрольные вопросы`. Exam statements must agree with the lessons they cite; where the platform behavior was not verified, the lesson says so. Experiments that verify an answer run in `УчебнаяКонсоль`, inside a cancelled transaction when they write data, and end with a clean `git status`. Exam conditions (number of questions, time, pass mark) are given as of the time of writing, with an instruction to check them on the 1С site. Career lessons (117–119) never put real personal data in the course; resume files live outside public repositories. Lesson 120 is the final checkpoint; the document `ВозвратМатериалов` appears only there.

## Lessons 26 and Later: Applied Standard

From lesson 26 the course stops teaching isolated mechanisms and builds one continuous project story. Stage 3 (26–38) is documents; stage 4 (39–52) is registers and posting; stage 5 (53–68) is the query language; stage 6 (69–80) is reports and the data composition system; stage 7 (81–90) is forms, interface and print forms; stage 8 (91–98) is rights, roles and administration; stage 9 (99–110) is team development, the change lifecycle and testing; stage 10 (111–120) is certification and career preparation. By lesson 38 the chain «Заявка → ввод на основании → Поступление» works; by lesson 52 the chain «Поступление → проведение → движения → остаток» works; by lesson 68 the balance is obtained by a query, and a transfer beyond the balance is not posted; by lesson 80 the supply summary of lesson 68 is a DCS report the user opens from **Логистика**, configures without a developer, and reconciles with the lesson 68 function; by lesson 90 the documents have journals that show and highlight what matters, forms that offer only allowed actions and values, and print forms — request, waybill, receipt order — printed from the form and from the journal, one document or a batch; by lesson 98 every user works under roles built by function, storekeepers and site foremen see only the documents of their warehouse or construction site, approval is reserved for the head of supply, and the event log answers who did what; by lesson 110 the configuration lives in the Git repository `construction-erp` as a text dump, every change goes «карточка задачи → ветка → коммиты → тесты → pull request → ревью → слияние → версия → поставка .cf», and posting and balances are covered by manual test cases and by the processing `ТестыСнабжения`, which checks them in seconds and leaves no data behind; by lesson 120 the learner has passed four training tickets and a timed mock exam, has a portfolio README verified by deploying an empty base from it, a resume and a rehearsed interview, and has delivered the materials return document as version `1.3.0` through the full lifecycle.

1. **Five questions per lesson.** Every lesson of stages 3–9 answers: which business problem we solve; which 1С mechanism that needs; where the logic belongs; what changes in our system; how to verify the solution really works. A `theory.md` opens with the business problem, never with the name of a mechanism. In stage 10 the «business problem» is the learner's own situation — the exam, the employer, the interview — and each lesson still says how to verify the result.
2. **Task before interface.** Never open a lesson with a configurator path. State the project's need, then ask which metadata object fits, and only then give the path **Конфигурация → Документы → Добавить**.
3. **One continuous scenario.** Each practice extends the same configuration instead of inventing a throwaway example. Scenario objects: `ЗаявкаНаМатериалы`, `ПоступлениеМатериалов`, `ПередачаМатериалов`, `ЦеныМатериалов`, `ОстаткиМатериалов`; from stage 6 also the reports `ОстаткиНаСкладах`, `ОборотнаяВедомостьМатериалов`, `ВыдачаПоОбъектам`, `ОбеспечениеОбъектов`; from stage 7 also the processing `ПанельСнабженца`, the list forms of `ЗаявкаНаМатериалы` and `ПоступлениеМатериалов`, and the templates `ПФ_Заявка`, `ПФ_Накладная`, `ПФ_ПриходныйОрдер`; from stage 8 also the roles `ПолныеПрава`, `БазовыеПрава`, `Кладовщик`, `Снабженец`, `СогласованиеЗаявок`, `Прораб`, the common module `ПраваПользователей`, the session parameters `ТекущийСотрудник`, `ТекущийСклад`, `ТекущийОбъектСтроительства` and the extension `ДоработкиСнабжения`; from stage 9 also the attribute `Завершен` of `ОбъектыСтроительства`, the processing `ТестыСнабжения`, the function `ОстаткиМатериалов` of the common module `ОстаткиМатериаловСервер`, the handler `ОбработкаУдаленияПроведения` of `ПоступлениеМатериалов`, the repository `construction-erp` with its server `server/construction-erp.git` and Орлов's clone `construction-erp-orlov`, and the bases `УСК_Тест` and `УСК_Рабочая`; in stage 10 also the project `README.md` with `docs/decisions.md` and `docs/releases`, and, in lesson 120 only, the document `ВозвратМатериалов`. Report names intentionally differ from register names.
4. **One architectural question.** Every practice includes at least one control question about placing logic: form module, object module or common module; client or server.
5. **20/80 proportion.** Keep new BSL constructs to a minimum; spend the lesson on the platform mechanism and on why the logic lives exactly there.
6. **Materials live in `Товары`.** There is no `Номенклатура` catalog: the tabular section `Материалы` references the catalog `Товары` created in lesson 6. Do not rename it.
7. **Diagrams.** At most one ASCII diagram per lesson, only for a data flow, in a ```text fence. Lessons 1–25 contain none; structures are shown with lists and tables.

Keep the main roadmap current. Do not mark course-status checkboxes as completed unless explicitly directed.

## Validation and Local Development

No build step is required. Before handing off content, run these checks from the repository root:

```powershell
rg --files -g '*.md' | Sort-Object
git diff --check
```

Verify every changed relative Markdown link resolves to an existing file. Check that no practice of lessons 1–25 leaks a later topic:

```powershell
rg -n -i 'табличн|РегистрСведений|РегистрНакопления|регистратор|провед|СхемаКомпоновки' --glob '[01][0-9]-*/practice.md' --glob '2[0-5]-*/practice.md'
```

Check that no practice of lessons 26–38 leaks a stage 4 topic. Three kinds of hit are acceptable and must be confirmed by eye; anything else is a leak:

- a statement that the document's **Проведение** property stays off, which every stage 3 practice is expected to make;
- the mandatory handler signature `Процедура ПередЗаписью(Отказ, РежимЗаписи, РежимПроведения)`, whose third parameter the platform always passes and the lesson explicitly leaves unused;
- the mention of the still-unavailable **Провести** command in lesson 34.


```powershell
rg -n -i 'РегистрСведений|РегистрНакопления|регистратор|провед|Движени' --glob '2[6-9]-*/practice.md' --glob '3[0-8]-*/practice.md'
```

Check that no practice of lessons 26–52 uses queries or the data composition system:

```powershell
rg -n 'ВЫБРАТЬ |Новый Запрос|СхемаКомпоновки|ВиртуальнаяТаблица' --glob '2[6-9]-*/practice.md' --glob '[34][0-9]-*/practice.md' --glob '5[0-2]-*/practice.md'
```

Check that no practice of lessons 53–68 leaks a stage 6–8 topic:

```powershell
rg -n -i 'СхемаКомпоновки|КомпоновщикМакета|ПодпискаНаСобытие|ПолучитьМакет' --glob '5[3-9]-*/practice.md' --glob '6[0-8]-*/practice.md'
```

Check that no practice of lessons 69–80 leaks a stage 7–8 topic, and that report code does not appear before lesson 79:

```powershell
rg -n -i 'ПолучитьМакет|ПолучитьОбласть|ПодпискаНаСобытие|РольДоступна|ПравоДоступа' --glob '69-*/practice.md' --glob '7[0-9]-*/practice.md' --glob '80-*/practice.md'
rg -n 'ПриКомпоновкеРезультата|КомпоновщикМакета|ПроцессорКомпоновки' --glob '69-*/practice.md' --glob '7[0-8]-*/practice.md'
```

Check that no practice of lessons 81–90 leaks a stage 8 topic or a modal dialog, and that templates do not appear before lesson 87:

```powershell
rg -n -i 'РольДоступна|ПравоДоступа|ПодпискаНаСобытие|Расширени' --glob '8[1-9]-*/practice.md' --glob '90-*/practice.md'
rg -n '\bВопрос\(|\bПредупреждение\(' --glob '8[1-9]-*/practice.md' --glob '90-*/practice.md'
rg -n 'ПолучитьМакет|ПолучитьОбласть|ТабличныйДокумент' --glob '8[1-6]-*/practice.md'
```

In the second command, the only acceptable hit is the lesson 83 sentence that names the forbidden modal call; confirm it by eye.

Check that stage 8 mechanisms do not appear before the lesson that introduces them:

```powershell
rg -n 'ПараметрыСеанса|УстановкаПараметровСеанса' --glob '9[1-3]-*/practice.md'
rg -n 'ГДЕ .*&Текущ|РАЗРЕШЕННЫЕ' --glob '9[1-4]-*/practice.md'
rg -n 'ЗаписьЖурналаРегистрации' --glob '9[1-5]-*/practice.md'
rg -n '&Перед\(|&После\(|&Вместо\(' --glob '9[1-6]-*/practice.md'
```

Check that stage 9 practices do not appear before the lesson that introduces them:

```powershell
rg -n 'git (push|pull|fetch|merge)|--bare' --glob '99-*/practice.md' --glob '10[01]-*/practice.md'
rg -n 'git tag' --glob '99-*/practice.md' --glob '10[0-2]-*/practice.md'
rg -n 'Хранилище конфигурации' --glob '99-*/practice.md' --glob '10[0-4]-*/practice.md'
rg -n 'НачатьТранзакцию|ТестыСнабжения' --glob '99-*/practice.md' --glob '10[0-7]-*/practice.md'
rg -n 'Остановка по ошибке' --glob '99-*/practice.md' --glob '10[0-8]-*/practice.md'
```

In stage 9 the modal `Вопрос(` may appear only in lesson 104, as a defect the review must find.

Check that the final checkpoint document does not leak into earlier stage 10 lessons:

```powershell
rg -n 'ВозвратМатериалов' --glob '11[1-9]-*/*.md'
```

For every exam ticket (111–116), confirm by eye that each answer key row names a lesson, that the cited lesson states the same fact, and that the correct answers are spread over different letters.

Confirm every practice still ends with its control questions:

```powershell
Get-ChildItem */practice.md | ForEach-Object { if (-not (Select-String -Path $_ -Pattern '^## Контрольные вопросы' -Quiet)) { "MISSING: $_" } }
```

Review rendered lists and tables for readable spacing and ensure practice instructions match the current project: **«Управление строительной компанией с логистикой»**.

## Commits and Pull Requests

Use short imperative messages, for example `Add lesson 26 documents`, `Clarify lesson 7 practice`, or `Restructure course foundation through lesson 25`.

Keep each commit focused on one lesson or documentation correction, unless a restructuring explicitly spans several lessons. Pull requests should summarize affected lessons, note validation performed, and call out changes to the course roadmap. Do not commit `.idea/` files or run `git push` without explicit user authorization.
