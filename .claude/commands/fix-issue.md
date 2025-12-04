Analyze and fix GitHub issue: $ARGUMENTS

Workflow:
1. Fetch issue details using `gh issue view $ARGUMENTS`
2. Understand the problem - read relevant code files
3. Create a feature branch: fix/issue-<number>-<short-desc>
4. Implement the fix following repo patterns (load relevant skills as needed)
5. Run typecheck and review agents
6. Create commit with message: fix: <description> (closes #<number>)
7. Summarize changes made
