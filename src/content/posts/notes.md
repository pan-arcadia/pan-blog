---
title: 'Notes'
pubDate: 2023-12-12 10:00:00.0 -7
description: 'My daily notes.'
author: 'JH'
tags: ['notes', 'linux']
---

## How to install Visual Studio Code as a Snap Package

We can install vscode from either the command line or the Ubuntu Software application.

Installation using the command line:

```shell
sudo snap install --classic code
```

## Things to do after installing Ubuntu 20.04

Here is a quick reminder list of things to do after installing Ubuntu 20.04.

## Get our system updated

Update *snap* packages:

```shell
sudo snap refresh
```

Update our *apt* packages:

```shell
sudo apt update && sudo apt upgrade
```

## Automatic Suspend and Screenlock for Laptops

Open *settings => power* .

We can turn off **Screen Blank**, set it to *Never*. Remember to lock the laptop with `Super + L` when we walk away.

We can turn off **Automatic Suspend**.

## Utilize the *nightlight* feature. Softens the screen brightness.

Open *Settings => Displays*. Tap the *Night Light* tab.

## Clean our system

We can remove packages that are not needed anymore:

```shell
sudp apt autoremove
```

## Install GNOME Tweaks

It can be installed using Ubuntu Software.
