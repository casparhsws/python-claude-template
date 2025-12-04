# 🐍 Python Claude Template

> Production-ready Python monorepo template with Claude Code integration, pre-configured agents, commands, and skills for AI-powered development.

[![Python](https://img.shields.io/badge/Python-3.12+-blue.svg)](https://www.python.org/)
[![uv](https://img.shields.io/badge/uv-package%20manager-green.svg)](https://github.com/astral-sh/uv)
[![Code style: ruff](https://img.shields.io/badge/code%20style-ruff-000000.svg)](https://github.com/astral-sh/ruff)
[![Type checked: mypy](https://img.shields.io/badge/type%20checked-mypy-blue.svg)](http://mypy-lang.org/)

---

## 📋 Overview

This template provides a **production-ready Python development environment** integrated with **Claude Code**, Anthropic's AI-powered coding assistant. It combines modern Python tooling with AI capabilities through custom agents, slash commands, and skills.

### Why This Template?

- ⚡ **Fast Setup** - Get a Python monorepo running in minutes with uv workspaces
- 🤖 **AI-Enhanced Development** - Pre-configured Claude Code agents, commands, and skills
- 🔒 **Type Safety** - Strict mypy configuration ensures robust code
- 🎯 **Best Practices** - Follows Anthropic's recommendations for agentic coding
- 🧪 **Testing Ready** - pytest with async support and coverage reporting
- 📦 **Monorepo Structure** - Easily manage multiple packages in `libs/`

---

## 🚀 Quick Start

1. **Clone the template**
   ```bash
   git clone <your-repo-url>
   cd python-claude-template
   ```

2. **Install dependencies with uv**
   ```bash
   uv sync
   ```

3. **Run quality checks**
   ```bash
   uv run poe check
   ```

4. **Start coding with Claude Code**
   ```bash
   claude
   ```

---

## ✨ Features

### Python Stack

- **[uv](https://github.com/astral-sh/uv)** - Ultra-fast Python package manager and workspace tool
- **[pytest](https://pytest.org/)** + **pytest-asyncio** - Modern testing with async support
- **[mypy](http://mypy-lang.org/)** - Strict type checking for robust code
- **[ruff](https://github.com/astral-sh/ruff)** - Lightning-fast linting and formatting
- **[poethepoet](https://github.com/nat-n/poethepoet)** - Task runner for common workflows
- **Workspace structure** - Monorepo support with multiple packages in `libs/`

### Claude Code Integration

Pre-configured with powerful AI development tools:

- 🤖 **2 Custom Agents** - Specialized AI assistants for specific tasks
- ⚡ **9 Slash Commands** - Quick workflows at your fingertips
- 🎯 **1 Skill** - Python testing expertise built-in

---

## 🤖 Claude Code Integration

This template leverages [Claude Code](https://www.anthropic.com/news/claude-code-plugins), Anthropic's AI-powered development tool, with custom configurations for Python development.

### What is Claude Code?

Claude Code is an AI-powered command-line tool that helps with software engineering tasks. It can understand your codebase, make edits, run tests, and follow complex workflows - all while maintaining context about your project.

Learn more: [Claude Code Best Practices](https://www.anthropic.com/engineering/claude-code-best-practices)

---

## 🎭 Agents

**Agents** are specialized AI assistants that can be launched to handle complex, multi-step tasks autonomously. They have specific tool access and system prompts tailored to their purpose.

### Included Agents

#### 🏗️ **fastapi-builder**
Builds complete FastAPI applications from requirements with proper structure, testing, and documentation.

**Use when:** You need to scaffold a new FastAPI project or microservice.

```bash
# Claude will use this agent automatically when you ask to build a FastAPI app
```

#### 🔍 **claude-config-auditor**
Audits and verifies consistency across Claude Code configuration files, identifying conflicts, redundancies, and misalignments.

**Use when:** You want to ensure your `.claude/` configuration is consistent and following best practices.

```bash
# Triggered by the /audit-claude command
/audit-claude
```

**Learn more:**
- [Agent Skills Overview](https://docs.claude.com/en/docs/agents-and-tools/agent-skills/overview)
- [Building Agents with Claude](https://www.anthropic.com/engineering/building-agents-with-the-claude-agent-sdk)

---

## ⚡ Commands

**Commands** (slash commands) are quick workflows stored as prompt templates. They're perfect for repeated tasks like code reviews, creating PRs, or running checks.

### Available Commands

| Command | Description |
|---------|-------------|
| `/audit-claude` | Audit Claude Code configuration for consistency and issues |
| `/commit` | Stage changes and create a conventional commit with AI-generated message |
| `/feature` | Create a new feature branch and plan implementation |
| `/fix-issue` | Fix a GitHub issue by number with automated workflow |
| `/pr` | Create a pull request with AI-generated summary and test plan |
| `/review` | Run code review on recent changes with quality checks |
| `/status` | Show comprehensive project status (git, tests, types, lint) |
| `/test` | Run pytest with coverage and fix failing tests |
| `/typecheck` | Run mypy type checking and fix type errors |

### Using Commands

Simply type a slash command in Claude Code:

```bash
claude> /review
# Reviews your recent changes and runs quality checks

claude> /pr
# Creates a pull request with auto-generated description

claude> /test
# Runs tests and helps fix failures
```

**Learn more:**
- [Claude Code Best Practices - Commands](https://www.anthropic.com/engineering/claude-code-best-practices)

---

## 🎯 Skills

**Skills** are organized folders of instructions, scripts, and resources that Claude can discover and load dynamically. They extend Claude's capabilities with your team's expertise.

### Included Skills

#### 🧪 **python-testing**
Provides comprehensive pytest patterns for uv workspace monorepos, including:
- Async testing with pytest-asyncio
- Mocking strategies for Python projects
- Test organization best practices
- Workspace-aware test configuration

**When it activates:** Claude automatically loads this skill when writing or reviewing Python tests.

**Location:** `.claude/skills/python-testing/SKILL.md`

### How Skills Work

Skills use **progressive disclosure** - Claude only loads the information it needs, when it needs it. This means skills can contain extensive documentation without cluttering context.

**Learn more:**
- [Introducing Agent Skills](https://www.anthropic.com/news/skills)
- [Equipping Agents with Skills](https://www.anthropic.com/engineering/equipping-agents-for-the-real-world-with-agent-skills)

---

## 🛠️ Development Workflow

### Task Runner Commands

```bash
# Testing
uv run poe test          # Run pytest with coverage

# Linting & Formatting
uv run poe lint          # Run ruff linter
uv run poe fix           # Auto-fix lint issues and format code
uv run poe format        # Format code with ruff
uv run poe format-check  # Check formatting without changes

# Type Checking
uv run poe typecheck     # Run mypy strict type checking

# Combined Checks
uv run poe check         # Run lint + format-check + typecheck
uv run poe check-all     # Run lint + typecheck + test
```

### Git Workflow

This template follows a **branch-based workflow** with conventional commits:

1. **Create a feature branch**
   ```bash
   /feature "add user authentication"
   ```

2. **Make changes and commit**
   ```bash
   /commit
   # Claude generates a conventional commit message
   ```

3. **Run quality checks**
   ```bash
   /status
   uv run poe check
   ```

4. **Create a pull request**
   ```bash
   /pr
   # Claude generates PR description and test plan
   ```

**Conventional commit prefixes:** `feat:`, `fix:`, `chore:`, `docs:`, `refactor:`, `test:`

---

## 📁 Project Structure

```
python-claude-template/
├── .claude/                     # Claude Code configuration
│   ├── agents/                  # Custom AI agents
│   │   ├── fastapi-builder.md
│   │   └── claude-config-auditor.md
│   ├── commands/                # Slash commands
│   │   ├── audit-claude.md
│   │   ├── commit.md
│   │   ├── feature.md
│   │   ├── fix-issue.md
│   │   ├── pr.md
│   │   ├── review.md
│   │   ├── status.md
│   │   ├── test.md
│   │   └── typecheck.md
│   ├── skills/                  # Reusable skills
│   │   └── python-testing/
│   │       └── SKILL.md
│   └── settings.json            # Project settings
├── libs/                        # Workspace packages
│   └── package-example/         # Example package
│       ├── src/
│       ├── tests/
│       └── pyproject.toml
├── CLAUDE.md                    # Project instructions for Claude
├── pyproject.toml               # Root workspace configuration
└── README.md                    # This file
```

---

## 📚 Resources

### Official Anthropic Documentation

- 📖 [Claude Code Best Practices](https://www.anthropic.com/engineering/claude-code-best-practices) - Tips and tricks for agentic coding
- 🎯 [Agent Skills Overview](https://docs.claude.com/en/docs/agents-and-tools/agent-skills/overview) - Understanding skills architecture
- 🤖 [Building Agents Guide](https://www.anthropic.com/engineering/building-agents-with-the-claude-agent-sdk) - Create your own agents
- ✨ [Introducing Agent Skills](https://www.anthropic.com/news/skills) - Skills announcement and examples
- 🔧 [Customize Claude Code](https://www.anthropic.com/news/claude-code-plugins) - Plugins and customization
- 🎓 [Anthropic Academy](https://www.anthropic.com/learn/build-with-claude) - Learn to build with Claude

### Python Tools Documentation

- [uv Documentation](https://github.com/astral-sh/uv)
- [pytest Documentation](https://docs.pytest.org/)
- [mypy Documentation](https://mypy.readthedocs.io/)
- [ruff Documentation](https://docs.astral.sh/ruff/)

---

## 🎨 Customization

### Adding Your Own Agent

Create a new file in `.claude/agents/your-agent.md`:

```yaml
---
name: your-agent
description: Brief description of when to use this agent
tools: [Read, Write, Edit, Bash, Grep, Glob]
model: inherit
color: blue
---

Your agent's system prompt here...
```

### Creating Custom Commands

Add a new file in `.claude/commands/your-command.md`:

```markdown
Brief description of what this command does

Steps:
1. First step
2. Second step
3. Third step
```

### Building Custom Skills

Create a new directory `.claude/skills/your-skill/` with a `SKILL.md` file:

```markdown
# Your Skill Name

Description and instructions for the skill...
```

Learn more in the [Agent Skills documentation](https://docs.claude.com/en/docs/agents-and-tools/agent-skills/overview).

---

## 🤝 Contributing

Contributions are welcome! Feel free to:

- Add new agents for common Python frameworks
- Create additional slash commands for workflows
- Expand the python-testing skill
- Improve documentation

---

## 📄 License

This template is open source and available under the MIT License.

---

## 🙏 Acknowledgments

Built with:
- [Claude Code](https://www.anthropic.com/news/claude-code-plugins) by Anthropic
- [uv](https://github.com/astral-sh/uv) by Astral
- Modern Python tooling ecosystem

---

**Ready to build with AI?** Start with `claude` and explore the included agents, commands, and skills! 🚀
