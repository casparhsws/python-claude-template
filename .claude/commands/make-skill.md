Create a new Claude Code skill: $ARGUMENTS

You are building a new skill for this Claude Code project. Follow this comprehensive workflow:

## 1. Understand the Request

Parse the skill description provided by the user. This should describe:
- What domain expertise the skill provides
- When Claude should use this skill
- What knowledge or guidelines it contains

If the description is unclear or incomplete, ask clarifying questions.

## 2. Research Existing Skills

Before creating the skill:
- Use Glob to list all existing skills in .claude/skills/
- Read existing SKILL.md files to understand:
  - Frontmatter structure (description field)
  - How skills organise domain knowledge
  - Common sections (guidelines, patterns, examples, best practices)
  - Tone and formatting style
- Identify any potential overlaps with existing skills

## 3. Look Up Best Practices

Use WebSearch to find Anthropic's latest documentation on skills:
- Search for "Claude Code skills best practices 2025 site:code.claude.com"
- Review guidelines for:
  - What makes a good skill vs an agent
  - How to write descriptions that trigger appropriately
  - How to structure domain knowledge
  - When skills should be invoked

## 4. Ask Clarifying Questions

Use AskUserQuestion to gather necessary details:

**Question 1: Skill Name**
- Ask: "What should we name this skill (kebab-case)?"
- Suggest a name based on the description
- Validate it doesn't conflict with existing skills
- Convention: Use noun-focused names (e.g., python-testing, react-patterns, api-design)

**Question 2: Scope and Domain**
- Ask: "What specific domain does this skill cover?"
- Clarify boundaries:
  - What's included in this skill
  - What's excluded (to avoid with other skills)
  - Related technologies or concepts
- Ensure it's focused enough to be useful, broad enough to be worthwhile

**Question 3: Key Topics**
- Present initial outline of main sections
- Ask: "Are these the right topics, or should we add/change anything?"
- Typical sections:
  - Core concepts/principles
  - Best practices
  - Common patterns
  - Anti-patterns to avoid
  - Examples
  - Project-specific guidelines

**Question 4: Invocation Triggers**
- Ask: "When should Claude automatically use this skill?"
- Identify keywords or situations:
  - Specific terms users might mention
  - Types of tasks that need this expertise
  - Related file types or project areas
- Craft description to capture these triggers

**Question 5: Project Context**
- Ask: "Should this skill reference project-specific conventions?"
- Examples:
  - Testing setup (pytest, workspace structure)
  - Tech stack (Python 3.12+, uv, mypy)
  - Workflows from CLAUDE.md
- Incorporate relevant context to make skill immediately useful

## 5. Generate the Skill Directory and File

Create the directory structure:
```bash
mkdir -p .claude/skills/{skill-name}
```

Create `.claude/skills/{skill-name}/SKILL.md` with this structure:

```markdown
---
description: [2-3 sentence description of what expertise this skill provides and when to use it. Include key terms users would mention and technologies covered.]
---

# {Skill Display Name}

[Opening paragraph explaining the skill's purpose and value]

## Core Principles

[3-6 fundamental principles or concepts for this domain]

1. **{Principle}**: {Explanation}
2. **{Principle}**: {Explanation}
[...]

## Best Practices

### {Category 1}

{Introduction to this category}

```{language if code examples}
{Concrete example demonstrating the best practice}
```

{Explanation of why this is good}

### {Category 2}

[Continue with additional best practice categories]

## Common Patterns

### Pattern: {Pattern Name}

{When to use this pattern}

```{language}
{Code example or template}
```

{Key points about implementation}

### Pattern: {Another Pattern}

[Continue with additional patterns]

## Anti-Patterns

### ❌ {Anti-pattern Name}

{What not to do and why}

```{language}
{Example of the wrong way}
```

**Why it's bad**: {Explanation}

**Instead do**: {Correct approach}

## Project-Specific Guidelines

[If applicable, include guidelines specific to this codebase]

- {Project convention}
- {Tool or dependency usage}
- {Workspace structure considerations}

[Reference CLAUDE.md where appropriate]

## Examples

### Example: {Use Case}

{Scenario description}

```{language}
{Complete working example}
```

{Walkthrough of key aspects}

### Example: {Another Use Case}

[Continue with 2-4 practical examples]

## Common Issues and Solutions

**Issue**: {Common problem}
- **Cause**: {Why it happens}
- **Solution**: {How to fix it}

[Include 3-5 common issues]

## Quick Reference

{Condensed cheat sheet of key points, commands, or patterns}

```{language if applicable}
{Quick reference examples}
```

## Further Reading

- {Relevant documentation links}
- {Official resources}
- {Related skills or concepts}
```

**Content Guidelines**:
- Be comprehensive but focused - cover the domain well without sprawling
- Include concrete examples - skills should be immediately actionable
- Use consistent formatting (code blocks with language tags, clear headers)
- Balance theory with practice - explain "why" along with "how"
- Reference project setup from CLAUDE.md when relevant
- Make it scannable - Claude needs to quickly find relevant guidance
- Include both positive patterns (do this) and negative patterns (avoid this)

## 6. Verify Integration

After creating the skill:
1. Read the generated SKILL.md file back to confirm it's well-formed
2. Run `/audit-claude` to check for:
   - Conflicts with existing skills
   - Inconsistencies with CLAUDE.md
   - Description field clarity for invocation
   - Missing critical domain knowledge
3. If issues found, fix them before proceeding

## 7. Summarize and Confirm

Present a summary to the user:

```
✅ Created new skill: {skill-name}
📄 File: .claude/skills/{skill-name}/SKILL.md

**Domain**: [Area of expertise]
**Triggers**: [When Claude will use this]
**Key sections**: [Main topics covered]

The skill is ready! Claude will automatically use it when working on {domain} tasks.

You can also explicitly invoke it using the Skill tool.

[If audit found any notes, include them here]
```

## Important Notes

- **Skills vs Agents**: Skills provide expertise and guidelines; agents take action. If it's knowledge-sharing, it's a skill. If it's doing work, it's an agent.
- **Skills vs Commands**: Skills are model-invoked (Claude decides); commands are user-invoked (user types /command)
- **Scope appropriately**: Too narrow = rarely useful; too broad = not specific enough
- **Update over creating**: If a skill exists in the same domain, consider enhancing it
- **Description is critical**: This is how Claude knows when to use the skill - include key terms and clear triggers
- **Examples matter**: Abstract guidance is less useful than concrete, working examples
- **Project context**: Skills are most valuable when they incorporate project-specific conventions

## Skill Design Patterns

### Pattern 1: Technology Guidelines
Example: python-testing, react-patterns, docker-best-practices
- Tool/framework overview
- Configuration in this project
- Best practices and patterns
- Common gotchas
- Examples

### Pattern 2: Domain Expertise
Example: api-design, database-optimization, security-practices
- Domain principles
- Design patterns
- Anti-patterns
- Decision frameworks
- Case studies

### Pattern 3: Workflow Guidance
Example: code-review-checklist, debugging-strategies, refactoring-guide
- Step-by-step processes
- Decision trees
- Checklists
- When to apply techniques
- Real scenarios

### Pattern 4: Language/Framework Deep-Dive
Example: python-async, typescript-advanced, fastapi-patterns
- Language features
- Idioms and conventions
- Performance considerations
- Integration with project setup
- Comprehensive examples

Choose the pattern that best fits the skill's purpose, or blend patterns as needed.

## Additional Files (Optional)

Skills can include supporting files in their directory:

```
.claude/skills/{skill-name}/
├── SKILL.md           # Main skill file (required)
├── examples/          # Optional: Larger code examples
│   ├── example1.py
│   └── example2.py
├── templates/         # Optional: Code templates
│   └── template.py
└── references/        # Optional: Additional documentation
    └── notes.md
```

Ask the user if they want supporting files, and create them if requested.
