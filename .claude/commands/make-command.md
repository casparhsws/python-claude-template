Create a new slash command: $ARGUMENTS

You are building a new slash command for this Claude Code project. Follow this comprehensive workflow:

## 1. Understand the Request

Parse the command description provided by the user. This should describe:
- What the command does
- What it helps the user accomplish
- Any arguments it should accept

If the description is unclear or incomplete, ask clarifying questions.

## 2. Research Existing Commands

Before creating the command:
- Use Glob to list all existing commands in .claude/commands/
- Read 2-3 similar commands to understand:
  - How they structure instructions
  - How they handle $ARGUMENTS
  - Common patterns (git workflows, testing, building)
  - Tone and formatting style
- Identify any potential overlaps or conflicts with existing commands

## 3. Look Up Best Practices

Use WebSearch to find Anthropic's latest documentation on slash commands:
- Search for "Claude Code commands slash commands 2025 site:code.claude.com"
- Review guidelines for:
  - When to use commands vs agents
  - How to structure command instructions
  - Argument handling patterns
  - Command naming conventions

## 4. Ask Clarifying Questions

Use AskUserQuestion to gather necessary details:

**Question 1: Command Name**
- Ask: "What should we name this command (kebab-case)?"
- Suggest a name based on the description
- Validate it doesn't conflict with existing commands
- Convention: Use verb-noun format (e.g., /create-test, /fix-issue)

**Question 2: Arguments**
- Ask: "Does this command accept arguments?"
- Options:
  - "No arguments - self-contained workflow"
  - "Required argument - command needs input to work"
  - "Optional argument - provides default behaviour"
- If yes, clarify what the argument represents (file path, description, name, etc.)

**Question 3: Scope and Steps**
- Present the main steps you've identified
- Ask: "Are these steps correct, or should anything be added/changed?"
- Ensure the workflow is:
  - Complete (covers all necessary steps)
  - Ordered (logical sequence)
  - Specific (actionable instructions, not vague)

**Question 4: Integration with Existing Workflows**
- Ask: "Should this command integrate with existing workflows?"
- Examples:
  - Follow git conventions from CLAUDE.md?
  - Run quality checks (uv run poe check, tests)?
  - Create commits or PRs?
- Identify relevant CLAUDE.md guidelines to incorporate

## 5. Generate the Command File

Create `.claude/commands/{command-name}.md` with this structure:

### For Simple Commands (No Complex Logic)

```markdown
[Action verb] [what it does]: $ARGUMENTS

[If arguments are used, explain them on the first line]
[Example: "Create a new feature branch for: $ARGUMENTS"]

Steps:
1. [First action with specific details]
2. [Second action with specific details]
3. [Continue with clear, numbered steps]
[...]
n. [Final action and confirmation]

[If relevant, include sections like:]

Format/Convention:
- [Rule or pattern to follow]
- [Another rule or pattern]

Examples:
- [Concrete example of usage]
- [Another concrete example]

Important:
- [Critical note or constraint]
- [Another important consideration]
```

### For Complex Commands (Multi-Step Workflows)

```markdown
[Comprehensive description]: $ARGUMENTS

[Optional: Context about when and why to use this command]

## Phase 1: [Phase Name]

Steps:
1. [Specific action]
   - [Sub-detail if needed]
   - [Another sub-detail]
2. [Next specific action]
[...]

## Phase 2: [Phase Name]

Steps:
1. [Specific action]
2. [Next specific action]
[...]

[Continue with remaining phases]

## Guidelines

- [Important guideline]
- [Another guideline]
[Reference relevant CLAUDE.md rules]

## Success Criteria

- ✅ [What indicates completion]
- ✅ [Another success indicator]

## Common Issues

- **Issue**: [Problem that might occur]
  - Solution: [How to handle it]
```

**Content Guidelines**:
- Be concise and direct - commands are instructions, not essays
- Use numbered steps for sequences, bullets for lists
- Include specific tool calls when known (e.g., "Run git status")
- Reference project conventions from CLAUDE.md (git workflow, commit format, testing)
- Add examples for commands with arguments
- Make success criteria explicit
- Use imperative voice ("Run", "Create", "Check", not "You should run")
- **SECURITY**: Only use $ARGUMENTS in the first line description. Never reference $ARGUMENTS in the steps/body as it could be injected. Instead use phrases like "the provided path", "if arguments given", "the specified file"

## 6. Verify Integration

After creating the file:
1. Read the generated file back to confirm it's well-formed
2. Run `/audit-claude` to check for:
   - Conflicts with existing commands
   - Inconsistencies with CLAUDE.md
   - Commands that duplicate functionality
   - Missing critical steps
3. If issues found, fix them before proceeding

## 7. Summarize and Confirm

Present a summary to the user:

```
✅ Created new command: /{command-name}
📄 File: .claude/commands/{command-name}.md

**Purpose**: [One sentence summary]
**Usage**: /{command-name} [arguments if applicable]

Example usage:
  /{command-name} [example with actual values]

The command is ready to use! Type `/{command-name}` to invoke it.

[If audit found any notes, include them here]
```

## Important Notes

- **Commands vs Agents**: Use commands for straightforward, user-invoked workflows. Use agents for complex tasks requiring autonomous decision-making
- **Avoid duplication**: If a similar command exists, consider enhancing it instead of creating a new one
- **Reference, don't repeat**: Point to CLAUDE.md guidelines rather than duplicating them in the command
- **Test the flow**: Walk through each step mentally - are they all clear and actionable?
- **Argument clarity**: If using $ARGUMENTS, the first line must make it crystal clear what should be provided

## Command Design Patterns

### Pattern 1: Simple Task Runner
Example: /test, /lint, /typecheck
- Description line
- Single command or short sequence
- Success confirmation

### Pattern 2: Git Workflow
Example: /feature, /commit, /pr
- Check current state
- Perform git operations
- Follow project conventions
- Verify success

### Pattern 3: Generator/Scaffolder
Example: /make-agent (this command!)
- Gather requirements
- Research existing patterns
- Ask clarifying questions
- Generate file(s)
- Verify and summarise

### Pattern 4: Multi-Phase Process
Example: /fix-issue
- Analysis phase
- Planning phase
- Implementation phase
- Verification phase
- Each phase with clear steps

Choose the pattern that best fits the command's purpose.
