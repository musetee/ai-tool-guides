[English](mattpocock-skills.md) · [中文](mattpocock-skills_cn.md)

[← 全部说明](../README_cn.md)

# Matt Pocock 的 Claude Code 技能

写给在 Claude Code 里装了（或考虑装）`mattpocock-skills` 插件的人：每个技能是干什么的、从哪里开始、要注意什么。

| | |
| :--- | :--- |
| 插件 | `mattpocock-skills@claude-plugins-official`，版本 1.3.1 |
| 来源 | Matt Pocock 的 [mattpocock/skills](https://github.com/mattpocock/skills)，MIT 许可 |
| 安装 | `claude plugin install mattpocock-skills@claude-plugins-official` |
| 本说明 | 根据每个技能的 `SKILL.md` 整理（2026-11-01），还没有逐个实际用过 |

它的主张：给真正做工程的人用的小技能，不是 vibe coding。每个技能小而独立，自己组合、修改；不像 Spec-Kit、BMAD 那样替你接管整个流程。

## 🚀 怎么调用

1. **新开会话。** 技能在会话开始时加载，装插件之前就开着的会话看不到它们。
2. **在要处理的文件夹里启动 Claude**，例如 `cd ~/projects/my-project && claude`。
3. **输入斜杠命令**，后面接你的问题，例如 `/grill-me 我在考虑……`。

注意：

- `ask-matt` 只能你自己输入 `/ask-matt` 调用，agent 不会自动用它。
- 有些技能（例如 `pr`、`codebase-design`）agent 会在合适的时候自己用。

## 🧭 从哪里开始

不知道用哪个就先问 `/ask-matt`：它不回答问题本身，而是告诉你该用哪个技能、按什么顺序用。

它推荐的主线（从想法到交付）：

| 步骤 | 技能 | 做什么 |
| :--- | :--- | :--- |
| 1. 把想法问清楚 | `/grill-with-docs`（在项目文件夹里）或 `/grill-me`（不写文件） | 一个问题接一个问题地追问，直到想法清楚 |
| 2. 需要先试一下才知道 | `/handoff` → `/prototype` → `/handoff` | 交接到新会话做一次性原型，再把结论带回来 |
| 3a. 一次会话做得完 | `/implement` | 直接写代码（内部用 `/tdd`，最后 `/code-review`） |
| 3b. 要跨好几次会话 | `/to-spec` → `/to-tickets` → `/implement` 或 `/implement-spec` | 先写需求规格，拆成任务单，再逐个或一次性实现 |
| 4. 发 PR | `/pr` | 写 PR 说明 |
| 5. 复盘 | `/retro` | 回看这次会话，建议怎么改进环境（检查、规范、提示文件） |

其他入口：

| 情况 | 技能 |
| :--- | :--- |
| 别人提的 bug 和需求堆起来了 | `/triage` |
| 有个难缠的 bug | `/diagnosing-bugs` |
| 一个很大、看不清方向的工作（一次会话装不下） | `/wayfinder` |
| 有空时整理代码库 | `/improve-codebase-architecture` |

## 📋 全部技能（启用的 27 个）

### 入口

| 技能 | 用来做什么 |
| :--- | :--- |
| `ask-matt` | 不知道用哪个？问它，它推荐适合你情况的技能或流程 |
| `setup-matt-pocock-skills` | 第一次用工程类技能前运行一次：给仓库配好 issue 追踪方式、分类标签和领域文档的位置 |

### 计划与需求

| 技能 | 用来做什么 |
| :--- | :--- |
| `grill-me` / `grilling` | 对你的计划、决定或想法不停追问，帮你把想法逼清楚 |
| `grill-with-docs` | 同样追问，同时把结论写成 ADR（架构决策记录）和术语表 |
| `to-spec` | 把当前对话整理成一份需求规格，发到 issue 追踪里（不再提问，只做整理） |
| `to-tickets` | 把计划或规格拆成一组小任务单，写清谁挡着谁 |
| `wayfinder` | 一次会话装不下的大工作：拆成一张"决策任务地图"，一个一个解决 |
| `triage` | 给 issue 和外部 PR 分类、核实，必要时追问，写成 agent 能直接接手的说明 |
| `to-questionnaire` | 一个你自己答不全的决定，做成问卷交给别人填 |

### 写代码

| 技能 | 用来做什么 |
| :--- | :--- |
| `implement` / `implement-spec` | 按规格或任务单写代码 |
| `tdd` | 测试驱动开发：先写失败的测试，再让它通过，再重构 |
| `diagnosing-bugs` | 难缠的 bug 和性能退化的排查流程 |
| `prototype` | 做一个用完就扔的原型，回答一个设计问题（状态逻辑对不对、界面该长什么样） |
| `wizard` | 生成一个交互式 bash 向导，带人一步步做只有人能做的事（配凭据、CI 密钥、点第三方后台） |

### 架构与领域

| 技能 | 用来做什么 |
| :--- | :--- |
| `codebase-design` | 设计"深模块"的共同词汇：接口怎么定、接缝放哪、怎样更好测、让 AI 更好读 |
| `improve-codebase-architecture` | 扫描整个代码库，找能改进的地方，出一份 HTML 报告，再挑一个深入追问 |
| `domain-modeling` | 建立和打磨项目的领域模型：术语表 GLOSSARY.md、ADR |

### 审阅与交付

| 技能 | 用来做什么 |
| :--- | :--- |
| `code-review` | 审阅从某个提交或分支以来的改动，分两方面看：符不符合仓库的编码规范；符不符合原来的需求 |
| `pr` | 写 PR 说明 |
| `retro` | 对一次编码会话做复盘 |

### 学习、写作、交接

| 技能 | 用来做什么 |
| :--- | :--- |
| `research` | 从可信的一手资料调查一个问题，结论写成仓库里的 Markdown 文件 |
| `teach` | 在当前工作区里教你一个新技能或概念 |
| `wait-what` | 上一条回复没看懂时用：让 agent 换个说法重讲 |
| `handoff` | 把当前对话压缩成交接文档，给另一个 agent 接手 |
| `writing-for-agents` | 写给 agent 看的文档：技能、AGENTS.md、CLAUDE.md |

包里另有 11 个技能**没有启用**：`in-progress/` 下的 chief-of-staff、claude-handoff、loop-me、setup-ts-deep-modules、writing-beats、writing-fragments、writing-shape（还在开发中），`misc/` 下的 git-guardrails-claude-code、migrate-to-shoehorn、scaffold-exercises、setup-pre-commit（杂项）。

## ⚠️ 要注意的地方

| 地方 | 可能出的问题 | 怎么办 |
| :--- | :--- | :--- |
| `code-review` | 和 Claude Code 自带的 `/code-review` 同名，输入 `/code-review` 不一定是你想要的那个 | 用之前看一眼调起来的是哪个 |
| `handoff` | 它写一份交接文档，不会把工作交给另一个正在运行的 agent | 换文件夹、换工具或交给同事时用；正在运行的 agent 之间交接，用你自己的方式 |
| `grill-with-docs`、`domain-modeling`、`research` | 会在**当前文件夹**写文件（GLOSSARY.md、ADR、调查结果）。在公开仓库里，一旦提交就公开了 | 公开仓库里用 `/grill-me`（不写文件），或者在一个私人笔记文件夹里开会话 |
| `to-spec`、`to-tickets`、`triage`、`wayfinder` | 依赖 issue 追踪器（GitHub issues，或本地 `.scratch/` 下的文件） | 先运行 `/setup-matt-pocock-skills`；如果你已经把计划放在别处，先想好任务单放哪 |
| `grill-me` / `grilling` | 会连续问很多轮 | 觉得够了就说"可以了，总结一下" |

## 💡 例子：一个项目要不要重构？

1. 在项目文件夹里开一个新终端：`cd ~/projects/my-project && claude`
2. 输入：
   ```
   /grill-me 我在考虑要不要重构这个项目，比如改成各个 AI 工具的原生插件，让人更容易上手。请先看一下仓库再问我。
   ```
3. 想先听它推荐用哪个技能，就输入 `/ask-matt 我想讨论要不要把项目重构成原生插件，应该用哪个技能？`

## 🔧 管理插件

| 想做 | 命令 |
| :--- | :--- |
| 看装了哪些插件 | `claude plugin list` |
| 看它带了什么、占多少上下文 | `claude plugin details mattpocock-skills` |
| 暂时停用 / 重新启用 | `claude plugin disable mattpocock-skills` / `claude plugin enable mattpocock-skills` |
| 更新（默认会自己更新） | `claude plugin update mattpocock-skills` |
| 卸载 | `claude plugin uninstall mattpocock-skills` |

这个插件也有 Codex、GitHub Copilot、Gemini CLI 的版本，见它的 [README](https://github.com/mattpocock/skills#readme)。
