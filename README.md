# agent-setup

A public catalog of the agent harnesses and skills I use to build software.

It is both:

- a showcase of practical agentic workflows;
- a bootstrap source for new repositories.

## Bootstrap a new repository

Open a clean repository in your coding agent and send:

```text
Read and follow:
https://raw.githubusercontent.com/pavelmaksimov/agent-setup/main/skills/setup-agent-harnesses/SKILL.md

Inspect this repository, ask which harnesses I want (grouped by category),
recommend a compatible set, and install only the set I approve.
```

The setup skill reads this README catalog, groups options by category, asks only
what it cannot infer, and installs **installable** entries after approval.
**Reference** entries get upstream links and install notes.

## What Kind means

Kind answers: **where is the real product installed from?**

| Kind | Meaning |
|---|---|
| **installable** | This repo is the source of truth for the artifact. Copy from `harnesses/<type>/<id>/`. The underlying CLI/package may still need a separate upstream install (see Notes). |
| **reference** | Upstream is the source of truth for the whole product (CLI, plugin, framework, or skill pack). Do not treat a local mirror as the product. |

Installable artifacts live only under typed dirs in `harnesses/` (`skills/`,
`rules/`, `hooks/`, `agents/`). Never vendor upstream/reference packs here.

## Catalog

### Agent runtimes / harnesses

Full coding-agent harnesses and opinionated workflow layers.

| ID | Name | Kind | Summary | Upstream | Notes |
|---|---|---|---|---|---|
| `oh-my-openagent` | oh-my-openagent | reference | Multi-harness coding agent layer (omo/lazycodex) for complex codebases on Codex/OpenCode | https://github.com/code-yeongyu/oh-my-openagent | Follow upstream install for your coding agent |
| `oh-my-pi` | oh-my-pi | reference | Terminal AI coding agent with hash-anchored edits, LSP, browser, and subagents | https://github.com/can1357/oh-my-pi | Install the oh-my-pi / omp CLI from upstream releases |
| `oh-my-hermes` | oh-my-hermes | reference | Opinionated workflow layer for building and shipping with Hermes Agent | https://github.com/Salomondiei08/oh-my-hermes | Install as a Hermes workflow layer from upstream |
| `superpowers` | Superpowers | reference | Agentic skills framework and software development methodology | https://github.com/obra/superpowers | Use upstream installer / skill pack instructions |

### Engineering skills

Skills that change how the agent designs, implements, and reviews code.

| ID | Name | Kind | Summary | Upstream | Notes |
|---|---|---|---|---|---|
| `ponytail` | Ponytail | reference | Forces the laziest solution that works — YAGNI, stdlib first, shortest diff | https://github.com/DietrichGebert/ponytail | Install skill pack from upstream |
| `mattpocock-skills` | Matt Pocock skills | reference | Engineering skills pack (triage, planning, implementation) | https://github.com/mattpocock/skills | Clone/copy skills from upstream |
| `deslop` | deslop | reference | Remove AI-generated code slop against the main-branch diff | https://github.com/cursor/plugins/blob/main/cursor-team-kit/skills/deslop/SKILL.md | From Cursor Team Kit / plugins |
| `thermo-nuclear-code-quality-review` | Thermo-nuclear code quality review | reference | Extremely strict maintainability review — ambitious restructuring | https://github.com/cursor/plugins/blob/main/cursor-team-kit/skills/thermo-nuclear-code-quality-review/SKILL.md | From Cursor Team Kit / plugins |
| `weekly-review` | Weekly review | reference | Weekly synthesis of authored commits by bugfix, tech debt, net-new | https://github.com/cursor/plugins/tree/main/cursor-team-kit/skills | From Cursor Team Kit / plugins |
| `logika` | Logika | reference | Classical formal logic review and rewrite of arguments | https://github.com/EvilFreelancer/logika | Install from upstream |
| `grep-ast` | grep-ast | installable | AST-aware code search via `uvx grep-ast` | https://github.com/Aider-AI/grep-ast | Install the tool from upstream (`uvx grep-ast` / pip). Take the skill from this repo: `harnesses/skills/grep-ast/SKILL.md` → `.cursor/skills/grep-ast/SKILL.md` |
| `layers-linter` | layers-linter | installable | Enforce Python layer and library import boundaries via `uvx layers-linter` | https://github.com/pavelmaksimov/layers-linter | Install the tool from upstream (`uvx layers-linter` / pip). Take the skill from this repo: `harnesses/skills/layers-linter/SKILL.md` → `.cursor/skills/layers-linter/SKILL.md` |

### Memory and knowledge

Persistent memory, knowledge graphs, and wiki scaffolds.

| ID | Name | Kind | Summary | Upstream | Notes |
|---|---|---|---|---|---|
| `continual-learning` | Continual Learning | reference | Cursor plugin that mines transcripts and updates `AGENTS.md` | https://github.com/cursor/plugins/tree/main/continual-learning | Install from Cursor marketplace or cursor/plugins |
| `haft` | haft | reference | Decision memory with evidence decay and parity checks — knows when decisions are stale | https://github.com/m0n0x41d/haft | Install from upstream for your coding agent |
| `graphify` | Graphify | reference | Turn a codebase/corpus into a knowledge graph with query/path/explain | https://github.com/Graphify-Labs/graphify | Install `graphifyy` (PyPI) + upstream skill |
| `supermemory` | Supermemory | reference | Fast memory/context engine and API for durable agent memory | https://github.com/supermemoryai/supermemory | Connect MCP/API; do not commit API keys |
| `llm-wiki-template` | LLM Wiki template | reference | Karpathy-style markdown wiki — agent maintains `wiki/`, you curate `raw/` | https://github.com/pavelmaksimov/llm-wiki-template | Clone as a separate wiki repo; not an app dependency |

[`llm-wiki-template`](https://github.com/pavelmaksimov/llm-wiki-template) is a
ready scaffold for a project or domain knowledge base.

### Agent tooling

CLI and browser/search tools that agents call while working.

| ID | Name | Kind | Summary | Upstream | Notes |
|---|---|---|---|---|---|
| `keenable-cli` | Keenable CLI | reference | Fast web search and page fetch with agent-friendly YAML output | https://github.com/keenableai/keenable-cli | Install the `keenable` binary from upstream |
| `agent-browser` | agent-browser | reference | Browser automation CLI — snapshot refs, fill forms, screenshots | https://github.com/vercel-labs/agent-browser | Install the `agent-browser` binary from upstream |

### Standards

Commit and changelog conventions for human-readable history.
These skills and rules were authored here from the official specs (not third-party skill packs).

| ID | Name | Kind | Summary | Upstream | Install from |
|---|---|---|---|---|---|
| `conventional-commits` | Conventional Commits | installable | Draft/validate commit messages per Conventional Commits 1.0.0 | https://www.conventionalcommits.org/en/v1.0.0/ | `harnesses/skills/conventional-commits/SKILL.md` → `.cursor/skills/conventional-commits/SKILL.md` |
| `keep-a-changelog` | Keep a Changelog | installable | Maintain `CHANGELOG.md` per Keep a Changelog 1.1.0; ask language first | https://keepachangelog.com/en/1.1.0/ | `harnesses/skills/keep-a-changelog/SKILL.md` → `.cursor/skills/keep-a-changelog/SKILL.md` |

### Project rules

Cursor `.mdc` rules that shape agent behaviour in a repository.

| ID | Name | Kind | Summary | Upstream | Install from |
|---|---|---|---|---|---|
| `agent-behavior` | Agent behavior | installable | Think before coding, simplicity first, surgical diffs, verifiable goals | https://github.com/pavelmaksimov/agent-setup | `harnesses/rules/agent-behavior/` → `.cursor/rules/agent-behavior/` |
| `python-fastapi` | Python FastAPI service | installable | Component layout, LazyInit/Container/Settings, pytest factories, FastAPI/SSE, SQLAlchemy async, uv/ruff/black | https://github.com/pavelmaksimov/agent-setup | `harnesses/rules/python-fastapi/` → `.cursor/rules/python-fastapi/` |

`python-fastapi` assumes package root `project/` (substitute globs if the repo differs). Pair with
`layers-linter`. Stack: uv, FastAPI, httpx, SQLAlchemy async, orjson, sse-starlette, pytest-asyncio,
testcontainers, respx, aioresponses, requests-mock, pre-commit, Black, isort, Ruff.
If `LazyInit` is missing, copy `STRUCTURES.md` from that rule dir into `project/libs/structures.py`.
If the DB adapter is missing, copy `DATABASE.md` into `project/infrastructure/adapters/database.py`.
Copy `CONFTEST.md` into `tests/conftest.py` for HTTP mocks, `TestClient`, Testcontainers, and
`Container.reset()`.

### Agent frameworks (stack)

Libraries and optimizers for building agent products in code.

| ID | Name | Kind | Summary | Upstream | Notes |
|---|---|---|---|---|---|
| `ag2` | AG2 | reference | Open-source AgentOS (formerly AutoGen) for multi-agent apps | https://github.com/ag2ai/ag2 | Project dependency |
| `pydantic-ai` | Pydantic AI | reference | Typed AI agent framework built around Pydantic | https://github.com/pydantic/pydantic-ai | Prefer for structured outputs |
| `dspy` | DSPy | reference | Program LM pipelines and optimize them systematically | https://github.com/stanfordnlp/dspy | When prompts should be compiled/optimized |
| `skillopt` | SkillOpt | reference | Text-space optimizer for reusable natural-language skills | https://github.com/microsoft/SkillOpt | Evaluate before production |
| `gepa` | GEPA | reference | Reflective optimizer for prompts, code, and related text | https://github.com/gepa-ai/gepa | Pair with DSPy or custom loops |

## Install the setup skill globally

Then ask the agent to run `setup-agent-harnesses` in any repository.

## License

[MIT](LICENSE)

Third-party skills keep their upstream licenses and attributions where applicable.
