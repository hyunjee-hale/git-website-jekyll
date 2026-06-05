---
layout: post
title: "Git Basics: The Commands You'll Use Every Day"
date: 2026-06-05 09:00:00 -0500
categories: git basics
---

If you only memorize a handful of Git commands, make it these. They cover the vast majority of day-to-day work.

## The core loop

```bash
git status          # see what's changed
git add <file>      # stage a file
git commit -m "..."  # commit with a message
git push            # push to remote
```

`git status` is the one command worth running constantly — before staging, after staging, before pushing. It tells you exactly where you are.

## Checking history

```bash
git log --oneline        # compact commit list
git log --oneline --graph  # shows branch/merge structure
git diff                 # unstaged changes
git diff --staged        # staged changes (what will be committed)
```

## Undoing things

```bash
git restore <file>        # discard unstaged changes to a file
git restore --staged <file>  # unstage a file (keep the changes)
git revert <commit-hash>  # create a new commit that undoes a past commit
```

Prefer `git revert` over `git reset --hard` when working on a shared branch — it's non-destructive and leaves a clear history trail.

## Branching

```bash
git branch feature/my-thing   # create a branch
git switch feature/my-thing   # switch to it
git switch -c feature/my-thing  # create and switch in one step
git merge feature/my-thing    # merge into current branch
```

`git switch` is the modern replacement for `git checkout` for branch operations — clearer intent, less ambiguity.
