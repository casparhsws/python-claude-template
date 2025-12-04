Run code review on recent changes: $ARGUMENTS

Steps:
1. Check `git diff` for changed files (or `git diff $ARGUMENTS` if specified)
2. For each changed Python file, review:
   - Type annotations present and correct
   - Test coverage for new/changed code
   - Follows project conventions (ruff, mypy strict)
   - No security issues or hardcoded secrets
3. Run `poe check` to verify lint and type errors
4. Summarize findings and suggested fixes
