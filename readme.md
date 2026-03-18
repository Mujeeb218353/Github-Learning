# 🚀 Git & GitHub — The Complete Cheat Sheet

---

## 🎯 Starting Your Journey

### Initialize a Repository
> Turn any folder into a Git-tracked project
````bash
git init
````

---

## 📋 Staying Informed

### Check File Status
> See what's changed, staged, or untracked
````bash
git status
````

### View Commit History
> See a log of all past commits
````bash
git log --oneline
````

---

## ➕ Staging Changes

### Add All Files
> Stage everything in the current folder
````bash
git add .
````

### Add a Specific File
> Stage only what you choose
````bash
git add filename.txt
````

### Unstage a File
> Oops, — remove a file from staging
````bash
git restore --staged filename.txt
````

---

## 💾 Saving Your Work

### Commit Changes
> Snapshot your staged files with a message
````bash
git commit -m "your message here"
````

### Amend Last Commit
> Fix a typo in your last commit message
````bash
git commit --amend -m "corrected message"
````

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

### 📋 List All Branches
```bash
# Local branches
git branch

# Local + remote branches
git branch -a
```

### 🚀 Push Local Branch to Remote
> Publish your local branch to GitHub for the first time
```bash
git push -u origin branch-name
```

### 🔍 Check Tracking Connection
> See which local branches are connected to which remote branches
```bash
git branch -vv
```

---

### 📡 Set Upstream for Existing Branch
> Already pushed but forgot `-u`? Link them manually
```bash
git branch --set-upstream-to=origin/branch-name branch-name
```

### ⬇️ Pull a Remote Branch Locally
> Someone else created a branch on GitHub — grab it locally
```bash
# Fetch all remote branches first
git fetch origin

# Then switch to it (Git auto-tracks it)
git switch branch-name
```

## ☁️ Remote & GitHub

### Connect to GitHub
````bash
git remote add origin https://github.com/username/repo.git
````

### Push to GitHub
````bash
git push -u origin main
````

### Pull Latest Changes
````bash
git pull origin main
````

### Clone a Repository
````bash
git clone https://github.com/username/repo.git
````

---

## 🧙 Pro Tips

| Command                 | What it does                        |
|-------------------------|-------------------------------------|
| `git diff`              | See unstaged changes                |
| `git stash`             | Save work without committing        |
| `git stash pop`         | Bring stashed work back             |
| `git reset --hard HEAD` | Undo everything back to last commit |
---

> 💡 **Golden rule:** Commit early, commit often. Every commit is a save point you can return to.