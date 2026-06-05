---
layout: post
title: "Repository Maintenance: Keeping Your Repo Healthy"
date: 2026-06-05 08:00:00 -0500
categories: git workflow
---

A little discipline with day-to-day Git habits prevents the kind of messy repo state that takes a long time to untangle. These are the practices worth building into your routine.

## Commit early, commit often

Small, focused commits are easier to understand and reverse than large dumps of mixed changes. If your commit message uses the word "and," it could probably be two commits.

## Keep main clean

Treat `main` like a production branch — it should always be in a working state. Do all experimental or in-progress work on a branch, and only merge into `main` when it's ready.

## Routine health-check commands

```bash
# What's the current state of my working directory?
git status

# What exactly changed in my files?
git diff

# See compact commit history
git log --oneline

# Check remote changes without touching your files
git fetch

# Remove stale remote-tracking references
git remote prune origin
```

## Shelving work temporarily with git stash

Need to switch tasks before you're ready to commit? `git stash` saves your changes without creating a commit:

```bash
git stash         # save uncommitted changes
git pull          # get latest from remote
git stash pop     # restore your saved changes
```

You can have multiple stashes. See them with `git stash list` and restore a specific one with `git stash pop stash@{1}`.

## Good .gitignore patterns

Add these before your first commit to avoid accidentally tracking files you shouldn't:

```
.env
*.log
*.csv
*.xlsx
*_export.*
*.bak
.DS_Store
Thumbs.db
node_modules/
```

The important rule: **create `.gitignore` before your first commit**. Files already tracked by Git are not automatically ignored when added to `.gitignore` later. If you committed something you shouldn't have, see the post on removing sensitive data.

## Checking whether you're in sync with remote

```bash
git fetch

# Then check status — Git will tell you clearly:
git status
# "Your branch is behind 'origin/main' by 3 commits"
# "Your branch is ahead of 'origin/main' by 2 commits"
# "Your branch and 'origin/main' have diverged"
```
