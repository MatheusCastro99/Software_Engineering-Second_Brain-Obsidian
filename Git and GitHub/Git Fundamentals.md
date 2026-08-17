---
tags:
  - git
  - version-control
  - development
category: Git and GitHub
related: DRY Principle, Error Handling
---

# Git Fundamentals

Git is a distributed version control system that tracks changes to files, enables collaboration, and maintains project history.

## Core Workflow

### Three States of Files

```
Working Directory → Staging Area → Repository
   (Local)         (Index/Cache)      (History)
   Modified         Staged             Committed
```

- **Working Directory** - Your local files (modified but not tracked)
- **Staging Area** - Files marked for commit (via `git add`)
- **Repository** - Committed snapshots (.git folder)

## Basic Concepts

### Commit
- **Snapshot** of your project at a point in time
- Contains changes, author, timestamp, message
- Immutable once created (you can amend before push)

```bash
# Stage changes
git add file.txt

# Commit to repository
git commit -m "Add feature X"

# View commit history
git log
```

### Branch
- **Independent line of development** - Parallel work
- Isolates features from main code
- Default branch: `main` or `master`

```bash
# Create new branch
git branch feature-new-ui

# Switch to branch
git checkout feature-new-ui
# Or: git switch feature-new-ui (modern)

# Create and switch in one command
git checkout -b feature-auth

# List branches
git branch

# Delete branch
git branch -d feature-complete
```

### HEAD
- **Pointer** to the current branch/commit
- Tells Git where you are in history
- Moving HEAD = checking out different commit/branch

```bash
# See current HEAD
git log --oneline -1

# HEAD points to current branch
cat .git/HEAD  # Shows: ref: refs/heads/main

# Detached HEAD - at specific commit, not on branch
git checkout abc123def
```

## Common Workflow

### Basic Add and Commit

```bash
# 1. Make changes to files
# (Edit files in your editor)

# 2. Check status
git status
# Output: Shows modified files

# 3. Stage specific files
git add file1.cs file2.cs

# 4. Stage all changes
git add .

# 5. Commit
git commit -m "Description of changes"

# 6. Push to remote (if using remote repo)
git push origin main
```

### Viewing Changes

```bash
# See what changed (not staged)
git diff

# See what's staged for commit
git diff --staged

# View commit history
git log

# View specific file history
git log file.cs

# See change in specific commit
git show abc123def
```

## Branching Workflow

```bash
# Start new feature
git checkout -b feature/user-auth

# Make commits
git add .
git commit -m "Add login form"
git add .
git commit -m "Add password validation"

# Switch back to main
git checkout main

# Merge feature into main
git merge feature/user-auth

# Delete feature branch
git branch -d feature/user-auth
```

## Merging

### Fast-Forward Merge
- When feature branch is ahead of main
- Pointer simply moves forward

```
main: A -> B
feature:     C -> D

After merge:
main: A -> B -> C -> D
```

### Three-Way Merge
- When both branches have changes
- Creates merge commit combining both
- May have conflicts

```bash
# Merge with conflicts
git merge feature/changes
# Conflict! Edit files to resolve
git add .
git commit -m "Merge feature/changes"
```

## Useful Commands

```bash
# Undo changes in working directory
git checkout file.cs

# Unstage file
git reset HEAD file.cs

# Undo last commit (keep changes)
git reset --soft HEAD~1

# View who changed each line
git blame file.cs

# Search commit history
git log -S "search term"

# Create tag for release
git tag v1.0.0
```

## Best Practices

✓ **Commit often** - Small, logical commits
✓ **Write clear messages** - "Add login" vs "fix stuff"
✓ **Branch for features** - Keep main stable
✓ **Review before push** - `git diff` before committing
✓ **Pull before push** - Stay in sync
✗ **Don't force push** - Except when necessary
✗ **Commit secrets** - Use .gitignore
✗ **Large binary files** - Use Git LFS

## Related Concepts

- [[DRY Principle]] - Clean commits avoid duplication
- [[Error Handling]] - Meaningful commit messages help debugging