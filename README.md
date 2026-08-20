# Personal AI Skills

一个小型、平台无关的可复用 AI Skill 仓库。

这个仓库的核心理念很简单：**Skill 的内容应该独立于加载它的 Agent。**

## 当前状态

目前仓库包含一个 Skill：

- `shopping` — 理性购物决策

以后只有在真正需要时才增加新的 Skill。

## 各部分的职责

### 本地仓库

本地 Git 工作副本是本地 Agent 的开发源和运行源。

Claude 和 Hermes 应直接从本地文件系统读取 Skill。修改并保存本地 `SKILL.md` 后，本地 Agent 就可以使用最新版本，不需要在运行时从 GitHub 下载 Skill。

### GitHub

GitHub 保存经过版本控制、已经发布的 Skill。

它用于：

- 保存版本历史
- 本地测试完成后发布版本
- 在条件允许时，为网页 AI 提供远程访问

GitHub **不是本地 Skill 加载的运行时依赖**。

### 网页 AI

ChatGPT、Kimi 等网页 AI 可以被要求查看这个仓库并使用指定的 Skill，例如：

> 前往 `Frank-Y81/personal-ai-skills`，找到 `shopping` Skill，并按照它完成这个任务。

实际能否访问仓库，取决于具体 AI 服务自身的能力。

## 目录结构

```text
personal-ai-skills/
├── shopping/
│   └── SKILL.md
├── registry/
│   └── skills.json
└── README.md
```

每个顶层 Skill 目录都包含自己的 `SKILL.md`：

```text
<skill-name>/
└── SKILL.md
```

如果某个 Skill 以后确实需要较多的辅助资料，可以再增加 `references/`、`scripts/` 等目录。没有实际需求时，不提前创建。

## 添加 Skill

1. 创建 `<skill-name>/SKILL.md`。
2. 在 `registry/skills.json` 中添加对应的索引项。
3. 用将要使用它的 Agent 在本地测试。
4. 确认满意后再提交并推送。

## 修改 Skill

1. 修改本地 `SKILL.md`。
2. 使用 Claude 和/或 Hermes 在本地测试修改。
3. 在需要时更新 Skill 版本号。
4. 由你决定是否提交并推送到 GitHub。

目前没有单独的开发版、预发布版或运行版。对于当前的单用户工作流，本地工作副本同时承担开发和本地运行；GitHub 代表已经发布的版本。

## Registry

`registry/skills.json` 是一个面向外部 AI 或其他读取方的轻量级 Skill 发现索引。它主要回答三个问题：

- 当前有哪些 Skill？
- 每个 Skill 叫什么？
- 它的 `SKILL.md` 在哪里？

Registry 不属于 Claude 或 Hermes 的本地运行链路，也不负责自动 Skill 路由。

## 设计原则

1. **单一本地来源** — 避免维护同一个 Skill 的多份副本。
2. **平台无关的 Skill 内容** — 尽量把 Agent 特有的加载逻辑放在 Skill 之外。
3. **显式调用** — Skill 在用户明确指定后使用，不依赖复杂的自动路由。
4. **本地优先** — 本地 Agent 正常运行时不应从 GitHub 获取 Skill。
5. **不做不必要的工程化** — 在没有真实需求之前，不增加 Adapter、同步系统、多环境、CI 或 API。
6. **按需扩展** — 只有在 Skill 确实需要大量额外内容时，才拆分到其他文件。
