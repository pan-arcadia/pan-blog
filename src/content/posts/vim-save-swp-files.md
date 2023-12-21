---
title: 'Vim: Saving swap, backup, and undo files'
pubDate: 2023-12-21 10:00:00.0 -7
description: 'How to get vim swap, backup, and undo files out of our working directory.'
author: 'JH'
tags: ['vim', 'linux']
---

I noticed that vim was saving `swp` files in my working directory. And `git` was tracking them. 

We can have vim store these files in a central directory. Add the following code to our `.vimrc` file:

```vim
set backupdir=.backup/,~/.backup/,/tmp//
set directory=.swp/,~/.swp/,/tmp//
set undodir=.undo/,~/.undo/,/tmp//
```

## Reference

[Vim Documentation: recover](https://vimdoc.sourceforge.net/htmldoc/recover.html#swap-file)

[Vim: Remove swap, backup and undo Files from Working Directory](https://medium.com/@Aenon/vim-swap-backup-undo-git-2bf353caa02f)


