Create a conventional commit: $ARGUMENTS

If no message provided:
1. Run git diff --staged to see changes
2. Analyze the changes to determine type (feat/fix/chore/docs/refactor/test)
3. Generate a concise commit message

Commit types:
- feat: new feature (MINOR version)
- fix: bug fix (PATCH version)
- docs: documentation only
- chore: maintenance, deps
- refactor: code change without feature/fix
- test: adding tests

Format: <type>[optional scope]: <description>
Example: feat(auth): add social login support
