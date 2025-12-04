Run full type validation across the workspace.

Steps:
1. Run `poe typecheck` (mypy in strict mode)
2. If errors found:
   - List each error with file path and line number
   - Group by file
   - Suggest fixes for common issues
3. Report success if no errors
