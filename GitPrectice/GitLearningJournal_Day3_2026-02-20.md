# Git Learning Journal — Day 3

Date: 2026-02-20

### What I Learned Today

I learned how to push new changes from my local repository to the remote (GitHub).

**Common workflow (quick):**
```bash
git status                    # see changed, unstaged, and staged files
git add .                     # stage all changes (or: git add <path/to/file>)
git commit -m "Short message"  # save a snapshot with a message
git pull --rebase origin main # update local branch to avoid merge commits (optional)
git push                      # push commits to the tracked remote branch
```

If this is the first push of a new branch:
```bash
git push -u origin your-branch-name
```

Notes:
- Use `git status` often to confirm what will be committed.
- If `git pull --rebase` reports conflicts: resolve the files, `git add` them, then `git rebase --continue`.
- For HTTPS remotes use a Personal Access Token (PAT) or enable the credential helper; or use SSH keys for passwordless pushes.
- Check your branch and tracking status with `git branch -vv`.

Practice: make a small change, follow the steps above, then verify on GitHub that the change appears in the repository and commit history.

### Restoring a deleted file (quick reference)

If you accidentally deleted a file, use one of these depending on the state:

- Deleted but not staged (working directory only):
```bash
git restore GitPrectice/GitLearningJournal.md
```

- Deletion staged but not committed:
```bash
git restore --staged GitPrectice/GitLearningJournal.md
git restore GitPrectice/GitLearningJournal.md
```

- Deletion already committed (restore from a commit that contains the file):
1) Find a commit that still has the file:
```bash
git log --follow -- GitPrectice/GitLearningJournal.md
```
2) Restore the file from that commit (replace <commit> with the hash):
```bash
git checkout <commit> -- GitPrectice/GitLearningJournal.md
# or with newer Git
git restore --source=<commit> -- GitPrectice/GitLearningJournal.md
```

- If you found the commit hash (example `19286ff`) you can preview file contents:
```bash
git show 19286ff:GitPrectice/GitLearningJournal.md
```

Notes:
- Use `git ls-tree -r <commit> --name-only` to discover the exact path inside a commit.
- After restoring, `git add` and `git commit` to save the restored file, then `git push`.

