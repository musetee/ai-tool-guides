[English](mattpocock-skills.md) · [中文](mattpocock-skills_cn.md)

[← All guides](../README.md)

# Matt Pocock's skills for Claude Code

For people who installed (or are considering) the `mattpocock-skills` plugin in Claude Code and want to know what each skill does, where to start, and what to watch out for.

| | |
| :--- | :--- |
| Plugin | `mattpocock-skills@claude-plugins-official`, version 1.3.1 |
| Source | [mattpocock/skills](https://github.com/mattpocock/skills) by Matt Pocock, MIT licence |
| Install | `claude plugin install mattpocock-skills@claude-plugins-official` |
| This guide | Summarised from each skill's `SKILL.md` on 2026-11-01; not every skill has been tried in practice yet |

The idea behind it: small, independent skills for real engineering, not vibe coding. You combine and adapt them yourself, instead of handing your whole process to a framework such as Spec-Kit or BMAD.

## 🚀 How to call a skill

1. **Start a new session.** Skills load when a session starts; a session opened before you installed the plugin does not see them.
2. **Start Claude in the folder you want to work on**, for example `cd ~/projects/my-project && claude`.
3. **Type the slash command** followed by your question, for example `/grill-me I'm thinking about …`.

Good to know:

- `ask-matt` runs only when you type `/ask-matt` yourself; the agent never calls it on its own.
- Some skills (for example `pr` and `codebase-design`) are used by the agent by itself when they fit.

## 🧭 Where to start

Not sure which skill fits? Ask `/ask-matt`. It does not answer your question itself; it tells you which skill to use and in what order.

The main path it recommends, from idea to shipped code:

| Step | Skill | What happens |
| :--- | :--- | :--- |
| 1. Get the idea clear | `/grill-with-docs` (in a project folder) or `/grill-me` (writes no files) | It asks you one question after another until the idea is clear |
| 2. You need to try something to know | `/handoff` → `/prototype` → `/handoff` | Hand off to a new session, build a throwaway prototype, bring what you learned back |
| 3a. Fits in one session | `/implement` | Writes the code (driving `/tdd`, finishing with `/code-review`) |
| 3b. Takes several sessions | `/to-spec` → `/to-tickets` → `/implement` or `/implement-spec` | Write a spec, split it into tickets, build them one by one or in one run |
| 4. Open a pull request | `/pr` | Writes the PR description |
| 5. Look back | `/retro` | Reviews the session and suggests changes to the environment (checks, standards, steering files) |

Other starting points:

| Situation | Skill |
| :--- | :--- |
| Bug reports and requests from others piling up | `/triage` |
| A hard bug | `/diagnosing-bugs` |
| A huge, unclear piece of work (more than one session) | `/wayfinder` |
| A spare moment to tidy the codebase | `/improve-codebase-architecture` |

## 📋 All skills (the 27 the plugin enables)

### Entry points

| Skill | What it is for |
| :--- | :--- |
| `ask-matt` | Not sure which skill to use? It recommends the skill or path that fits your situation |
| `setup-matt-pocock-skills` | Run once before the engineering skills: sets up the repository's issue tracker, triage labels and where domain docs live |

### Planning and requirements

| Skill | What it is for |
| :--- | :--- |
| `grill-me` / `grilling` | Questions your plan, decision or idea relentlessly until it is sharp |
| `grill-with-docs` | The same interview, and it writes the conclusions down as ADRs (architecture decision records) and a glossary |
| `to-spec` | Turns the current conversation into a spec and publishes it to the issue tracker (no more questions, only synthesis) |
| `to-tickets` | Splits a plan or spec into small tickets, each stating what blocks it |
| `wayfinder` | For work too big for one session: a map of decision tickets, resolved one at a time |
| `triage` | Sorts and checks incoming issues and external PRs, asks follow-up questions if needed, and writes briefs an agent can pick up |
| `to-questionnaire` | Turns a decision you cannot fully answer into a questionnaire for someone else |

### Writing code

| Skill | What it is for |
| :--- | :--- |
| `implement` / `implement-spec` | Builds code from a spec or tickets |
| `tdd` | Test-driven development: a failing test first, then make it pass, then refactor |
| `diagnosing-bugs` | A diagnosis loop for hard bugs and performance regressions |
| `prototype` | A throwaway prototype to answer a design question (does the state logic hold, what should the UI look like) |
| `wizard` | Generates an interactive bash wizard that walks a person through steps only they can do (credentials, CI secrets, third-party dashboards) |

### Architecture and domain

| Skill | What it is for |
| :--- | :--- |
| `codebase-design` | A shared vocabulary for designing deep modules: interfaces, seams, testability, code that is easy for AI to navigate |
| `improve-codebase-architecture` | Scans the codebase for improvements, shows them in an HTML report, then questions you on the one you pick |
| `domain-modeling` | Builds and sharpens the project's domain model: GLOSSARY.md and ADRs |

### Review and delivery

| Skill | What it is for |
| :--- | :--- |
| `code-review` | Reviews the changes since a commit or branch on two axes: does it follow the repository's coding standards, and does it match the original spec |
| `pr` | Writes a pull request description |
| `retro` | A retrospective on a coding session |

### Learning, writing, handing over

| Skill | What it is for |
| :--- | :--- |
| `research` | Investigates a question in trustworthy primary sources and writes the findings to a Markdown file in the repository |
| `teach` | Teaches you a new skill or concept, in your workspace |
| `wait-what` | The last reply did not land: the agent explains it again differently |
| `handoff` | Compresses the conversation into a handoff document for another agent |
| `writing-for-agents` | Writing documents for agents: skills, AGENTS.md, CLAUDE.md |

The package holds 11 more skills that the plugin does **not** enable: in `in-progress/` chief-of-staff, claude-handoff, loop-me, setup-ts-deep-modules, writing-beats, writing-fragments, writing-shape (still being developed); in `misc/` git-guardrails-claude-code, migrate-to-shoehorn, scaffold-exercises, setup-pre-commit.

## ⚠️ Things to watch

| Where | What can go wrong | What to do |
| :--- | :--- | :--- |
| `code-review` | Same name as Claude Code's built-in `/code-review`; typing `/code-review` may not give you the one you expect | Check which one started |
| `handoff` | Writes a handoff document; it does not pass work to another agent that is already running | Use it for a new folder, a new tool or a colleague; use your own setup for live handoffs between running agents |
| `grill-with-docs`, `domain-modeling`, `research` | They write files into the **current folder** (GLOSSARY.md, ADRs, findings). In a public repository those notes would end up published once committed | In a public repository use `/grill-me` (writes nothing), or start the session in a private notes folder |
| `to-spec`, `to-tickets`, `triage`, `wayfinder` | They need an issue tracker (GitHub issues, or local files under `.scratch/`) | Run `/setup-matt-pocock-skills` first; decide where tickets should live if you already keep plans elsewhere |
| `grill-me` / `grilling` | They ask many rounds of questions | Say "that's enough, summarise" when you are done |

## 💡 Example: should a project be restructured?

1. Open a new terminal in the project: `cd ~/projects/my-project && claude`
2. Type:
   ```
   /grill-me I'm considering restructuring this project, for example shipping it as a native plugin for each AI tool so it is easier to start with. Look at the repository first, then ask me.
   ```
3. To hear which skill it recommends first, type `/ask-matt I want to discuss whether to restructure my project into native plugins. Which skill should I use?`

## 🔧 Managing the plugin

| To | Command |
| :--- | :--- |
| See installed plugins | `claude plugin list` |
| See what it brings and its context cost | `claude plugin details mattpocock-skills` |
| Disable / enable it | `claude plugin disable mattpocock-skills` / `claude plugin enable mattpocock-skills` |
| Update it (it also updates itself) | `claude plugin update mattpocock-skills` |
| Remove it | `claude plugin uninstall mattpocock-skills` |

The plugin also exists for Codex, GitHub Copilot and Gemini CLI; see its [README](https://github.com/mattpocock/skills#readme).
