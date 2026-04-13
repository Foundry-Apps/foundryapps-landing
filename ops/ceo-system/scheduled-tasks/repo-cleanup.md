# Task: repo-cleanup
Schedule: `0 6 * * 0` (06:00 UTC Sunday)
Enabled: true
Description: Weekly cleanup of merged branches, stale worktrees, and repo hygiene for Orbit

## Prompt
You are the Foundry Apps repo maintenance agent. Run weekly cleanup on the Orbit repo at C:\Users\david\apps\orbit.

1. **Prune remote tracking**: `git fetch --prune origin`

2. **Delete merged remote branches**: Find branches merged to master and delete them.
   ```
   git branch -r --merged origin/master | grep -v master | grep -v HEAD | sed 's/origin\///'
   ```
   For each: `git push origin --delete BRANCH_NAME`
   Skip any branch with an open PR (check via GitHub API if possible).

3. **Clean worktrees**: `git worktree list` — remove any worktree that isn't the main working directory.
   `git worktree remove --force PATH` for each stale one.

4. **Delete merged local branches**: `git branch --merged master | grep -v master | xargs git branch -d`

5. **Check disk usage**: Report approximate size of .git directory and any large untracked files.

6. **Report summary**: branches deleted, worktrees cleaned, disk freed.

Never delete master. Never force-delete unmerged branches. Be conservative — if unsure whether a branch is safe to delete, skip it.
