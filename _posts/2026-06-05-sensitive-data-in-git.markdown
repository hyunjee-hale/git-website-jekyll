---
layout: post
title: "Sensitive Data in Git: Prevention and Recovery"
date: 2026-06-05 08:00:00 -0500
categories: git security
---

Accidentally committing a password, API key, or sensitive file to a repository is a common mistake with serious consequences. Here's how to prevent it and what to do if it happens.

## Prevention (always easier than recovery)

- Create `.gitignore` **before your first commit** and include `.env`, credential files, data exports, and backup files
- Use `git add <specific-file>` instead of `git add .` — it forces you to think about what you're staging
- Run `git status` before every commit and look at what's staged
- Store secrets in `.env` files locally and never commit them

Common patterns to add to `.gitignore`:

```
.env
*.pem
*password*
*credential*
*_export.*
secrets.txt
config/local_*.php
```

## If it happens: act immediately

If sensitive data was pushed to a remote repository, **assume it was seen** — even if only for a few minutes. GitHub, forks, pull request history, and CI logs can all cache content.

**First step regardless of scenario: revoke and rotate the exposed credential.** Don't wait until you've cleaned the repo.

## Scenario A: Committed but not yet pushed

This is the easy case — it only exists on your machine:

```bash
# Undo the last commit, but keep the file contents
git reset --soft HEAD~1

# Add the sensitive file to .gitignore
echo "secrets.txt" >> .gitignore

# Unstage the sensitive file
git restore --staged secrets.txt

# Commit just the .gitignore change
git add .gitignore
git commit -m "Add secrets.txt to .gitignore"
```

## Scenario B: Already pushed to a remote

Use **BFG Repo Cleaner** — it's faster and safer than the built-in `git filter-branch`:

1. **Revoke any exposed credentials first** (don't wait)
2. Download BFG from [rtyley.github.io/bfg-repo-cleaner](https://rtyley.github.io/bfg-repo-cleaner/) — requires Java
3. Clone a fresh mirror: `git clone --mirror https://github.com/user/repo.git`
4. Remove the file from all history: `java -jar bfg.jar --delete-files secrets.txt repo.git`
5. Prune and clean: `cd repo.git && git reflog expire --expire=now --all && git gc --prune=now --aggressive`
6. Force push: `git push --force`
7. Notify all collaborators — they must re-clone, as their local copies still contain the old history
8. Contact GitHub support to purge server-side caches

Alternatively, `git filter-repo` is a modern built-in option (install via pip):

```bash
git filter-repo --path secrets.txt --invert-paths
git push --force
```

## The key takeaway

A `.gitignore` created before the first commit prevents almost all of these scenarios. The cost of setting it up is five minutes. The cost of cleaning up a pushed secret — and rotating all affected credentials — is much higher.
