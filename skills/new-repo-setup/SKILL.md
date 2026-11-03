---
name: new-repo-setup
description: Set up a repository with the standard agent docs — AGENTS.md from the bundled template, a CLAUDE.md pointer, and the docs/ scaffold (architecture, glossary, known pitfalls, specs index). Use when starting a new repo or adding the agent conventions to an existing one.
argument-hint: "[target repo path]"
---

# New repository setup

Bring a repository in line with `templates/AGENTS.md` next to this skill. That file is the single source of truth — always read it fresh, never work from memory of it.

Target: `$ARGUMENTS` if given, else the current working directory. Confirm the resolved path once before writing anything.

## 1. Inspect the target

- Existing files: `AGENTS.md`, `CLAUDE.md`, `README.md`, `docs/`. Never overwrite one; if present, merge in what is missing and show the user the diff.
- Stack and commands — if the repository already contains configs / code infer from that, otherwise ask the user.
- Purpose: from `README.md`, package description or repo name.

Ask the user only for what you could not infer (typically Purpose for an empty repo). One question round, all gaps at once.

## 2. AGENTS.md

Copy the template and fill the placeholders:

- `Purpose: <...>` → one sentence.
- `Stack: <...>` → language, framework, key libraries.
- `Test` / `Lint` / `Run` → the exact commands. If one genuinely does not exist yet, write `n/a` rather than inventing one.

> [!NOTE]
> also consider adding information about a `Screenshots` Script to update Screenshots that can be used by the Agent and README if the Repository includes visual elements.

Keep every other section verbatim.

## 3. CLAUDE.md

Create `CLAUDE.md` containing exactly:

```
@AGENTS.md
```

## 4. docs/ scaffold

Create every document listed in the template's Orientation table that does not exist yet, using the files in `templates/` next to this skill:

| Target                   | Source                        |
| ------------------------ | ----------------------------- |
| `docs/architecture.md`   | `templates/architecture.md`   |
| `docs/glossary.md`       | `templates/glossary.md`       |
| `docs/known-pitfalls.md` | `templates/known-pitfalls.md` |
| `docs/specs/README.md`   | `templates/specs-README.md`   |

For an existing codebase, fill `architecture.md` with a short real overview (entry points, main modules, data flow) instead of leaving placeholders, and seed `glossary.md` with obvious domain terms you met while inspecting. For an empty repo, leave the placeholders.

If the Orientation table in the template lists a document with no matching file in `templates/`, create it with a heading and the "Why" text from the table.

If `README.md` is missing, create a minimal one: title and the Purpose sentence.

## 5. Finish

- Ask the user to `git init` if not yet initialized.
- Do not commit or push unless asked.
- Report: files created, files merged (with what changed), inferred Stack/commands and where each came from, and anything left as a placeholder.
