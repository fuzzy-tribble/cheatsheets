# VIM - NSFBeginners

If you are holding a key down or pressing a key more than once...you could prob be doing something more efficiently!

## Navigation

### Nav - filewise

`gg` and `G` top, bottom of file 

### Nav - screenwise

`L`, `M`, `H` low, middle, high part of the file (ie bottom, mid, top)

`z.` move current like to center of screen

`zz`, `zt`  mv cursor to middle, top of screen

`C-e`, `C-y` scroll

`10%` scroll by percent

These are nice too but only if you usee a smooth scroll plugin - otherwise hard to follow
`C-d`, `C-u`  jump down and up half screen at a time
`C-f`, `C-b` full screen scrolling

### Nav - linewise

`^` or `$` beginning, end of line
*Note: you can also use `0` to get to beg of line*

`e` or `E`, `b` or `B`, `w` or `W` increment/decrement by word

*Note: can also use `ge` backwards to the ends of words*

`f`, `t` find char or till char (eg. `df.` delete find period or del up to pd)
 *Note: then you can hit dot to do it again* 

`x` backwards delete

*Plugin Note: Relative Number: can help you nav really efficienty (eg. `d7j` del 7 lines down)*

:-16,-14co.

## Setting Marks

`m<register>` (eg mm) backtick m; 

## Marcos

`qq` start a macro
`@q` rerun

## Search/Find/Replace

`*` search for the word you are currently on
`#` same as astrik but previous

turn highlight search on

`/apricot` finds apricot (then hit `n` to find the next occurance)

## Editing (Copy/Paste/Delete)

`-5,-10co.` Copy lines -5 to -10 and put in current cursor location

Visual mode highlight, `y` then `p` where you want

Plugin Note: ctags

`:tag create_` -> then hit tab a few times (note: create is what you are searching for)

`Ctrl]` Jump to something that your cursor is on

`Ctrl t` to go back up the tag stack

## Folding (using Plugin SimplyFold & FastFold)

za : Toggle code folding at the current line 
zo : Open fold.
zc : Close fold.
zR : Open all folds
zM : close all folds.
zM : Close all folds.

# TODOs

"cmd" t -> fuzzy finder

surround.vim hange surrounding

ctags

Vundle Plugins

Indentwise
[- : Move to previous line of lesser indent than the current line.
[+ : Move to previous line of greater indent than the current line.
[= : Move to previous line of same indent as the current line that is separated from the current line by lines of different indents.
]- : Move to next line of lesser indent than the current line.
]+ : Move to next line of greater indent than the current line.
]= : Move to next line of same indent as the current line that is separated from the current line by lines of different indents..



### POWERLINES

### SURROUND

installed using native vim 8 package mngr

tpope

cs'" replace single with double
ds" remove quotes around a word that already has "them"
cst" to put quote

yss


### NERDTREE

:help NERDTrees

t: Open the selected file in a new tab
i: Open the selected file in a horizontal split window
s: Open the selected file in a vertical split window
I: Toggle hidden files
m: Show the NERD Tree menu
R: Refresh the tree, useful if files change outside of Vim
?: Toggle NERD Tree's quick help

### SIMPLYFOLD

### vim-test

### indentwise
