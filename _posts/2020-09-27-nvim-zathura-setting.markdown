---
layout: post
title:  "NeoVim, Vimtex, and Zathura"
description: 
date:   2020-09-27 04:00:00
categories: 
---

I saw an interesting [post](https://castel.dev/post/lecture-notes-1/) by [Gilles Castel](https://castel.dev/) on writing Tex with Vim and thought it would be useful.

I decided to learn how to use them and see if they really improves my productivity.

#### Installation

First, I installed NeoVim via Home brew.

```
$brew install neovim
```

To enable python3 in Vim,

```
$pip3 install pynvim
```

You can check if python is active in vim by `:echo has(‘python3’)`, which should return 1. 

For Vim plugins manager, I installed Plug.

```
$sh -c 'curl -fLo "${XDG_DATA_HOME:-$HOME/.local/share}"/nvim/site/autoload/plug.vim --create-dirs \
       https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim'
```

Zathura can be installed by

```
$brew tap zegervdv/zathura

$brew install zathura
$brew install zathura-pdf-poppler

$mkdir -p $(brew --prefix zathura)/lib/zathura
```

#### Vim Configuration

Basic settings are from this [post](https://yufanlu.net/2018/09/03/neovim-python/).

```
" Turn off backup
set nobackup
set noswapfile
set nowritebackup
" Search configuration
set ignorecase                    " ignore case when searching
set smartcase                     " turn on smartcase
" Tab and Indent configuration
set expandtab
set tabstop=4
set shiftwidth=4
set smartindent
set tabstop=4
set shiftwidth=4
set expandtab
set autoindent
```

For fancy layout, I installed the following plugins.

```
Plug 'chriskempson/base16-vim'
Plug 'vim-airline/vim-airline'
Plug 'vim-airline/vim-airline-themes'

" Base16 -- color
let base16colorspace=256
colorscheme base16-phd
set background=dark

" True Color Support if it's avaiable in terminal
if has("termguicolors")
    set termguicolors
endif

" airline
let g:airline_left_sep  = ''
let g:airline_right_sep = ''
let g:airline#extensions#ale#enabled = 1
let airline#extensions#ale#error_symbol = 'E:'
let airline#extensions#ale#warning_symbol ='W:' 
```

[Base 16](https://github.com/chriskempson/base16) is for colorscheme. The list of schemes are avaialbe at [here](http://chriskempson.com/projects/base16/).

The reason why I got interested in writing tex with vim is Snippets and Zathura live preview. 

```
Plug 'lervag/vimtex'
Plug 'sirver/ultisnips'
Plug 'honza/vim-snippets' 
Plug 'xuhdev/vim-latex-live-preview', { 'for': 'tex' }
" live preview
let g:livepreview_previewer = 'zathura'
" vimtex
let g:tex_flavor='latex'
let g:vimtex_view_method='zathura'
let g:vimtex_quickfix_mode=0
" UltiSnips
let g:UltiSnipsExpandTrigger = '<tab>'
let g:UltiSnipsJumpForwardTrigger = '<s-tab>'
let g:UltiSnipsJumpBackwardTrigger = '<s-tab>'
augroup ultisnips_no_auto_expansion
    au!
    au VimEnter * au! UltiSnips_AutoTrigger
augroup END
```

For snippets, I first create a directory and snippets file for tex.

```
$mkdir ~/.config/nvim/UltiSnips
$nvim tex.snippets
```

At this moment, I just copied the snippets from [here](https://github.com/gillescastel/latex-snippets/blob/master/tex.snippets) with minor modification.

#### Zathura Configuration

```
# Zathura configuration file

# settings
set selection-clipboard clipboard
set adjust-open "width"
set window-height 1024
set window-width 768

# keys
map r reload
map p print
map i recolor
map J zoom out
map K zoom in
map R rotate
unmap f
map f toggle_fullscreen
map [fullscreen] f toggle_fullscreen

# One page per row by default
set pages-per-row 1

#stop at page boundries
set scroll-page-aware "true"
set scroll-full-overlap 0.01
set scroll-step 100
```

