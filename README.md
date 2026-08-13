# agent-setup

A public catalog of the agent harnesses I use to build software.

It is both:

- a showcase of practical agentic workflows;
- a bootstrap source for new repositories.

## Bootstrap a new repository

Open a clean repository in your coding agent and send:

```text
Read and follow:
https://raw.githubusercontent.com/pavelmaksimov/agent-setup/main/skills/setup-agent-harnesses/SKILL.md

Inspect this repository, ask which harnesses I want, recommend a compatible set,
and install only the set I approve.
```

The setup skill inspects the project, reads [`catalog.yaml`](catalog.yaml), asks
only questions it cannot answer from the repository, and proposes a minimal
compatible selection before changing files.

## Install the setup skill globally

If your agent supports personal skills, copy
[`skills/setup-agent-harnesses`](skills/setup-agent-harnesses) into its personal
skills directory. For Cursor:

```bash
mkdir -p ~/.cursor/skills
git clone https://github.com/pavelmaksimov/agent-setup.git /tmp/agent-setup
cp -R /tmp/agent-setup/skills/setup-agent-harnesses ~/.cursor/skills/
rm -rf /tmp/agent-setup
```

Then ask the agent to run `setup-agent-harnesses` in any repository.

## Repository layout

```text
catalog.yaml                         machine-readable harness catalog
harnesses/<id>/                     files installed by a catalog entry
skills/setup-agent-harnesses/       bootstrap and recommendation skill
```

Harnesses will be added incrementally. Each catalog entry states what it does,
where its files are installed, and which other harnesses it conflicts with.

## License

[MIT](LICENSE)
