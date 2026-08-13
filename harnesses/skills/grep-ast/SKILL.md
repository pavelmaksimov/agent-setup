---
name: grep-ast
description: Performs AST-aware code search with `uvx grep-ast` to find definitions, callers, and structure without brittle line-based grep. Use before refactoring large areas, when mapping impact of a symbol, replacing plain grep for Python/JS, or when the user mentions grep-ast, structural search, or AST navigation.
---

# grep-ast (AST search)

Tool: [Aider-AI/grep-ast](https://github.com/Aider-AI/grep-ast) — install / run via `uvx` or pip.
Skill: take from this catalog (`harnesses/skills/grep-ast/`), not from upstream.

`uvx grep-ast` works in AST terms: a method is shown within its class bounds, without hand-picking line ranges and without risking a broken structure.

## Install the tool

```bash
uvx grep-ast --help
# or: pip install grep-ast / uv tool install grep-ast
```

Repo: https://github.com/Aider-AI/grep-ast

## When to use

**Problem:** before refactoring a function/method/class it is hard to estimate the full change surface. Plain grep returns dozens of line matches but no structural context (class, module, interface).

**Approach:** use `uvx grep-ast` for surgical reconnaissance before edits — get an AST map of dependencies:

- **Where** — where the target is defined (with full body)
- **Who calls** — who calls it (with caller context)
- **Inheritance chain** — overrides / inheritance
- **Test coverage** — which tests are involved (search by name under test directories)

## CLI reference

```bash
uvx grep-ast --help
usage: uvx grep-ast [-h] [--encoding ENCODING] [--languages] [-i] [--color] [--no-color] [--no-gitignore] [--verbose] [-n] [pattern] [filenames ...]

positional arguments:
  pattern              the pattern to search for
  filenames            the files to display

options:
  -h, --help           show this help message and exit
  --encoding ENCODING  file encoding
  --languages          show supported languages
  -i, --ignore-case    ignore case distinctions
  --color              force color printing
  --no-color           disable color printing
  --no-gitignore       ignore .gitignore file
  --verbose            enable verbose output
  -n, --line-number    display line numbers
```

## OR condition: `|` without escaping

Wrong:

```bash
uvx grep-ast "(get\|post\|put\|delete)"
```

Correct:

```bash
uvx grep-ast "(get|post|put|delete)"
```

## Examples

Search the project (auto language detection):

```bash
uvx grep-ast "class.*Agent|def.*review|def.*prompt|user_prompt|system_prompt" project
```

File or directory, case-insensitive:

```bash
uvx grep-ast -i "validate_email" project/models/
```

Class definitions only (Python):

```bash
uvx grep-ast "class.*Service|class.*Schema"
```

Method with calling-function context:

```bash
uvx grep-ast "send_notification\(|call_endpoint"
```

FastAPI endpoints:

```bash
uvx grep-ast "@.*\.(get|post|put|delete)"
```

Imports of a legacy module:

```bash
uvx grep-ast "from.*components" | grep "import\|from"
```

## Do not search overly generic words

Bad:

```bash
uvx grep-ast 'get' .
uvx grep-ast 'data' .
uvx grep-ast 'id' .
```

Understand the code first, then confirm with tests. For long e2e tests, ask the user for permission.
