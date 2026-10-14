---
name: project-memory-manager
description: Maintain durable project context across Codex sessions by reading and updating a project-level .memory directory. Use when work spans multiple sessions or when project state, decisions, failures, environment, assets, or next steps should persist.
metadata:
  short-description: Maintain project memory across Codex sessions
---

# Project Memory Manager

Use this skill to preserve only project information that will change future engineering work. The project memory uses a hierarchy: a root `.memory/` for the umbrella project and an optional `.memory/` inside each subproject.

## Session start

1. Locate the umbrella project root from the current working directory and repository markers.
2. Determine the active subproject. Prefer an explicitly named subproject or the nearest ancestor containing a project marker (`.git`, `pyproject.toml`, `package.json`, `Cargo.toml`, `Makefile`, `src/`, or equivalent). Do not treat every dataset, cache, output, or arbitrary directory as a subproject.
3. Read the root `.memory/SUBPROJECTS.md` when it exists. Use it as the registry of subproject names, paths, relationships, and status.
4. Read the root `.memory/` overview files for umbrella context. Then read the active subproject's own `.memory/` files for detailed context. Never mix entries from sibling subprojects into the active subproject's state.
5. If a required `.memory/` directory does not exist, offer to initialize it from `assets/memory-template/`; create it when the user has asked for this skill or explicitly requested initialization.
6. Treat memory as context, not authority: verify stale paths, versions, and claims against the current workspace when practical.

## Subproject isolation

Keep umbrella concerns in the root `.memory/` and implementation-specific concerns in the active subproject's `.memory/`. A subproject memory has the same standard files as the root memory. Record cross-subproject dependencies in the root `SUBPROJECTS.md` and link to the affected subproject paths. When a task touches multiple subprojects, update each relevant memory separately and add a root summary only for shared decisions or relationships.

## Language for memory entries

Write all human-facing content stored in `.memory/` in Chinese. Keep filenames, API names, model names, software names, technical abbreviations, code identifiers, and path strings unchanged. This language rule applies to templates, examples, topic entries, and session summaries; it does not translate this skill's internal instructions.

## During work

Record an entry when information is durable and likely to prevent repeated analysis or mistakes:

- **Failures:** problem, cause, failed approaches, final fix, and what to avoid.
- **Decisions:** chosen design, reason, rejected alternatives, and when to revisit.
- **Environment:** OS, Python, CUDA, GPU, virtual environment, compiler/build tools. Record versions and paths, never credentials.
- **Assets:** code, dataset, model, checkpoint, output, and configuration paths.
- **Project state:** current milestone, working areas, known constraints, and risks.
- **TODO:** actionable unfinished work and dependencies.

Do not record ordinary conversation, transient thoughts, secrets, API keys, tokens, passwords, personal data, or copied sensitive configuration. Redact secrets if encountered.

Prefer concise dated entries. Keep one source of truth per topic and update existing entries instead of duplicating them. Preserve useful history when changing a decision or correcting a failure.

## Task completion

At the end of an important task, append a dated session summary to `SESSION_LOG.md` covering:

- completed work;
- modified or added files;
- newly learned durable information;
- problems and resolutions;
- recommended next steps.

Also update the topic files when the task changed project state, assets, decisions, failures, environment, or TODOs. If no durable information changed, do not create noise; a session log entry may state that briefly when a task summary is requested.

## File contract

Keep these files in `.memory/`:

- `PROJECT_STATE.md` — overall status and constraints.
- `ENVIRONMENT.md` — reproducible development environment.
- `ASSETS.md` — important project paths.
- `DECISIONS.md` — durable technical choices.
- `FAILURES.md` — errors and fixes.
- `SESSION_LOG.md` — chronological task summaries.
- `TODO.md` — current actionable work.
- `SUBPROJECTS.md` — root-only registry of subprojects and their relationships.

`SUBPROJECTS.md` is required only in the umbrella root memory. Each subproject memory uses the other seven standard files.

Use the templates in `assets/memory-template/` for initialization. The templates are deliberately plain Markdown so they are easy to modify or extend with experiment, dataset-version, report, or Git sections later.

## Safety and quality

Never infer that a memory entry is current solely because it exists. Mark stale information and refresh it. Do not run broad destructive cleanup of memory. When unsure whether information is durable, prefer a short note in the session summary and promote it to a topic file only if it will affect future work.
