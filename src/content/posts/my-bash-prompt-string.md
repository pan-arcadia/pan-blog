---
title: 'My Bash Prompt String'
pubDate: 2024-01-27 10:00:00.0 -7
description: 'My current bash prompt string.'
author: 'JH'
tags: ['bash', 'prompt']
---

Paste the following `PS1` string into our `.bashrc` file:

```bash
PS1='\[\033[38;5;10m\][\t]-[\[\033[38;5;9m\j\[\033[38;5;10m\]]-[\h:\[\033[38;5;14m\]\w]\[\033[0m\] \n\$ '
```

We want to wrap the color codes in \[ \]. This tells the shell that everything between the escaped brackets are non-printing characters.

Breaking down the PS1 string:

```bash

\[\033[1;32m\] => Set the color to green.
`[\t] => The current time in 24 hour format HH:MM:SS.
-[ => Print a dash and open bracket.
\[\033[1;31m => Set the color to red.
\j => The number of jobs currently managed by the shell.
\[\033[1;32m => Set the color back to green.
]- => Close off the jobs section.
[\h: => Bracket the host name.
`[\033[1;36m] => Set the color to cyan.
\w] => Show the current working directory and close the bracket.
\[\033[0m => Reset the text color settings for the terminal.
\n => newline
\$ => Show $ on next line.
```
