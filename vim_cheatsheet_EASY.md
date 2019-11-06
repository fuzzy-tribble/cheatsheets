# Most Non-Intimidating VIM Cheatsheet Ever

## Mode Switching

`i` Enter insert mode

`:` Enter command mode

`esc` Return to normal mode from insert or replace mode

## Navigation

`h` `k` `j` `l` Left, right, up, down (can use arrow keys too)

`gg` First line of the file

`G` Last line of the file

`&#0036;` `^` Begining of line, end of line

`:20` Go to line 20 of the file

`:tag <tagname>` or `Ctrl-]` when your cursor is positioned over the tag name *(esp useful when browsing source code and you need to jump to function definitions, etc)*

## Editing (Copy/Paste/Delete)

`U` Undo

`Ctrl+R` Redo

`y` Yank

`p` Paste after the cursor

`c` ‘Change’; cut and enter insert mode

`d` Delete; cut but remain in normal mode


## Search/Replace

`/word\c` Find the next occurrence of ‘word’, ignoring case (‘\c’ can appear anywhere in the sequence being searched for)

`*` `#` Find the next, previous instance of the current word

`:s/foo/bar/` Replace the first occurrence of foo on the current line with bar


## Open/Close/Save Files
`:w` Save the current file

`:wq` Save the current file and close it; exits vim if no open files remain

`:sav` newname Save a copy of the current file as ‘newname’ and continue editing the file
‘newname’

`:q!` Close a file without saving
