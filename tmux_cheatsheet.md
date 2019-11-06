# TMUX Workflow Cheatsheet

## Basic Workflow

**Sessions:** Use a session to store one entire context or project.

`tmux new -s robots_app`

In this workflow example you can see three projects when you type `tmux ls` to list sessions &amp; windows
```bash
robots_app: 2 windows
jupyter_notebooks: 1 windows
networks_app: 3 windows
```
`tmux attach -t 0` -> Connect/attach to specific session (sess 0 in this case) |

`C-b d` or `Ctrl-b D` -> detach current session, or detach from specific session

*Note: When you create a new session, tmux will by default start with one window and a single panel inside.*

**Windows:** Inside a session you can have windows, these allow you to keep various parts of a project open like if you have course notes and your notes in one window you may want to have your homework or an example script in another windows. Windows are just groupings of things you want to look at together.

`C-b c` -> create window

`C-b n` -> next window

`C-b p` -> previous window

`C-b <number>` specific window (see bottom left for window numbers)

`exit` -> close the window

**Panes:** These are separate panels that you see in a given window. For example we could have our course notes and your notes in one window but split in two panes vertically so you can see them next to eachother.

`C-b <` or `Ctrl-b >` -> access the next pane

`C-b %` -> Split vertically

`C-b "` -> Split horizontally

`C-b space` -> Iterate through split options

`C-b z` -> maximize pane, repeat command to minimize again

`exit` -> close the pane


## Other sometimes useful commands

| Command | Description |
|:--------|:------------|
| `tmux ls` | Figure out which session is running (0: bla bla bla) |
| `C-b ?` | see all key bindings |
| `C-b ,` | rename the current window |
| `C-b :` | enter command mode |
