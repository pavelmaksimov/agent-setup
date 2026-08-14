---
name: setup-agent-harnesses
description: Recommends and installs compatible agent harnesses from pavelmaksimov/agent-setup. Use when bootstrapping agent rules, skills, hooks, or workflows in a new repository.
---

# Set up agent harnesses

Use `https://github.com/pavelmaksimov/agent-setup` as the catalog and source.

## Workflow

1. Inspect the target repository's languages, tools, existing agent files, and
   development workflow.
2. Clone the source repository into a temporary directory and read `README.md`
   (the **Catalog** section is the source of truth).
3. Present harnesses **grouped by category**. For each category, list
   installable and reference entries separately. For **Python stack**, present
   the three bands (core, adapters, enforcement). Recommend core for any Python
   repo, adapters that match the codebase (FastAPI, SQLAlchemy), and the three
   linter skills with the stack. Do not offer the stack as one catch-all ID.
4. Filter out entries that clearly do not fit the repo.
5. Ask the user only about choices that cannot be inferred:
   - which categories matter for this repo;
   - desired agent clients;
   - workflow goals;
   - project-only or personal installation;
   - for `keep-a-changelog`, which language to use for CHANGELOG entries.
6. Recommend the smallest compatible set. For each item, state the benefit,
   install path or upstream link, and conflicts with already-present skills.
7. Get explicit approval for the final set.
8. For **installable** rows, copy `Install from` source → target (see below).
   Kind means this repo is the artifact source of truth.
9. For **reference** rows, print the upstream URL and notes; install from
   upstream. Do not treat a missing local mirror as something to recreate here
   (e.g. `agent-browser` needs the upstream CLI).
10. Preserve existing files. If a target exists, show the conflict and ask
    whether to merge, replace, or skip it.
11. Report installed, referenced (manual), skipped, and unresolved items.

The setup is complete when every approved installable file is installed or
explicitly skipped and every approved reference entry has install notes shown.

## How to read the README catalog

Each category section has a table with:

| Column | Meaning |
|---|---|
| ID | Stable id used in recommendations |
| Kind | `installable` or `reference` |
| Upstream | Canonical project / spec URL |
| Install from / Notes | Copy mapping `source → target`, or manual install notes |

Installable artifacts are grouped by type under `harnesses/`:

```text
harnesses/skills/<id>/   → .cursor/skills/<id>/
harnesses/rules/<id>/    → .cursor/rules/<id>/
harnesses/hooks/<id>/    → .cursor/hooks/<id>/   # or project hooks layout
harnesses/agents/<id>/   → .cursor/agents/<id>/  # sub-agents
```

Default for an installable **skill** with id `<id>`:

```text
harnesses/skills/<id>/SKILL.md → .cursor/skills/<id>/SKILL.md
```

If the table shows an explicit `source → target`, use that. For personal
install, replace `.cursor/` with `~/.cursor/` (or the Claude / Codex
equivalent).

Resolve relative source paths from the cloned catalog root and targets from
the target repository root (or home for personal installs).

## Safety

- Keep the target repository's conventions authoritative.
- Install only files under `harnesses/{skills,rules,hooks,agents}/` for
  selected installable entries.
- Never copy or recreate upstream/reference packs into the catalog repo.
- Require approval before overwriting, deleting, or changing existing content.
- Do not copy credentials, local absolute paths, generated output, or source
  repository Git metadata.
- Remove the temporary clone after the result is reported.
