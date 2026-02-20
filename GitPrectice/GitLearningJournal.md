# Git Learning Journal

## Day 1 - February 17, 2026

### What I Learned Today

I learned a git command `git --version` today.

**What it does:**
- This command shows the installed version of Git on my system
- It helps verify that Git is properly installed and accessible from the command line

**Example:**
```bash
git --version
```

**Output:**
```
git version 2.XX.X.windows.1
```

## Day 2 - February 19, 2026

### What I Learned Today

I configured my Git identity and created a local repository, then made my first commit.

**Commands I ran:**
```bash
git config --global user.name "Anant Dosi"
git config --global user.email "jain.anant555@gmail.com"
git init
git add .
git commit -m "Initial commit"
```

Why:
- `git config` sets the name/email recorded in commits
- `git init` creates a local Git repository
- `git add` stages files for commit
- `git commit` records a snapshot in history

Verify with: `git log --oneline`

### How I added a GitHub repository and pushed my code

- I created a new empty repository on GitHub using the website.
- Then in my local repo I ran:
```bash
git remote add origin https://github.com/USERNAME/REPO.git
git branch -M main
git push -u origin main
```

Notes:
- For HTTPS remotes you may need to use a Personal Access Token (PAT) when prompted for a password.
- Alternatively set up SSH keys and use the `git@github.com:USERNAME/REPO.git` remote.

### Full Day 2: Step-by-step details (what I did and why)

1) Configure identity (so commits have your name/email):
```bash
git config --global user.name "Anant Dosi"
git config --global user.email "jain.anant555@gmail.com"
git config --global init.defaultBranch main
```

2) Add a `.gitignore` before adding files (prevents IDE/build files from being tracked):
Create ` .gitignore` with common entries:
```text
.vs/
bin/
obj/
*.user
*.suo
node_modules/
wwwroot/lib/
```

3) Initialize and make the first commit:
```bash
git init
git add .
git commit -m "Initial commit"
```

If `git add` fails with "Permission denied" (Windows/Visual Studio locks):
- Close Visual Studio or any program that may lock files, then run `git add .` again.
- If files were already added accidentally, remove them from the index and keep them locally:
```bash
git rm -r --cached .vs
git rm -r --cached bin obj
git add .gitignore
git commit -m "Remove IDE/build files and add .gitignore"
```

4) Add remote and push to GitHub:
```bash
git remote add origin https://github.com/41092Anant/GitCommands.git
git branch -M main
git push -u origin main
```

Troubleshooting push:
- If using HTTPS and you see an authentication error, create a GitHub Personal Access Token (PAT) and use it as the password.
- To avoid entering credentials, enable the credential helper:
```bash
git config --global credential.helper manager-core   # Windows
```

5) (Optional) Set up SSH for easier auth:
```bash
ssh-keygen -t ed25519 -C "jain.anant555@gmail.com"
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519
# Copy ~/.ssh/id_ed25519.pub to GitHub (Settings -> SSH and GPG keys)
```

6) Verify on GitHub: open your repository in the browser and check files and commit history.

What I learned: small things like `.gitignore`, credential helpers, and closing IDEs when files are locked make the workflow smoother.
