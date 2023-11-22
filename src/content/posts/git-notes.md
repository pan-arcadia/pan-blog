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

Set username and email:

```shell
git config --global user.name "our name"
git config --global user.email "ourname@example.com"
```

Set the default `branch` name for our repositories:

```shell
git config --global init.defaultBranch main
```

Display our `config` settings:

```shell
git config --list
```

[Customizing git configuration](https://git-scm.com/book/en/v2/Customizing-Git-Git-Configuration)

## Initialize Git Repository

Create an empty git repository or reinitialize an existing one:

```bash
git init
```

This creates a `.git` directory and contains information about the repository.

## Remove a Git Repository

To remove a Git repository, we need to remove the `.git` folder from the directory:

```bash
rm -r .git
```

## Git remote

Show the remote url:

```shell
git remote -v
```



## Remove a remote

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
