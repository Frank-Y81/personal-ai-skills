# Personal AI Skills

A small, platform-agnostic repository of reusable AI skills.

The repository is designed around one simple idea: a skill's content should be independent from the agent that loads it.

## Current Status

The repository currently contains one skill:

- `shopping` — rational purchase decision-making

Additional skills can be added later when they are actually needed.

## Roles

### Local repository

The local Git working copy is the development and runtime source for local agents.

Claude and Hermes should read skills directly from the local filesystem. Editing and saving a local `SKILL.md` should make the latest version available to the local agent without downloading the skill from GitHub.

### GitHub

GitHub stores the version-controlled, published copy of the skills.

It is used for:

- version history
- publishing a version after local testing
- remote access for web-based AI when available

GitHub is **not** a runtime dependency for local skill loading.

### Web AI

Web-based AI such as ChatGPT or Kimi may be asked to inspect this repository and use a named skill, for example:

> Go to `Frank-Y81/personal-ai-skills`, find the `shopping` skill, and follow it for this task.

Actual access depends on the capabilities of the specific AI service.

## Directory Structure

```text
personal-ai-skills/
├── README.md
├── registry/
│   └── skills.json
├── skills/
│   └── shopping/
│       └── SKILL.md
└── tests/
    └── README.md
```

Future skills can follow the same structure:

```text
skills/
└── <skill-name>/
    └── SKILL.md
```

If a skill eventually needs substantial supporting material, it may later add directories such as `references/` or `scripts/`. They are intentionally not created until needed.

## Adding a Skill

1. Create `skills/<skill-name>/SKILL.md`.
2. Add its metadata to `registry/skills.json`.
3. Test it locally with the agents that will use it.
4. Commit and push after you are satisfied with the result.

## Modifying a Skill

1. Edit the local `SKILL.md`.
2. Test the change locally with Claude and/or Hermes.
3. Update the skill version when appropriate.
4. Commit and push when you decide to publish the change.

There is currently no separate development, staging, or runtime copy. For this single-user workflow, the local working copy is both the development and local runtime source; GitHub represents the published version.

## Skill Format

Each skill uses a `SKILL.md` with lightweight metadata:

```markdown
---
name: <skill-name>
description: <short description>
version: <MAJOR.MINOR.PATCH>
---
```

The body should contain only the instructions and decision logic that are specific to that skill. It should not depend on Claude, Hermes, or another specific agent unless the skill itself is intentionally agent-specific.

## Versioning

Versions use `MAJOR.MINOR.PATCH`:

- **MAJOR** — core behavior changes significantly
- **MINOR** — meaningful capability is added
- **PATCH** — small fixes or clarifications

## Design Principles

1. **One local source** — avoid maintaining duplicate copies of the same skill.
2. **Platform-agnostic skill content** — keep agent-specific loading outside the skill itself.
3. **Explicit invocation** — skills are used when explicitly requested rather than through a complex automatic router.
4. **Local-first** — local agents should not fetch skills from GitHub during normal runtime.
5. **No unnecessary engineering** — do not add adapters, sync systems, multiple environments, or APIs until a real need appears.
6. **Progressive disclosure when needed** — keep the main skill concise and move substantial optional material out only when the skill genuinely requires it.
