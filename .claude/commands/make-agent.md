Create a new Claude Code agent: $ARGUMENTS

You are building a new agent for this Claude Code project. Follow this comprehensive workflow:

## 1. Understand the Request

Parse the agent description provided by the user. This should describe:
- What the agent does (its primary purpose)
- When it should be used
- What problem it solves

If the description is unclear or incomplete, ask clarifying questions.

## 2. Research Existing Patterns

Before creating the agent:
- Use Glob to list all existing agents in .claude/agents/
- Read 2-3 similar agents to understand:
  - Common frontmatter patterns (name, description, tools, model, color)
  - How examples are structured in the description field
  - Typical tool combinations
  - System prompt organisation and tone
- Identify any potential overlaps or conflicts with existing agents

## 3. Look Up Best Practices

Use WebSearch to find Anthropic's latest best practices for agent creation:
- Search for "Claude Code agents best practices 2025 site:code.claude.com"
- Review guidelines for:
  - When to make agents proactive ("use PROACTIVELY", "MUST BE USED")
  - How to write clear, non-overlapping descriptions
  - Tool selection guidance
  - Example formatting in the description field

## 4. Ask Clarifying Questions

Use AskUserQuestion to gather necessary details:

**Question 1: Agent Name and Identifier**
- Ask: "What should we name this agent (kebab-case)?"
- Suggest a name based on the description
- Validate it doesn't conflict with existing agents

**Question 2: Tools Required**
- Present common tool combinations:
  - Read-only: `Read, Glob, Grep, WebFetch, WebSearch`
  - Code writing: `Read, Write, Edit, Glob, Grep, Bash`
  - Full access: `Read, Write, Edit, Glob, Grep, Bash, TodoWrite, WebFetch, WebSearch`
  - Specialised: Custom combinations based on needs
- Ask which tools are needed, or suggest based on the agent's purpose

**Question 3: Proactivity Level**
- Ask: "When should this agent be invoked?"
- Options:
  - "Proactive - Claude should use this automatically when relevant"
  - "On-demand - Only when user explicitly needs this capability"
  - "Suggested - Claude should recommend it but ask first"

**Question 4: Agent Color**
- Suggest a color not heavily used by existing agents
- Options: blue, green, purple, orange, red, yellow, cyan, magenta

**Question 5: Additional Context**
- Ask if there are specific:
  - Constraints or guidelines this agent must follow
  - Success criteria that define completion
  - Common patterns or code examples to include
  - Project-specific context from CLAUDE.md to incorporate

## 5. Generate the Agent File

Create `.claude/agents/{agent-name}.md` with this structure:

```markdown
---
name: agent-name
description: [2-4 sentence description of what this agent does and when to use it. Include key terms users would mention. If proactive, include "use PROACTIVELY" or "MUST BE USED".]

Examples:

<example>
Context: [Describe the situation]
user: "[Example user request]"
assistant: "[How Claude responds and invokes this agent]"
<Task tool call to agent-name>
</example>

[Include 2-3 diverse examples showing different use cases]

tools: [Comma-separated list of tools]
model: inherit
color: [chosen color]
---

You are an expert [role/specialty]. Your specialty is [core competency]. You follow [key principles] and ensure [quality standards].

## Your Mission

[Clear statement of the agent's primary goal and what it will accomplish]

## Core Principles

1. **[Principle 1]**: [Explanation]
2. **[Principle 2]**: [Explanation]
3. **[Principle 3]**: [Explanation]
[4-6 principles that guide how this agent operates]

## Your Process

### 1. [First Phase Name]
- [Step or consideration]
- [Step or consideration]
- [Ask clarifying questions if requirements are ambiguous]

### 2. [Second Phase Name]
- [Concrete actions to take]
- [How to approach the work]

[Continue with 3-6 phases covering the complete workflow]

## Important Guidelines

1. **Always use TodoWrite** to track progress through complex tasks
2. **Ask clarifying questions** if requirements are vague or incomplete
3. **[Guideline specific to this agent]**
4. **[Guideline specific to this agent]**
[5-10 guidelines, with project-specific ones from CLAUDE.md if relevant]

## Success Criteria

Your job is complete when:
- ✅ [Specific success criterion]
- ✅ [Specific success criterion]
- ✅ [Specific success criterion]
[4-8 clear checkboxes defining done]

## Common Patterns

[Include 2-4 code examples or patterns relevant to this agent's work]

```

**Content Guidelines**:
- Use professional, direct tone (no emojis unless requested)
- Include specific, actionable instructions
- Reference CLAUDE.md guidelines where relevant (git workflow, testing, etc.)
- Provide concrete examples in Common Patterns section
- Make the mission and success criteria crystal clear
- Ensure the description field has 2-3 diverse examples showing when to invoke
- Use British English spelling throughout

## 6. Verify Integration

After creating the file:
1. Read the generated file back to confirm it's well-formed
2. Run `/audit-claude` to check for:
   - Conflicts with existing agents
   - Inconsistencies with CLAUDE.md
   - Missing or malformed fields
3. If issues found, fix them before proceeding

## 7. Summarize and Confirm

Present a summary to the user:

```
✅ Created new agent: {agent-name}
📄 File: .claude/agents/{agent-name}.md

**Purpose**: [One sentence summary]
**Tools**: [List of tools]
**Invocation**: [Proactive/On-demand/Suggested]

The agent is ready to use! You can invoke it by [description of how it gets triggered].

[If audit found any notes, include them here]
```

## Important Notes

- **Avoid overlaps**: If an existing agent already does something similar, either enhance that agent or ensure this one has a clearly distinct purpose
- **Be specific in examples**: Generic examples make agents trigger incorrectly - include actual user phrasing and specific use cases
- **Tool selection matters**: Only grant tools the agent actually needs - more isn't always better
- **Consider the project context**: Incorporate relevant guidelines from CLAUDE.md (tech stack, workflows, standards)
- **Test the description**: Read it from the perspective of "when would I invoke this?" - if it's unclear, rewrite it
