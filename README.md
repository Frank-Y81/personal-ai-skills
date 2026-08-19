# Personal AI Skills

A platform-agnostic registry of AI skills, designed to be shared across multiple AI agents (Claude, Hermes, and future agents) without coupling skills to any specific platform.

## Why Skill-Agent Separation?

Different AI agents have different runtime environments, tool ecosystems, and capabilities. If a skill is written for a specific agent, it becomes locked to that agent and cannot be reused. By keeping skills platform-agnostic and separating them from agent-specific loading logic, we achieve:

- **Portability**: Any agent that can read Markdown can use these skills.
- **Consistency**: All agents follow the same decision logic for the same task.
- **Maintainability**: Skills are updated in one place, not duplicated across agent configurations.
- **Testability**: The same test cases can validate behavior across agents.

## Roles

### GitHub (Canonical Source)

- Stores the stable, versioned release of all skills.
- Serves as the source of truth for skill content.
- Provides remote access for web-based AI (GPT, Kimi, etc.) to read skills.
- **Is not** a runtime dependency for local agents.

### Local Agent (Claude, Hermes, etc.)

- Reads skill files directly from the local filesystem.
- Does **not** access GitHub at runtime because of skills.
- Syncs from GitHub manually or through a separate process (future), but once synced, operates fully offline.
- Agent-specific loading logic (how to read, parse, and apply a skill) lives in the agent's own configuration, not in this repository.

### Web AI (GPT, Kimi, etc.)

- Can read skills from GitHub URLs.
- Operates on the stable version published in the repository.
- Cannot execute skills that require local tools or filesystem access.
- Useful for consultation and analysis tasks.

## Directory Structure

```
personal-ai-skills/
├── README.md              # This file
├── registry/
│   └── skills.json        # Skill index (metadata only, no full content)
├── skills/
│   ├── shopping/
│   │   └── SKILL.md       # Rational purchase decision-making
│   ├── research/
│   │   └── SKILL.md       # Structured research and evidence evaluation
│   └── writing/
│       └── SKILL.md       # Writing and rewriting
└── tests/
    └── README.md          # Testing guidelines
```

### Planned (Not Yet Implemented)

- `skills/<name>/references/` — Extended reference material for skills that need deeper context.
- `adapters/` — Agent-specific adapters that define how each agent loads and applies skills.
- `scripts/` — Sync and validation utilities.

## How to Add a New Skill

1. Create `skills/<skill-name>/SKILL.md` using the [standard structure](#skillmd-standard-structure).
2. Add an entry to `registry/skills.json` with the correct `id`, `version`, `path`, `description`, and `triggers`.
3. Ensure the `path` in the registry exactly matches the file location.
4. Test the skill locally with at least one agent.
5. Commit and push.

## How to Modify a Skill

1. Edit the `SKILL.md` file.
2. Update the version in the frontmatter **and** in `registry/skills.json` following [versioning rules](#versioning-rules).
3. Test locally.
4. Commit with a clear message describing what changed and why.
5. Push to GitHub.

## SKILL.md Standard Structure

Every skill follows this structure:

```markdown
---
name: <skill-name>
description: <short description>
version: <MAJOR.MINOR.PATCH>
---
# Purpose
# When To Use
# Workflow
# Decision Rules
# Output Format
# Constraints
```

- **description**: One sentence, concise.
- **Workflow**: Must be genuinely executable steps.
- **Decision Rules**: Only skill-specific logic — no generic AI behavior rules.
- **Output Format**: Suggested structure, not a rigid template.
- **Constraints**: Only skill-specific limitations.

## Versioning Rules

Follows [Semantic Versioning](https://semver.org/):

| Change Type | Version Bump | Example |
|---|---|---|
| Core behavior fundamentally changes | MAJOR | 1.0.0 → 2.0.0 |
| New capability added, backward-compatible | MINOR | 1.0.0 → 1.1.0 |
| Small fix or clarification | PATCH | 1.0.0 → 1.0.1 |

## Why GitHub Is Not a Local Runtime Dependency

Local agents read skill files from the local filesystem. The skills in this repository are plain Markdown — they contain no executable code, no API calls, and no external dependencies. An agent that has synced this repository can operate fully offline.

GitHub's role is limited to:

- Version control and history
- Stable release distribution
- Remote access for web-based AI

Treating GitHub as a runtime dependency would:

- Break offline usage
- Introduce latency and availability risks
- Couple skills to a specific hosting platform
- Violate the platform-agnostic principle

## Design Principles

1. **Platform-agnostic**: Skills contain no agent-specific logic, no references to specific tools, APIs, or model capabilities.
2. **Progressive disclosure**: Skills are concise by default. Deeper context is deferred to optional `references/` (future).
3. **Behavior-focused**: Skills define decision rules and workflows, not generic AI behavior guidelines.
4. **No filler**: No "you are a professional assistant" or "be polite" — these are universal and don't belong in individual skills.
5. **Negative outcomes allowed**: Skills must allow for conclusions like "don't buy", "insufficient evidence", etc.
