# Agent setup catalog

This repository publishes reusable agent harnesses and the skill that installs
them into other repositories.

- `catalog.yaml` is the source of truth for discovery and installation.
- Keep each harness self-contained under `harnesses/<id>/`.
- Add only files that are safe to publish and reuse.
- Every catalog file mapping must resolve inside this repository.
- Prefer concise instructions and native agent features over installer code.
