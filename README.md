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

## 目录结构（例子）

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

---

# AI 新手教程：如何使用这个 Skill 库

本章节面向第一次访问本仓库的网页 AI 或其他远程 Agent。

如果用户告诉你这个 GitHub 仓库是其 Skill 库，并要求你根据 `/skill-name` 调用 Skill，请按照以下规则执行。

## 1. 识别 Skill 调用

当用户输入一个你当前不认识的 `/skill-name` 时，将 `/` 后、第一个空格前的内容视为 Skill 名称，其余内容视为该 Skill 的输入。

例如：

```text
/tech VPS
```

解析为：

```text
Skill 名称：tech
Skill 输入：VPS
```

不要因为自己不认识该命令，就直接把它当作普通问题处理。

## 2. 查找 Skill

按以下顺序查找：

1. **先精确匹配**对应的 Skill。
2. 如果精确匹配失败，再进行**模糊匹配**。
3. 如果模糊匹配得到唯一且明显对应的 Skill，则使用该 Skill。
4. 如果仍然找不到，或存在多个候选且无法确定，则询问用户。

不得因为一次关键词搜索无结果，就直接判断 Skill 不存在。

推荐的精确匹配形式为：

```text
<skill-name>/SKILL.md
```

例如：

```text
/tech
→ tech/SKILL.md

/shopping
→ shopping/SKILL.md
```

`registry/skills.json` 可以作为 Skill 发现和路径确认的辅助索引。

## 3. 加载并执行 Skill

找到对应 Skill 后：

1. 读取完整的 `SKILL.md`。
2. 将 `/skill-name` 后面的内容作为该 Skill 的输入。
3. 严格按照 `SKILL.md` 中的规则执行。

Skill 文件中的具体规则优先于本 README 中的通用说明。

## 4. 无法确定时

只有在完成精确匹配和模糊匹配后仍无法确定对应 Skill 时，才询问用户。

在此之前：

- 不要因为一次搜索失败就判定 Skill 不存在；
- 不要随意选择多个候选中的一个；
- 不要把未知的 `/skill-name` 直接当作普通问题回答。

## 快速规则

> **当用户输入未知的 `/skill-name` 时，先精确查找对应 Skill；若找不到，再进行模糊匹配；找到后读取并严格按照其 `SKILL.md` 执行，仍无法确定时再询问用户，不得直接当作普通问题处理。**
