---
title: 'Vim Adding Plugins'
pubDate: 2023-12-16 10:00:00.0 -7
description: 'How to add plugins to Vim'
author: 'JH'
tags: ['vim']
---

We can extend Vim's functionality by using plugins. The best way to implement this is by using a Vim plugin manager.

Here, we will use [vim-plug](https://github.com/junegunn/vim-plug) plugin manager.

## Installation

```shell
curl -fLo ~/.vim/autoload/plug.vim --create-dirs https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim
```

## Installing plugins using `vim-plug`

We install plugins by editin our `~/.vimrc` file:

```vim
call plug#begin()

Plug 'preservevim/nerdtree'

call plug#end()
```

## Reference

[How to Extend Vim's Functionality by Adding Plugins](https://linuxhandbook.com/install-vim-plugins/)
