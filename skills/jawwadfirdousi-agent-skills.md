---
title: "agent-skills"
url: "https://github.com/jawwadfirdousi/agent-skills"
description: "by [jawwadfirdousi](https://github.com/jawwadfirdousi) - Read-only PostgreSQL query skill for Claude Code. Executes SELECT/SHOW/EXPLAIN/WITH queries across configured databases with strict validation, timeouts, and row limits. Supports multiple connections with descriptions for database selection."
sourceRepo: "jawwadfirdousi/agent-skills"
tags: ["Claude Code", "IA", "Claude", "Skills", "Agents"]
date: 2026-02-13
language: "en"
stars: 2
forks: 1
---

# agent-skills

[![Mentioned in Awesome Claude Code](https://awesome.re/mentioned-badge.svg)](https://github.com/hesreallyhim/awesome-claude-code)

Reusable skill definitions.

## Available skills

- `read-only-postgres`: Run safe, read-only PostgreSQL queries.
- `read-only-gh-pr-review`: Review GitHub PRs using the gh CLI (read-only).

## Symlink a skill into your project

If your project expects skills under `skills/` (adjust paths as needed):

```bash
ln -s /path/to/agent-skills/skills/read-only-postgres /path/to/your-project/skills/read-only-postgres
ln -s /path/to/agent-skills/skills/read-only-gh-pr-review /path/to/your-project/skills/read-only-gh-pr-review
```
