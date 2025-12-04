Run tests: $ARGUMENTS

Steps:
1. If $ARGUMENTS provided, run `pytest -k "$ARGUMENTS"` or `pytest $ARGUMENTS` (if it's a path)
2. If no arguments, run `poe test` for full test suite with coverage
3. Report results clearly:
   - Number passed/failed/skipped
   - Coverage percentage
   - Details of any failures
   - Suggest fixes for failing tests
