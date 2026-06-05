---
layout: post
title: "Fork vs Clone: Which One Do You Need?"
date: 2026-06-05 08:00:00 -0500
categories: git basics
---

"Fork" and "clone" both create copies of a repository, but they're different operations that serve different purposes. Choosing the wrong one leads to a setup you have to undo.

## The short version

| | Clone | Fork |
|---|---|---|
| **What it is** | A local copy downloaded to your machine | Your own copy created on GitHub/GitLab (cloud) |
| **Where it lives** | Your computer | Your GitHub account (you then clone it locally) |
| **Use when** | You have write access to the repo | You don't have write access, or want your own independent copy |
| **Can you push?** | Yes, directly | Yes — to your fork. Then open a Pull Request to propose changes upstream. |

## When to clone (without forking)

- It's your own repo, setting up on a new machine
- You're an added collaborator with direct write access
- You just need a read-only local reference copy

```bash
git clone https://github.com/username/repo-name.git
```

## When to fork

- Contributing to an open-source project you don't own
- Working on an institutional repo without direct write access
- Making your own modified version you want to maintain independently

Click **Fork** on GitHub/GitLab first, then clone *your fork*:

```bash
git clone https://github.com/your-username/repo-name.git
```

## The fork workflow step by step

1. Click **Fork** on GitHub — this creates `github.com/your-username/repo-name`
2. Clone your fork locally: `git clone https://github.com/your-username/repo-name.git`
3. Add the original as "upstream": `git remote add upstream https://github.com/original-owner/repo-name.git`
4. Make changes on a branch, commit, push to your fork
5. Open a Pull Request to propose changes to the original

## Keeping your fork in sync

Over time the original repo gets updates your fork doesn't have:

```bash
git fetch upstream           # get updates from the original
git checkout main
git merge upstream/main      # bring them into your local main
git push origin main         # update your fork on GitHub
```

GitHub also has a **Sync fork** button on the repo page that does this in one click.
