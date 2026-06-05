---
layout: post
title: "Git Core Concepts: The Four Zones Explained"
date: 2026-06-05 08:00:00 -0500
categories: git basics
---

Before Git clicks, you need a mental model of where your files actually live at any given moment. There are four zones, and every Git command moves changes between them.

## The four zones

```
Working Directory  ──git add──▶  Staging Area  ──git commit──▶  Local Repo  ──git push──▶  Remote
  (your files)                   (what goes in                  (your history             (GitHub/GitLab)
                                  the next commit)               on this machine)
```

- **Working Directory** — the actual files on your computer. Changes here are invisible to Git until you explicitly tell it about them.
- **Staging Area (Index)** — a holding area where you decide what goes into the next commit. You can stage some files and leave others out.
- **Local Repository** — Git's history on your machine, stored in the hidden `.git` folder. Commits here are saved permanently but haven't been shared with anyone.
- **Remote** — the shared copy on GitHub or GitLab. This is what teammates see.

## The three states of a file

| State | What it means | How to move forward |
|---|---|---|
| **Modified** | You changed the file but haven't told Git | `git add <file>` |
| **Staged** | Marked to be included in the next commit | `git commit -m "message"` |
| **Committed** | Safely recorded in Git's history | `git push` to share |

## What is a commit?

A commit is a **snapshot of your entire project at a moment in time**. Each one records:

- A unique ID (a hash like `a3f1c9d`)
- Author name and email
- Timestamp
- A message explaining what changed and *why*
- A pointer to the commit before it — forming an unbroken chain of history

## Writing good commit messages

Your future self will thank you. Write messages that explain *why*, not just *what*:

```bash
# Too vague
git commit -m "changes"
git commit -m "fix"

# Good
git commit -m "Fix enrollment form to reject future birth dates"
git commit -m "Add .gitignore to exclude data export files"
```

A useful test: if your commit message needs the word "and," it could probably be two separate commits.
