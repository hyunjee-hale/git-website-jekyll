---
layout: post
title: "Using Git Across Multiple Devices"
date: 2026-06-05 08:00:00 -0500
categories: git workflow
---

If you work from both a laptop and a desktop — or at home and the office — Git handles this naturally. The remote repository on GitHub or GitLab is the **single source of truth**. Both machines sync through it.

## The golden rule

**Always run `git pull` before you start working.** Every time, on every machine. This brings in any changes you pushed from your other machine. Skipping this step is the number one cause of merge conflicts.

## The sync workflow

```
Machine A (Mac)                  Remote (GitHub)            Machine B (Windows)
     │                                │                              │
     ├── git pull ◀───────────────────┤                              │
     ├── make changes                 │                              │
     ├── git add / commit             │                              │
     ├── git push ───────────────────▶│                              │
     │                                ├◀── git pull ─────────────────┤
```

## Windows and Mac: fix line endings once

Mac uses `LF` line endings; Windows uses `CRLF`. Without the right setting, Git shows every line as changed even when nothing actually changed.

```bash
# On Windows
git config --global core.autocrlf true

# On Mac/Linux
git config --global core.autocrlf input
```

Run this once per machine and forget about it.

## Stop typing your password: SSH keys

Generate an SSH key on each machine and register the public key with GitHub or GitLab. Each machine gets its own key — never copy private keys between computers.

```bash
# 1. Generate a key (press Enter to accept all defaults)
ssh-keygen -t ed25519 -C "you@example.com"

# 2. Copy your public key
cat ~/.ssh/id_ed25519.pub

# 3. Paste it into GitHub: Settings → SSH and GPG Keys → New SSH Key

# 4. Test it
ssh -T git@github.com
```

## If you forgot to pull first

If you committed on Machine B without pulling Machine A's latest work, Git will tell you the branches have "diverged." The fix is straightforward:

```bash
git fetch       # see what's on the remote
git pull        # fetch + merge remote changes in
# resolve any conflicts if needed
git push
```
