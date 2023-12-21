pubDate: 2023-12-12 10:00:00.0 -7
description: 'Using the system clipboard in Vim.'
author: 'JH'
tags: ['vim', 'linux', 'clipboard']
---

## How to use Vim with the system clipboard

The version of vim that came with Ubuntu 22.04 did not have access to the system clipboard.

We can see if Vim has system clipboard support by running the following command:

```shell
vim --version | grep clipboard
```

If we see `+clipboard` or `+xterm_clipboard`, then system clipboard support is enabled.

If not we can install `vim-gtk`:

```shell
sudp apt install vim-gtk3
```

Note: I've seen `vim-gtk` and `vim-gtk3`. Not sure what the difference is. I installed `vim-gtk3` and it had the system clipboard enabled.

Now that we have the system clipboard enabled, we can paste some text. Put Vim into INSERT mode. Paste from the clipboard with `Shift+Insert` or `Ctrl+Shift+V`.

### Reference

[How do I install vim-gnome on Ubuntu 19.10?](https://askubuntu.com/questions/1208159/how-do-i-install-vim-gnome-on-ubuntu-19-10) 

[How to Paste Clipboard Text in Vim](https://codingissimple.com/how-to-paste-clipboard-text-in-vim/)

