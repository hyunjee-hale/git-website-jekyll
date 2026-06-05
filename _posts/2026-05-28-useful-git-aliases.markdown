---
layout: post
title: "Git Aliases Worth Setting Up"
date: 2026-06-05 09:00:00 -0500
categories: git productivity
---

Git aliases let you shorten commands you type dozens of times a day. Add these to your `~/.gitconfig` under `[alias]` and you'll wonder how you lived without them.

## The essentials

```ini
[alias]
  st   = status
  co   = switch
  br   = branch
  last = log -1 HEAD
  lg   = log --oneline --graph --decorate --all
  undo = restore --staged
```

After adding these:

```bash
git st           # same as git status
git co main      # same as git switch main
git lg           # compact visual commit graph
git undo <file>  # unstage a file
```

## A few more useful ones

```ini
  # Show which files changed in the last commit
  changed = diff --name-only HEAD~1 HEAD

  # Amend the last commit without changing the message
  amend = commit --amend --no-edit

  # Clean up merged local branches
  cleanup = "!git branch --merged | grep -v '\\*\\|main\\|master' | xargs -n 1 git branch -d"
```

## Adding aliases from the command line

You don't have to edit `~/.gitconfig` by hand — you can set aliases directly:

```bash
git config --global alias.st status
git config --global alias.lg "log --oneline --graph --decorate --all"
```

## Viewing your current aliases

```bash
git config --global --list | grep alias
```

Start with `st`, `co`, and `lg` — those three alone save a noticeable amount of typing.
