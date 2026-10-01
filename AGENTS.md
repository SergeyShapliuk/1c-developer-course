# Repository Guidelines

## Project Structure & Module Organization

This repository is a Russian-language Markdown course for 1С development. The root [README.md](README.md) contains the course overview and 30-day roadmap. Each completed lesson uses its own numbered directory, for example `01-basics/` or `08-material-requests/`, containing exactly:

- `README.md` — lesson goal, outcome, and study route;
- `theory.md` — concepts and terminology;
- `practice.md` — beginner-friendly steps and final control questions.

Do not create directories for future lessons until the lesson is requested. There is currently no application source code, generated asset directory, or automated test suite.

## Content and Naming Conventions

Write in clear Russian for readers with no 1С experience. Introduce a term before using it, explain both the action and its purpose, and give exact UI paths such as **Конфигурация → Обновить конфигурацию базы данных**.

Use two-digit, lowercase, hyphenated directory names: `09-information-registers/`. Keep lesson filenames lowercase and fixed as `README.md`, `theory.md`, and `practice.md`. Use Markdown headings, ordered lists for procedures, and fenced code blocks only for actual code or commands. Put `## Контрольные вопросы` at the end of every `practice.md`.

Keep the main roadmap current. Lesson links must be relative, for example `[День 1](01-basics/README.md)`. Do not mark course-status checkboxes as completed unless explicitly directed.

## Validation and Local Development

No build step is required. Before handing off content, run these checks from the repository root:

```powershell
rg --files -g '*.md' | Sort-Object
git diff --check
```

Verify every changed relative Markdown link resolves to an existing file. Review rendered lists and tables for readable spacing and ensure practice instructions match the current project: **«Управление строительной компанией с логистикой»**.

## Commits and Pull Requests

The visible history contains only `Initial commit`, so no repository-specific commit convention exists yet. Use short imperative messages, for example `Add day 9 information registers` or `Clarify day 7 practice`.

Keep each commit focused on one lesson or documentation correction. Pull requests should summarize affected days, note validation performed, and call out changes to the course roadmap. Do not commit `.idea/` files or run `git push` without explicit user authorization.
