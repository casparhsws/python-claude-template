Check and fix spelling mistakes, particularly British spelling: $ARGUMENTS

If arguments provided, check the specified file or directory path.
If no arguments, check README.md by default.

## Phase 1: Search for Spelling Issues

Steps:
1. Determine scope:
   - If a path was provided: Use the specified path
   - If no path provided: Default to README.md
2. Search for common American/British spelling patterns:
   - Use Grep to find: organize/organise, specialize/specialise, analyze/analyse
   - Use Grep to find: color/colour, behavior/behaviour, favor/favour
   - Use Grep to find: ize/ise endings, yze/yse endings
   - Search for other common misspellings and typos
3. Catalogue all findings with file paths and line numbers

## Phase 2: Review and Filter

Steps:
1. Review each finding in context by reading the relevant files
2. Filter out:
   - Variable names or identifiers imported from external packages
   - API endpoints or external service names
   - Third-party library names or technical terms
   - Code that should not be modified (e.g., import statements)
3. Keep:
   - Documentation text (comments, docstrings, markdown files)
   - User-facing strings and messages
   - Code comments and internal documentation

## Phase 3: Correct Spelling

Steps:
1. For British spelling corrections:
   - Use Edit tool to change American spellings to British equivalents
   - Common patterns: -ize → -ise, -yze → -yse, -or → -our, -er → -re (where applicable)
2. For general misspellings:
   - Correct typos and spelling errors found in documentation
3. Track all changes made

## Phase 4: Report Results

Steps:
1. Summarise corrections made:
   - List files modified
   - Count of spelling corrections by type
   - Note any potential issues skipped (with reason)
2. If no issues found, report clean bill of health

## Guidelines

- **DO NOT modify**:
  - Imported variable names from external packages
  - API parameter names from third-party services
  - Technical terms with standardised American spelling
  - Code identifiers that would break functionality
- **DO modify**:
  - README.md and documentation files
  - CLAUDE.md project instructions
  - .claude/ configuration files (agents, commands, skills)
  - Python docstrings and comments
  - User-facing strings and messages
- **British spelling patterns**:
  - -ize → -ise (organise, specialise, analyse)
  - -yze → -yse (analyse)
  - -or → -our (colour, behaviour, favour)
  - -er → -re (centre, theatre) - use cautiously
- **Reference CLAUDE.md**: Follow the British English spelling guideline

## Common Patterns to Search

Use these regex patterns with Grep:
- `\b(speciali[zs]e[ds]?|organi[zs]e[ds]?|analy[zs]e[ds]?|summari[zs]e[ds]?|customi[zs]e[ds]?|optimi[zs]e[ds]?)\b`
- `\b(behavio?r|colo?r|favo?r|hono?r)\b`
- `\b(centre|center|theatre|theater)\b`

## Success Criteria

- ✅ All spelling issues found in specified scope
- ✅ British spelling corrections applied appropriately
- ✅ External package references left unchanged
- ✅ Clear summary of changes provided

## Examples

```bash
# Check and fix README.md (default)
/fix-spelling

# Check specific file
/fix-spelling CLAUDE.md

# Check directory
/fix-spelling .claude/

# Check multiple documentation files
/fix-spelling docs/
```
