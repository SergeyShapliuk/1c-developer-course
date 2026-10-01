# Repository Guidelines

## Project Structure & Module Organization

This repository is a Russian-language Markdown course for 1С development. The root [README.md](README.md) contains the course overview and the lesson program of roughly 120 lessons, grouped into 10 stages. Lessons 1–25 are filled; later stages exist only as a roadmap.

Each written lesson uses its own numbered directory, for example `01-platform/` or `25-mini-project/`, containing exactly:

- `README.md` — lesson goal, outcome, and study route;
- `theory.md` — concepts and terminology;
- `practice.md` — beginner-friendly steps, result check, and final control questions.

Do not create directories for lessons 26 and later until the lesson is requested. There is currently no application source code, generated asset directory, or automated test suite.

## Content and Naming Conventions

Write in clear Russian for readers with no 1С experience. Introduce a term before using it, explain both the action and its purpose, and give exact UI paths such as **Конфигурация → Обновить конфигурацию базы данных**. Write keys in backticks: `F5`, `F7`, `F9`, `F11`.

Address lessons as «Занятие N», never «День N». Lesson links must be relative, for example `[Занятие 1](01-platform/README.md)`.

Use two-digit, lowercase, hyphenated directory names: `11-bsl-syntax/`. Keep lesson filenames lowercase and fixed as `README.md`, `theory.md`, and `practice.md`.

A lesson `README.md` has exactly five sections: `# Занятие N. Название`, `## Цель`, `## Результат занятия`, `## Маршрут`, `## Ключевые термины`.

A `practice.md` always carries three things: the practical task, a result check, and control questions.

Use Markdown headings, ordered lists for procedures, and fenced code blocks only for actual code or commands — never for ordinary prose. Tag fences by language: ```bsl for the 1С built-in language, ```bash for Git commands, ```powershell for PowerShell.

Put `## Контрольные вопросы` at the end of every `practice.md`. The one exception is a checkpoint lesson (lesson 25 and the lesson closing each later stage), whose `practice.md` uses this fixed order instead:

1. `## Самостоятельная задача`
2. `## Критерии готовности`
3. `## Чек-лист проверки`
4. `## Контрольные вопросы`
5. `## Типичные ошибки`
6. `## Разбор и эталонный вариант`

**Disclosed-concepts rule.** The practice of lesson N may use only concepts explained in lessons 1..N. Documents, tabular sections, registers, posting, movements, queries, and the data composition system must not appear in the practices of lessons 1–25 at all — those topics belong to stages 3–6.

Keep the main roadmap current. Do not mark course-status checkboxes as completed unless explicitly directed.

## Validation and Local Development

No build step is required. Before handing off content, run these checks from the repository root:

```powershell
rg --files -g '*.md' | Sort-Object
git diff --check
```

Verify every changed relative Markdown link resolves to an existing file. Check that no practice of lessons 1–25 leaks a later topic:

```powershell
rg -n -i 'табличн|РегистрСведений|РегистрНакопления|регистратор|провед|СхемаКомпоновки' --glob '*/practice.md'
```

Confirm every practice still ends with its control questions:

```powershell
Get-ChildItem */practice.md | ForEach-Object { if (-not (Select-String -Path $_ -Pattern '^## Контрольные вопросы' -Quiet)) { "MISSING: $_" } }
```

Review rendered lists and tables for readable spacing and ensure practice instructions match the current project: **«Управление строительной компанией с логистикой»**.

## Commits and Pull Requests

Use short imperative messages, for example `Add lesson 26 documents`, `Clarify lesson 7 practice`, or `Restructure course foundation through lesson 25`.

Keep each commit focused on one lesson or documentation correction, unless a restructuring explicitly spans several lessons. Pull requests should summarize affected lessons, note validation performed, and call out changes to the course roadmap. Do not commit `.idea/` files or run `git push` without explicit user authorization.
