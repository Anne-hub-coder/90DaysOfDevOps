# Day 22 – Introduction to Git: My First Repository

## Objective

Today I started my Git journey by creating my first Git repository on an Ubuntu EC2 instance. I learned how Git tracks files, uses a staging area, stores history inside the `.git` folder, and builds a clean commit history through multiple commits.

---

## Environment

- Platform: AWS EC2
- Operating System: Ubuntu 26.04 LTS
- Git Version: 2.53.0

---

# Task 1 – Install & Configure Git

I verified Git was installed and configured my global identity.

## Commands

```bash
git --version

git config --global user.name "ANUSHKA"

git config --global user.email "anushka.ag10@gmail.com"

git config --global --list
```

## Output

```text
git version 2.53.0

user.name=ANUSHKA
user.email=anushka.ag10@gmail.com
```

## What I Learned

- Git must know my name and email before creating commits.
- Global configuration applies to all repositories.
- `git config --global --list` verifies my settings.

---

# Task 2 – Create My First Git Repository

I created a practice repository and explored the hidden Git directory.

## Commands

```bash
mkdir -p ~/devops-git-practice

cd ~/devops-git-practice

git init

git status

ls -la

ls -la .git
```

## Output

Git initialized successfully.

Repository contained:

```text
.git
git-commands.md
tatus
```

Inside `.git` I found folders like:

- `objects`
- `refs`
- `logs`
- `hooks`
- `info`

along with configuration files such as `HEAD`, `config`, and `index`.

## What I Learned

- `.git` stores the complete repository history.
- `git init` creates the hidden Git database.
- `git status` explains exactly what Git is tracking.

---

# Task 3 – Create My Git Commands Reference

I created a personal reference file called `git-commands.md`.

The file contains categories for:

- Setup & Configuration
- Basic Workflow
- Viewing Changes
- Additional useful commands like `git diff`, `git restore`, and `git log --oneline`.

## Commands Used

```bash
nano git-commands.md
```

## What I Learned

- Writing my own command reference makes revision easier.
- Git documentation grows over time as I learn new commands.
- Markdown is perfect for maintaining technical notes.

---

# Task 4 – First Commit

I staged my first file and created my first Git commit.

## Commands

```bash
git add git-commands.md

git status

git commit -m "Initial Git commands reference"

git log
```

## Output

```text
[master 502d024] Initial Git commands reference
```

`git log` showed:

- Commit ID
- Author
- Date
- Commit message

## What I Learned

- `git add` stages changes.
- `git commit` permanently records a snapshot.
- Every commit receives a unique hash.

---

# Task 5 – Build Commit History

Instead of making one large commit, I created multiple meaningful commits.

## Second Commit

Added `git diff`.

```bash
git diff
git status
git add git-commands.md
git commit -m "Add git diff command"
```

Commit:

```text
d6fe4ab Add git diff command
```

---

## Third Commit

Added `git restore`.

```bash
git add git-commands.md
git commit -m "Add git restore command"
```

Commit:

```text
436a4d9 Add git restore command
```

---

## Fourth Commit

Expanded my Git history reference.

```bash
git add git-commands.md
git commit -m "Expand Git history reference"
```

Commit:

```text
dc04cfe Expand Git history reference
```

## What I Learned

- Small commits make history easier to understand.
- Every update should have a meaningful commit message.
- `git diff` shows changes before committing.

---

# Task 6 – Git Workflow Notes

I created `day-22-notes.md` containing answers about Git concepts.

## Commands

```bash
nano day-22-notes.md

git add day-22-notes.md

git commit -m "Add Day 22 Git notes"
```

Commit:

```text
afb6409 Add Day 22 Git notes
```

## My Answers

### Difference between `git add` and `git commit`

- `git add` moves changes into the staging area.
- `git commit` permanently saves staged changes into Git history.

### What is the staging area?

The staging area lets me review exactly what will be included before creating a commit.

### What does `git log` show?

It displays commit history including:

- Commit ID
- Author
- Date
- Commit message

### What is the `.git` folder?

The `.git` folder stores the complete repository history, branches, commits, and configuration. Deleting it removes Git tracking.

### Working Directory vs Staging Area vs Repository

| Area | Purpose |
|------|---------|
| Working Directory | Where I edit files |
| Staging Area | Temporary area before committing |
| Repository | Permanent Git history |

---

# Final Commit History

Running:

```bash
git log --oneline
```

produced:

```text
afb6409 Add Day 22 Git notes
dc04cfe Expand Git history reference
436a4d9 Add git restore command
d6fe4ab Add git diff command
502d024 Initial Git commands reference
ef291ae Initial Git commands reference
```

The duplicate initial commit appeared because I reinitialized and recommitted while practicing Git, which helped me understand how Git records each commit separately.

---

# Commands Used

```bash
git --version

git config --global user.name "ANUSHKA"
git config --global user.email "anushka.ag10@gmail.com"
git config --global --list

mkdir -p ~/devops-git-practice
cd ~/devops-git-practice

git init
git status

ls -la
ls -la .git

nano git-commands.md

git add git-commands.md
git commit -m "Initial Git commands reference"

git diff
git status

git commit -m "Add git diff command"
git commit -m "Add git restore command"
git commit -m "Expand Git history reference"

nano day-22-notes.md

git add day-22-notes.md
git commit -m "Add Day 22 Git notes"

git log
git log --oneline
```

---

# What I Learned

- Git tracks project history through commits.
- The staging area gives control over what gets committed.
- `git status` is the most useful command for checking repository state.
- The `.git` folder contains Git's internal database.
- Frequent, meaningful commits create a cleaner project history.

---

# DevOps Takeaway

Git is one of the most important tools in DevOps because every infrastructure change, automation script, and CI/CD pipeline is version-controlled. Learning to stage changes, create meaningful commits, and read commit history builds the foundation for collaborative software development.

---

# Evidence

Capture these screenshots for GitHub:

- `git-config.png`
- `git-init.png`
- `git-folder.png`
- `first-commit.png`
- `git-log-oneline.png`
- `final-git-history.png`
- `repo-files.png`

---

# Day 22 Summary

Today I created my first Git repository, configured Git, explored the `.git` directory, built a personal Git commands reference, created multiple commits, and learned how the working directory, staging area, and repository work together. This marks the beginning of my version control journey, which is essential for modern DevOps workflows.
