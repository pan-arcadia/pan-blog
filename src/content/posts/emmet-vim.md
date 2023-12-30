---
title: 'How to set up emmet-vim' 
pubDate: 2023-12-21 10:00:00.0 -7
description: 'Setting up emmet-vim'
author: 'JH'
tags: ['vim', 'emmet']
---



## Add to `.vimrc`

```vim
let g:user_emmet_install_global = 0
autocmd FileType html,css EmmetInst
let g:user_emmet_leader_key=’,’
```

## Reference

[emmet-vim](https://github.com/mattn/emmet-vim)

[vim for web development](https://medium.com/@felipe.anjos/vim-for-web-development-html-css-in-2020-95576d9b21ad)


