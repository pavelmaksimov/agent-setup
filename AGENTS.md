# AGENTS.md — agent-setup

Public catalog of agent harnesses used as a showcase and as a bootstrap source
for new repositories. English for repo docs and skills unless the user asks
otherwise.

## Sources of truth

- **Catalog:** `README.md` → section **Catalog**. Do not recreate `catalog.yaml`.
- **Bootstrap skill:** `skills/setup-agent-harnesses/SKILL.md`.
- **Installable artifacts:** only under typed dirs in `harnesses/`.

When the catalog and a local copy disagree, fix the README and remove the stale
copy. Do not invent a second catalog format.

## Layout

```text
README.md                         human + agent catalog
AGENTS.md                         rules for working in this repo
skills/setup-agent-harnesses/     bootstrap / recommend / install skill
harnesses/
  skills/<id>/SKILL.md            installable skills
  rules/<id>/                     installable rules
  hooks/<id>/                     installable hooks
  agents/<id>/                    installable sub-agents
```

Empty typed dirs may keep a `.gitkeep`. Do not put installable content at
`harnesses/<id>/` without a type folder.

## Kind

| Kind | Meaning |
|---|---|
| **installable** | This repo owns the artifact. Copy from `harnesses/<type>/<id>/`. |
| **reference** | Upstream owns the product. Link + notes only. |

Rules:

- Kind answers where the **product** is installed from, not whether a helper
  file happens to exist here.
- Never vendor upstream/reference skills, rules, hooks, or agents into
  `harnesses/`.
- Hybrid case (e.g. `grep-ast`, `layers-linter`, `domain-types-linter`,
  `di-linter`, `python-monitoring`): tool from upstream; skill or rule from this
  repo under the matching typed dir. State both in the README Notes column.
- CLIs/plugins/frameworks (`agent-browser`, `keenable-cli`, Cursor plugins,
  oh-my-*, Superpowers, AG2, …) are **reference** even if a usage skill could
  be written here.

## Language stacks

A language stack is its own catalog category, split into layered IDs:

- **core** — tooling, structure, exceptions, settings, logging, DI, tests (language-wide)
- **adapters** — HTTP, persistence, cache, monitoring (only if the repo uses them)
- **enforcement** — matching linter skills in the same section; not every ID is
  required with the stack (`di-linter` is optional)

Do not collapse a stack into one catch-all rule ID or a comma-separated library
list after the table. Templates (`SETTINGS.md`, `LOGGER.md`, `STRUCTURES.md`, `BASE_MODELS.md`, `BASE_SCHEMAS.md`, `FSM.md`, `RETRY.md`, `DATABASE.md`, `ENV.md`, `CACHE.md`, `CONFTEST.md`, `BOT.md`, `TELEGRAM.md`, `CLIENT.md`)
live in the rule dir they belong to; mention the copy path on that band.
Linter configs (`layers.toml`, `di.toml`) live next to their skills and copy to
the target repo root.

## Adding or changing catalog entries

1. Edit the matching category table in `README.md`. Language-stack pieces go in
   the stack section (core / adapters / enforcement), not a catch-all row.
2. If Kind is **installable**, add files under the correct typed dir and set
   `Install from` as `source → target`.
3. If Kind is **reference**, add Upstream + Notes only — no `harnesses/` copy.
4. Keep IDs stable (`kebab-case`), summaries short, no secrets.
5. Update `skills/setup-agent-harnesses/SKILL.md` only when install layout or
   Kind semantics change.

Default Cursor install targets:

```text
harnesses/skills/<id>/  → .cursor/skills/<id>/
harnesses/rules/<id>/   → .cursor/rules/<id>/
harnesses/hooks/<id>/   → .cursor/hooks/<id>/
harnesses/agents/<id>/  → .cursor/agents/<id>/
```

## Authoring installable rules

- One catalog ID per directory: `harnesses/rules/<id>/` with one or more `.mdc` files.
  For a language stack, that ID is one layer, not the whole stack.
- Frontmatter: `description`, and either `alwaysApply: true` or `globs`.
- English bodies. Default package root is `project/`; note in the README if the installer should substitute.
- One concern per `.mdc`. Name the layer (tooling, HTTP, persistence); leave version pins and Ruff selects to the target `pyproject.toml`.
- Env config (`pydantic-settings`, `Settings().PARAM`) is its own core ID (`python-settings`).
  `python-di` owns Container and LazyService. Do not fold Settings into DI.
- Optional enforcement (`di-linter`) stays out of default pairing lines in
  installable rule bodies. When that ID is added to a target repo, patch those
  companion rules so they mention it.
- No machine-local absolute paths, source-project product names, or secrets.
- When enriching an installable rule from a source template, map each spec into the matching
  catalog ID. Product metric prefixes belong in `python-monitoring`. Leave unmatched concerns
  (named third-party SaaS auth adapters) out until they have their own ID.

## Authoring installable skills

- One directory per skill: `harnesses/skills/<id>/SKILL.md`.
- Frontmatter: `name`, `description` (third person, what + when).
- Keep `SKILL.md` concise; put long reference in sibling files if needed.
- For standards skills authored here (Conventional Commits, Keep a Changelog),
  cite the official spec URL and follow it.
- `keep-a-changelog` must ask changelog language before writing entries.
- Prefer English skill bodies in this public repo.
- Linter config templates (`layers.toml`, `di.toml`) and skill examples use
  package root `project/` and `components/`, matching `python-structure`. Do not
  keep a parallel `domains/` layout.

## Bootstrap behaviour

When running or editing the setup skill:

1. Read the README catalog; present options **by category**.
2. Ask only what cannot be inferred; get approval before copying files.
3. Install only approved **installable** paths; for **reference**, print
   upstream install notes. Recommend `di-linter` separately from
   `layers-linter` and `domain-types-linter`; if approved, patch companion
   rules in the target so they name it next to the other linters.
4. Never overwrite existing target files without asking.
5. Do not commit API keys, tokens, or machine-local absolute paths.

## Learn from mismatches

If the result is clearly not what the user needed (wrong Kind, wrong layout,
vendored upstream packs, catalog in the wrong file, etc.):

1. Fix the immediate mistake in the repo.
2. Update **this** `AGENTS.md` with a durable rule that would have prevented it.
3. Keep the new rule short, positive, and checkable — one instruction, not a
   post-mortem essay.
4. Prefer editing an existing section over adding a duplicate.
5. Do this in the same turn when the mismatch is acknowledged; do not wait to
   be asked to “remember” it unless the user declines.

Goal: the next agent session should not repeat the same disagreement.

## Safety and hygiene

- No credentials, tokens, or private URLs in the catalog or harnesses.
- No absolute `/home/...` paths in published files.
- Ignore IDE junk (`.idea/`); keep `.gitignore` current.
- Prefer the smallest change that keeps README, layout, and setup skill aligned.
- Do not turn this repo into an app, CLI installer binary, or package registry
  unless the user explicitly asks.
