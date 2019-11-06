# IRSSI Cheatsheet

*Note: See irc_cheatsheet.md for basic gettings started, setup*

`brew install irssi` or `apt-get install irssi`

## Bottom Bar

`[13:29] [uakari96(+Zi)][1: FreeNode (change with ^X)] [Act: 2,6,7]`

`[time] [mynick(myusermodes)][network] [active windows]`

Change default using `/STATUSBAR`

## Configs File

Your `~/.irssi/config` file stores all your custom configs (layout, connection preferences, etc)

`/SAVE`

`/RELOAD`

## Window Navigation

Switch Networks

`Ctrl+X`

Scroll

 `fn + up/down`

Change windows

`esc + <0-9>`

`/WINDOW <next or previous>`

`/WINDOW help`

Close window

`/WINDOW close`

Split windows

*Note: Irssi cannot do vertical splits, only horizontal splits.*

If you are in window 5 and you want to simultaneously see window 3:
`/WINDOW show 3`

This means that window 2 will always appear in the top container and never in the bottom container. The other four windows are non-sticky and do not have a set container, so they are free to move around to whatever the active container is.

`/WINDOW hide 3`

`/WINDOW balance`

`/WINDOW grow [<lines>]`

`/WINDOW shrink [<lines>]`

`/WINDOW size <lines>`

Save window layout in `~/.irssi/config`
`/LAYOUT save`

### Auto-connect to Network

Secure auto-connect

`/SERVER ADD -auto -tls -tls_verify -network freenode -port 6697 chat.freenode.net`
