# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

**Генеративный ИИ в бизнесе** — блог о применении генеративного ИИ в SMB: от создания контента до governance и compliance. Статический сайт на Astro 6, проект курса Claude Code Basics. Контент на русском языке.

Проект в стадии начального шаблона и будет развиваться по ступеням курса. Тестов и линтеров нет, добавятся на следующих ступенях.

**При создании статей** — читай `EDITORIAL.md` в корне проекта (целевая аудитория, тематика, стиль, объём).

## Commands

```bash
npm run dev       # Dev-сервер на :4321
npm run build     # Production-сборка в dist/
npm run preview   # Предпросмотр сборки
```

Требуется Node >= 22.12.0.

## Architecture

**Astro 6** статический сайт с интеграциями: `@astrojs/mdx`, `@astrojs/sitemap`, `@astrojs/rss`.

Маршруты — в `src/pages/`, отдельная статья через catch-all `[...slug]`. Layout статей — `src/layouts/BlogPost.astro`. Глобальные константы (`SITE_TITLE`, `SITE_DESCRIPTION`) — в `src/consts.ts`, их нужно обновить под текущий фокус проекта («Генеративный ИИ в бизнесе» вместо «AI Digest»).

### Content Layer

Статьи хранятся в `src/content/blog/` как `.md`/`.mdx`. Схема frontmatter определена в `src/content.config.ts` через Zod.

Для добавления новой статьи — создать `.md` файл с frontmatter:

```markdown
---
title: 'Заголовок статьи'
description: 'Краткое описание в 2–3 предложения.'
pubDate: '2026-04-05'
tags: ['llm', 'anthropic']
source: 'https://example.com/original-article'
---

Текст статьи. 300–500 слов.
```

Обязательные поля: `title`, `description`, `pubDate`. Опциональные: `updatedDate`, `heroImage`, `source`, `tags`.

## Key Conventions

- TypeScript strict mode (`astro/tsconfigs/strict` + `strictNullChecks`)
