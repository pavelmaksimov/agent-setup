---
name: setup-agent-harnesses
description: Recommends and installs compatible agent harnesses from pavelmaksimov/agent-setup. Use when bootstrapping agent rules, skills, hooks, or workflows in a new repository.
---

# Set up agent harnesses

Use `https://github.com/pavelmaksimov/agent-setup` as the catalog and source.

## Workflow

1. Inspect the target repository's languages, tools, existing agent files, and
   development workflow.
2. Clone the source repository into a temporary directory and read
   `catalog.yaml`.
3. Filter out entries whose compatibility requirements are not met.
4. Ask the user only about choices that cannot be inferred:
   - desired agent clients;
   - workflow goals;
   - project-only or personal installation;
   - optional strictness or automation levels exposed by matching entries.
5. Recommend the smallest compatible set. For each item, state the benefit,
   installation targets, and any conflicts.
6. Get explicit approval for the final set.
7. Copy the approved entry files according to their `files` mappings.
8. Preserve existing files. If a target exists, show the conflict and ask
   whether to merge, replace, or skip it.
9. Run every validation command declared by the installed entries.
10. Report installed, skipped, and unresolved items.

The setup is complete when every approved file is installed or explicitly
skipped and every declared validation passes.

## Catalog contract

Each `catalog.yaml` entry has:

```yaml
- id: example
  name: Example harness
  summary: What changes in agent behavior
  clients: [cursor]
  goals: [implementation]
  compatibility:
    files_any: [pyproject.toml]
  conflicts: []
  files:
    - source: harnesses/example/AGENTS.md
      target: AGENTS.md
  validate: []
```

Treat missing optional fields as empty lists. Resolve relative source paths
from the cloned catalog root and target paths from the target repository root.

## Safety

- Keep the target repository's conventions authoritative.
- Install only cataloged files from the selected entries.
- Require approval before overwriting, deleting, or changing existing content.
- Do not copy credentials, local paths, generated output, or source repository
  Git metadata.
- Remove the temporary clone after the result is reported.
