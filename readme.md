# 🚀 Git & GitHub — The Complete Cheat Sheet

---

## 🎯 Starting Your Journey

### Initialize a Repository
> Turn any folder into a Git-tracked project
```bash
git init
```

---

## 📋 Staying Informed

### Check File Status
> See what's changed, staged, or untracked
```bash
git status
```

### View Commit History
> See a log of all past commits
```bash
git log --oneline
```

---

## ➕ Staging Changes

### Add All Files
> Stage everything in the current folder
```bash
git add .
```

### Add a Specific File
> Stage only what you choose
```bash
git add filename.txt
```

### Unstage a File
> Oops — remove a file from staging
```bash
git restore --staged filename.txt
```

---

## 💾 Saving Your Work

### Commit Changes
> Snapshot your staged files with a message
```bash
git commit -m "your message here"
```

### Amend Last Commit
> Fix a typo in your last commit message
```bash
git commit --amend -m "corrected message"
```

---

## ⏪ Reset — Undoing Commits

All three modes move HEAD back to a commit. The difference is what happens to your files and staged changes.

### --soft
> Undoes the commit. Changes stay **staged**, ready to re-commit.
```bash
git reset --soft HEAD~1
```
- ✅ Commit gone
- ✅ Changes still staged
- ✅ Files untouched

### --mixed (default)
> Undoes the commit and **unstages** changes. Files are untouched.
```bash
git reset HEAD~1
# same as:
git reset --mixed HEAD~1
```
- ✅ Commit gone
- ⚠️ Changes unstaged
- ✅ Files untouched

### --hard
> Wipes the commit **and all changes**. Cannot be undone easily.
```bash
git reset --hard HEAD~1
```
- ✅ Commit gone
- ❌ Staged changes lost
- ❌ File changes wiped

### Quick Reference

| Flag | Commit | Staging area | Working files |
|------|--------|--------------|---------------|
| `--soft` | removed | kept staged | untouched |
| `--mixed` | removed | cleared | untouched |
| `--hard` | removed | cleared | wiped |

> 💡 Use `HEAD~2` to go back 2 commits, `HEAD~3` for 3, etc. Or pass a commit hash: `git reset --soft abc1234`

---

## 🔀 Merge — Combining Branches

### Basic Merge
> Switch to the branch you want to merge **into**, then merge
```bash
git switch main
git merge feature-name
```

### Merge Strategies

#### Fast-forward merge (default when possible)
> No new commit created — Git simply moves the pointer forward
```bash
git merge feature-name
```
```
Before:  main → A → B
                      feature → C → D

After:   main → A → B → C → D
```

#### No fast-forward (always create a merge commit)
> Preserves branch history even if fast-forward is possible
```bash
git merge --no-ff feature-name
```
```
After:   main → A → B ──────────── M
                      feature → C → D ↗
```

#### Squash merge
> Squashes all commits from the branch into one staged change — you then commit it yourself
```bash
git merge --squash feature-name
git commit -m "add feature-name"
```
- ✅ Clean history on main
- ✅ All feature changes in one commit
- ⚠️ Branch history is not preserved

### Abort a Merge
> Stuck in a conflict? Cancel and go back to where you were
```bash
git merge --abort
```

### Resolving Merge Conflicts
> When Git can't auto-merge, it marks conflicts in the file
```bash
# Step 1 — open the conflicted file, you'll see:
<<<<<<< HEAD
your changes
=======
their changes
>>>>>>> feature-name

# Step 2 — edit the file to keep what you want, then:
git add filename.txt
git commit -m "resolve merge conflict"
```

### Check Differences Before Merging
```bash
git diff main..feature-name
```

### Merge vs Rebase

| | `merge` | `rebase` |
|---|---|---|
| History | preserves all commits | rewrites as linear |
| Safety | safe on shared branches | risky on shared branches |
| Use when | merging into main | cleaning up local feature branch |

```bash
# Rebase your feature branch onto main
git switch feature-name
git rebase main
```

---

## 📦 Stash — Save Work Without Committing

### Basic Stash
> Temporarily shelve uncommitted changes so you can switch tasks
```bash
git stash
```

### Stash with a Name
> Give it a label so you remember what it contains
```bash
git stash save "work in progress: login form"
```

### View All Stashes
```bash
git stash list
# Output:
# stash@{0}: On main: work in progress: login form
# stash@{1}: WIP on feature: abc1234 some commit
```

### Apply a Stash
```bash
# Apply the most recent stash (keeps it in the list)
git stash apply

# Apply a specific stash
git stash apply stash@{2}
```

### Pop a Stash
> Apply and remove from the stash list in one step
```bash
# Pop the most recent stash
git stash pop

# Pop a specific stash
git stash pop stash@{1}
```

### Stash Including Untracked Files
> By default, stash ignores new untracked files — use `-u` to include them
```bash
git stash -u
# or
git stash --include-untracked
```

### Stash a Specific File
```bash
git stash push -m "only stashing this file" filename.txt
```

### View What's Inside a Stash
```bash
git stash show stash@{0}         # summary
git stash show -p stash@{0}      # full diff
```

### Create a Branch from a Stash
> Useful when your stashed changes conflict with the current branch
```bash
git stash branch new-branch-name stash@{0}
```

### Drop a Stash
```bash
# Remove a specific stash
git stash drop stash@{1}

# Clear all stashes
git stash clear
```

### Stash Quick Reference

| Command | What it does |
|---------|--------------|
| `git stash` | Stash all tracked changes |
| `git stash -u` | Stash including untracked files |
| `git stash list` | See all stashes |
| `git stash pop` | Apply latest + remove from list |
| `git stash apply` | Apply latest + keep in list |
| `git stash drop stash@{n}` | Delete a specific stash |
| `git stash clear` | Delete all stashes |

---

## 🌿 Working with Branches

### Create a New Branch
```bash
git branch feature-name
```

### Switch to a Branch
```bash
# Old way
git checkout feature-name

# ✅ Modern way (Git 2.23+)
git switch feature-name
```

### Create + Switch in One Step
```bash
# Old way
git checkout -b feature-name

# ✅ Modern way
git switch -c feature-name
```

### Create a Branch from Another Branch (without switching)
> Stay on your current branch while creating a new one from a specific branch
```bash
git branch new-branch source-branch
```

### Merge a Branch
```bash
git merge feature-name
```

### Delete a Branch
```bash
git branch -d feature-name
```

### List All Branches
```bash
# Local branches
git branch

# Local + remote branches
git branch -a
```

### Push Local Branch to Remote
> Publish your local branch to GitHub for the first time
```bash
git push -u origin branch-name
```

### Check Tracking Connection
> See which local branches are connected to which remote branches
```bash
git branch -vv
```

### Set Upstream for Existing Branch
> Already pushed but forgot `-u`? Link them manually
```bash
git branch --set-upstream-to=origin/branch-name branch-name
```

### Pull a Remote Branch Locally
> Someone else created a branch on GitHub — grab it locally
```bash
# Fetch all remote branches first
git fetch origin

# Then switch to it (Git auto-tracks it)
git switch branch-name
```

---

## ☁️ Remote & GitHub

### Connect to GitHub
```bash
git remote add origin https://github.com/username/repo.git
```

### Push to GitHub
```bash
git push -u origin main
```

### Sync After a Reset (diverged history)
```bash
# Safe — checks no one else pushed first
git push --force-with-lease origin branch-name

# On shared branches, prefer revert instead
git revert HEAD~2..HEAD
git push origin main
```

### Pull Latest Changes
```bash
git pull origin main
```

### Clone a Repository
```bash
git clone https://github.com/username/repo.git
```

---

## 🧙 Pro Tips

| Command | What it does |
|---------|--------------|
| `git diff` | See unstaged changes |
| `git stash` | Save work without committing |
| `git stash pop` | Bring stashed work back |
| `git reset --hard HEAD` | Undo everything back to last commit |
| `git revert <hash>` | Safely undo a pushed commit |
| `git log --oneline --graph` | Visual branch history |
| `git cherry-pick <hash>` | Apply a single commit to current branch |

---

> 💡 **Golden rule:** Commit early, commit often. Every commit is a save point you can return to.