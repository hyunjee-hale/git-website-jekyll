---
layout: post
title: "Branching Strategies: When to Use What"
date: 2026-06-05 09:00:00 -0500
categories: git workflow
---

Choosing a branching strategy early saves a lot of cleanup later. Here are the three most common approaches and when each makes sense.

## Feature branches (most common)

The simplest model: `main` is always deployable, and all work happens on short-lived feature branches.

```
main
 └── feature/add-login
 └── feature/fix-header-bug
 └── feature/update-docs
```

Each branch merges into `main` via a pull request. Works well for small to medium teams where everyone is working on independent pieces.

**Good for:** most projects, teams of 2–10, continuous deployment workflows.

## Git Flow

A more structured model with two long-lived branches (`main` and `develop`) plus supporting branches for features, releases, and hotfixes.

```
main ────────────────────── (production releases only)
develop ─────────────────── (integration branch)
 └── feature/xyz
 └── release/1.2.0
 └── hotfix/critical-bug
```

**Good for:** projects with scheduled releases, larger teams, versioned software.

**Downside:** overhead is real — PRs go through more steps and the branch graph gets complex fast.

## Trunk-based development

Everyone commits directly to `main` (or merges very short-lived branches within a day). Relies heavily on feature flags to hide incomplete work.

**Good for:** teams with strong CI/CD, high deployment frequency, experienced engineers.

## Which one to pick

If you're starting a new project and unsure: use feature branches. It's simple, it works, and you can always add structure later. Git Flow is often chosen before teams realize the overhead isn't worth it for their size.
