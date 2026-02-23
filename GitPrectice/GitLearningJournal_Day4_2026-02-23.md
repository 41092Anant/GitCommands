# Git Learning Journal — Day 4

Date: 2026-02-23

### Topic: Branching & Pull Requests (feature workflow)

What I learned today: how to create a feature branch, push it to the remote, open a pull request (PR) on GitHub, and merge safely.

Quick commands (copy/paste):
```bash
# Start from an up-to-date main
git switch main
git pull --rebase origin main

# Create a new branch and switch to it
git switch -c feature/add-day4-note

# Make changes, stage and commit
git add .
git commit -m "Add Day 4 learning note: branching & PRs"

# Push the branch and set upstream
git push -u origin feature/add-day4-note
```

Create and complete a PR:
- Open the repository on GitHub and click "Compare & pull request" for your branch.
- Add a clear title and description, request a reviewer, then merge when ready.

Verify and cleanup locally:
```bash
# Confirm branch merged on GitHub, then update local main
git switch main
git pull --rebase origin main

# Delete local and remote feature branch (optional)
git branch -d feature/add-day4-note
git push origin --delete feature/add-day4-note
```

Notes:
- Use small, focused branches and descriptive commit messages.
- Protect important branches (e.g., `production` or `main`) in GitHub settings to require PR reviews and CI.

Practice: create the branch, push it, open a PR, merge via GitHub, and record the PR link and commands used in this file.

### Create a new branch from an existing branch — detailed

When you need a new branch that starts from an existing branch (local or remote), follow these steps.

1) Ensure your base branch is up to date
```bash
# switch to the base branch (example: main or production)
git switch main
git fetch origin            # update remote refs
git pull --rebase origin main
```

2) Create the new branch locally and switch to it
```bash
# create from current branch
git switch -c feature/my-new-branch

# or create from a remote branch (no local branch yet)
git fetch origin
git switch -c feature/my-new-branch origin/main

# or create from a specific commit or tag
git switch -c feature/my-new-branch <commit-hash>
```

3) Work, stage and commit
```bash
git add <files>
git commit -m "Short, descriptive message"
```

4) Push and set upstream so future `git push` works without args
```bash
git push -u origin feature/my-new-branch
```

Tips and edge cases:
- If you have uncommitted work and want to start a branch now, either commit the work or stash it:
  `git stash --include-untracked` -> create branch -> `git stash pop`.
- To create the remote branch without a local checkout:
  `git push origin main:refs/heads/feature/my-new-branch`
- To delete the branch locally and remotely after merge:
  `git branch -d feature/my-new-branch` and `git push origin --delete feature/my-new-branch`.

