<div align="center">

# project-memory-manager

**Durable project context for Codex across multiple sessions.**

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Codex Skill](https://img.shields.io/badge/Codex-Skill-6E56CF)](SKILL.md)

[中文说明](README.md) · [Usage](references/usage.md)

</div>

`project-memory-manager` keeps durable project context in versionable Markdown files: project state, decisions, failures, environment, assets, TODOs, and session summaries.

## Highlights

- Cross-session project memory.
- Root project and independent subproject memory isolation.
- Chinese human-facing memory entries while preserving technical names and paths.
- Secret-safe by default: do not store passwords, API keys, tokens, or private configuration.
- Plain Markdown templates that are easy to review and extend.

## Install

```bash
cp -R project-memory-manager ~/.codex/skills/
```

Invoke in Codex:

```text
$project-memory-manager
Read the current project memory, then continue this task.
```

See [SKILL.md](SKILL.md) and [usage.md](references/usage.md) for the full workflow.

## License

MIT. See [LICENSE](LICENSE).
