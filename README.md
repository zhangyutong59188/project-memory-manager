# project-memory-manager

A Codex skill for maintaining durable project context across sessions, including project state, decisions, failures, environment details, assets, TODOs, and session summaries.

## Features

- Supports an umbrella project with multiple independent subprojects.
- Reads root `.memory/` context and the active subproject's `.memory/` context separately.
- Maintains a root `SUBPROJECTS.md` registry for paths, status, and dependencies.
- Writes human-facing memory content in Chinese while preserving technical names, paths, and identifiers.
- Avoids storing passwords, API keys, tokens, or private configuration.

## Install

Copy this directory into your Codex skills directory:

```bash
cp -R project-memory-manager ~/.codex/skills/
```

## Use

Invoke explicitly with:

```text
$project-memory-manager
```

Use it from the umbrella project root for cross-project work, or from a subproject directory to load that subproject's own `.memory/` first.

## Layout

```text
project-memory-manager/
├── SKILL.md
├── agents/openai.yaml
├── assets/memory-template/
└── references/usage.md
```

## License

MIT. See [LICENSE](LICENSE).
