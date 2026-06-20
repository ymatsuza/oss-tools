# oss-tools

A collection of small, focused CLI tools for everyday developer workflows.
Each tool lives in its own repository — install only what you need.

## Tools

| Tool | Description | Install |
|------|-------------|---------|
| [rcmd](https://github.com/ymatsuza/rcmd) | Personal command knowledge base: import shell history, annotate/tag, search, and recall (print or run) with `{{placeholder}}` substitution. Local-only single TOML, cross-platform. | `uv tool install "git+https://github.com/ymatsuza/rcmd.git"` |

## Installation

Each tool is published to PyPI and can be installed with [uv](https://docs.astral.sh/uv/) or [pipx](https://pipx.pypa.io/):

```bash
uvx <name>                  # run without installing
uv tool install <name>      # install as a persistent tool
pipx install <name>         # alternative
```

Or install directly from GitHub:

```bash
uv tool install "git+https://github.com/ymatsuza1128/<name>.git"
```

## Tool conventions

Each tool in this collection follows the same structure:

- **Language:** Python 3.11
- **Package manager:** [uv](https://docs.astral.sh/uv/)
- **CLI framework:** [Typer](https://typer.tiangolo.com/)
- **Testing:** pytest
- **Architecture:** pure-core logic + thin CLI layer
- **License:** MIT

## License

MIT — see [LICENSE](LICENSE).
