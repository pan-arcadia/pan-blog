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

We want to wrap our color codes in starting and ending sequences of non-printing characters. 

```bash
`\[ColorCode\]`
```

Each color is formatted like this: 

```bash
\[\033[Color\]
```
We can reset the color to default: 

```bash
\[033[0m\]
```

| Special Character | Description |
| --- | --- |
| `\[` | Start sequence of non-printing characters |
| `\]` | End sequence of non-printing characters |
| `\t` | The current time in 24 hour HH:MM:SS format |
| `\j` | The number of jobs currently managed by the shell |
| `\h` | The hostname up to the first '.' |
| `\w` | The current working directory |
| `\n` | newline |
| `\$` | If the effective UID is 0, a #, otherwist a $ |


