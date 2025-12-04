Create a pull request for the current branch: $ARGUMENTS

Steps:
1. Check we're not on main branch
2. Ensure all changes are committed
3. Push branch to remote with -u flag if needed
4. Analyze all commits on this branch vs main using:
   - git log main..HEAD
   - git diff main...HEAD
5. Generate PR description with:
   ## Summary
   <bullet points of key changes>

   ## Test plan
   <checklist of testing steps>
6. Create PR using gh pr create
7. If $ARGUMENTS contains --draft, create as draft PR
8. Return the PR URL
