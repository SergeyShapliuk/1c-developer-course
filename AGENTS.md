# Repository Guidelines

## Project Structure & Module Organization

This repository is a Russian-language Markdown course for 1С development. The root [README.md](README.md) contains the course overview and the lesson program of roughly 120 lessons, grouped into 10 stages. Lessons 1–52 are filled; later stages exist only as a roadmap.

Each written lesson uses its own numbered directory, for example `01-platform/` or `25-mini-project/`, containing exactly:

- `README.md` — lesson goal, outcome, and study route;
- `theory.md` — concepts and terminology;
- `practice.md` — beginner-friendly steps, result check, and final control questions.

Do not create directories for lessons 53 and later until the lesson is requested. There is currently no application source code, generated asset directory, or automated test suite.

## Content and Naming Conventions

Write in clear Russian for readers with no 1С experience. Introduce a term before using it, explain both the action and its purpose, and give exact UI paths such as **Конфигурация → Обновить конфигурацию базы данных**. Write keys in backticks: `F5`, `F7`, `F9`, `F11`.

Address lessons as «Занятие N», never «День N». Lesson links must be relative, for example `[Занятие 1](01-platform/README.md)`.

Use two-digit, lowercase, hyphenated directory names: `11-bsl-syntax/`. Keep lesson filenames lowercase and fixed as `README.md`, `theory.md`, and `practice.md`.

A lesson `README.md` has exactly five sections: `# Занятие N. Название`, `## Цель`, `## Результат занятия`, `## Маршрут`, `## Ключевые термины`.

A `practice.md` always carries three things: the practical task, a result check, and control questions.

Use Markdown headings, ordered lists for procedures, and fenced code blocks only for actual code or commands — never for ordinary prose. Tag fences by language: ```bsl for the 1С built-in language, ```bash for Git commands, ```powershell for PowerShell, ```text for a data-flow diagram (see the applied standard below).

Put `## Контрольные вопросы` at the end of every `practice.md`. The one exception is a checkpoint lesson (lesson 25 and the lesson closing each later stage), whose `practice.md` uses this fixed order instead:

1. `## Самостоятельная задача`
2. `## Критерии готовности`
3. `## Чек-лист проверки`
4. `## Контрольные вопросы`
5. `## Типичные ошибки`
6. `## Разбор и эталонный вариант`

**Disclosed-concepts rule.** The practice of lesson N may use only concepts explained in lessons 1..N. Documents, tabular sections, registers, posting, movements, queries, and the data composition system must not appear in the practices of lessons 1–25 at all — those topics belong to stages 3–6. Registers, posting and movements must not appear in the practices of lessons 26–38 either: stage 3 is documents only. Queries, temporary tables, register virtual tables and the data composition system must not appear anywhere in lessons 26–52 — balances in stage 4 are checked through the register’s standard list form, never a query.

## Lessons 26 and Later: Applied Standard

From lesson 26 the course stops teaching isolated mechanisms and builds one continuous project story. Stage 3 (26–38) is documents; stage 4 (39–52) is registers and posting. By lesson 38 the chain «Заявка → ввод на основании → Поступление» works; by lesson 52 the chain «Поступление → проведение → движения → остаток» works.

1. **Five questions per lesson.** Every lesson of stages 3–4 answers: which business problem we solve; which 1С mechanism that needs; where the logic belongs; what changes in our system; how to verify the solution really works. A `theory.md` opens with the business problem, never with the name of a mechanism.
2. **Task before interface.** Never open a lesson with a configurator path. State the project's need, then ask which metadata object fits, and only then give the path **Конфигурация → Документы → Добавить**.
3. **One continuous scenario.** Each practice extends the same configuration instead of inventing a throwaway example. Scenario objects: `ЗаявкаНаМатериалы`, `ПоступлениеМатериалов`, `ПередачаМатериалов`, `ЦеныМатериалов`, `ОстаткиМатериалов`.
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
rg -n -i 'ВЫБРАТЬ |Новый Запрос|СхемаКомпоновки|ВиртуальнаяТаблица' --glob '[2-5][0-9]-*/practice.md'
```

Confirm every practice still ends with its control questions:

```powershell
Get-ChildItem */practice.md | ForEach-Object { if (-not (Select-String -Path $_ -Pattern '^## Контрольные вопросы' -Quiet)) { "MISSING: $_" } }
```

Review rendered lists and tables for readable spacing and ensure practice instructions match the current project: **«Управление строительной компанией с логистикой»**.

## Commits and Pull Requests

Use short imperative messages, for example `Add lesson 26 documents`, `Clarify lesson 7 practice`, or `Restructure course foundation through lesson 25`.

Keep each commit focused on one lesson or documentation correction, unless a restructuring explicitly spans several lessons. Pull requests should summarize affected lessons, note validation performed, and call out changes to the course roadmap. Do not commit `.idea/` files or run `git push` without explicit user authorization.
