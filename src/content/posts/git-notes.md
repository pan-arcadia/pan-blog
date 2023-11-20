---
title: 'Git Cheat Sheet'
pubDate: 2023-11-19 10:00:00.0 -7
description: 'Git cheat sheet.'
author: 'JH'
tags: ['git']
---

## How to install git on Ubuntu

Update our packages:

```shell
sudo apt-get update
```

Install git on our machine:

```shell
sudo apt-get install git-all
```

Verify our installation:

```shell
git version
```

[Official git site - installing on Linux](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)


## Verify git version

```bash
git version
```

## Configure git on our machine

```bash
# Set user name.
git config --global user.name "our name"

# Set user email.
git config --global user.email "oursite@example.com"

# Show config settings.
git config --list

# Set default branch name
# This sets the default branch name for all repos created.
# Common names are trunk, main, development.
git config --global init.defaultBranch main
```

## Initialize Git Repository

```bash
git init
```

## Remote verbose

```shell
git remote -v
```

## Remove a Git Repository

```bash
# Just remove the .git directory.
rm -r .git
```

## Remove a Git Remote URL

```shell
git remote rm <remote-name>
git remote remove <remote-name>
```

## Git Status

```bash
git status
git status --short
```

Short status flags:
- ?? - Untracked files
- A - Files added to stage
- M - Modified files
- D - Deleted files

## Staging Files

```bash
# Stage a file by name.
git add <filename>

# Stage multiple files.
git add --all

# Stage multiple files shorthand.
git add .
```

## Commiting Files

```bash
git commit -m "message"

# Stage all changed and tracked files.
git commit -a -m "message"
```

## Git Log

```bash
git log

# Show one line per commit.
git log --oneline
```

**Note**: If there is a long list view in the terminal, `shift + G` to jump to the end of the list, then `q` to exit the list.

## Git Branch

```bash
# Create a new branch.
git branch branch_name

# Checkout a branch.
git checkout branch_name

# Create a new branch and move to it immediately.
git checkout -b branch_name

# List all branches in repository.
git branch

# Merge branches.
git merge branch_name

# Delete a branch
git branch -d branch_name

# Force delete a branch.
git branch -D branch_name

# Change branch name.
git branch -M branch_name
```
