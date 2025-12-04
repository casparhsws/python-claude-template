
## Tech Stack

- **Python**: 3.12+
- **Package Manager**: [uv](https://github.com/astral-sh/uv)
- **Type Checking**: mypy (strict mode)
- **Linting/Formatting**: ruff
- **Testing**: pytest with pytest-asyncio
- **Task Runner**: poethepoet (poe)

## Project Structure

This is a uv workspace monorepo with two main directories:
- `libs/` - Reusable library packages
- `apps/` - Deployable applications (e.g., FastAPI services)

Each package has its own `pyproject.toml`, `src/`, and `tests/` directories.

```
python-claude-template/
├── libs/                        # Reusable libraries
│   └── package-example/         # Example package
│       ├── src/
│       ├── tests/
│       └── pyproject.toml
├── apps/                        # Deployable applications
│   └── api-example/             # Example FastAPI app
│       ├── src/
│       ├── tests/
│       └── pyproject.toml
└── pyproject.toml               # Root workspace configuration
```

## Development Commands

```bash
uv run poe test        # Run pytest with coverage
uv run poe lint        # Run ruff linter
uv run poe typecheck   # Run mypy
uv run poe check       # Run lint + format-check + typecheck
uv run poe fix         # Auto-fix lint issues and format
```

## Git Workflow

- **Never commit directly to main** - always create a feature branch first
- Branch naming: `feat/123-description` or `fix/456-description` (include issue number if working on an issue)
- Use conventional commits: `feat:`, `fix:`, `chore:`, `docs:`, `refactor:`, `test:`
- Run `uv run poe check` before committing

## Communication Guidelines

- **Always ask for clarification** when requirements are ambiguous or unclear
- **Surface important decision points** before implementation - don't assume or guess
- **Present options with trade-offs** when multiple valid approaches exist
- **Confirm architectural choices** that will impact the codebase significantly
- **British English Spelling** Use British English spelling throughout (do not correct imported code)
