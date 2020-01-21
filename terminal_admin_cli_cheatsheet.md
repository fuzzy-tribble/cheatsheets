# Terminal Admin Stuff

## Users and Groups

`su`    Become superuser

`su someotheruser`   Become someotheruser

`dscacheutil -q user | grep -A 3 -B 2 -e uid:\ 5'[0-9][0-9]'`   List all user accounts

`dscl . list /groups` list groups

`dscacheutil -q group -a name <admin>`    List group `<admin>` members

`dseditgroup`   TODO

## Permissions

`ls -ld`    Display the default permission for a home directory

`ls -ld/<dir>`  Display the read, write, and access permission of a particular folder

`chmod 755 <file>`	Change the permission of a file to 755

`chmod -R 600 <dir>`	Change the permission of a folder (and its contents) to 600

`chown <user>:<group> <file>`	Change the ownership of a file to user and group. Add -R to include folder contents

## Processes

`ps -ax`	Output currently running processes. Here, a shows processes from all users and x shows processes that are not connected with the Terminal

`ps -aux`	Shows all the processes with %cpu, %mem, page in, PID, and command
top	Display live information about currently running processes

`top -ocpu -s 5`	Display processes sorted by CPU usage, updating every 5 seconds

`top -o rsize`	Sort top by memory usage

`kill PID`	Quit process with ID <PID>. You'll see PID as a column in the Activity Monitor

`ps -ax | grep <appname>`	Find a process by name or PID

## Search / Find / Grep

`find <dir> -name <"file">` Find all files named `<file>` inside `<dir>`. Use wildcards (*) to search for parts of filenames

`grep "<text>" <file>`	Output all occurrences of `<text>` inside `<file>` (add `-i` for case insensitivity)

`grep -rl "<text>" <dir>`	Search for all files containing `<text>` inside `<dir>`

## Pipes / Output

`cat <file>`	Output the content of `<file>`

`less <file>`	Output the contents of `<file>` using the less command that supports pagination and more

`head <file>`	Output the first 10 lines of `<file>`

`<cmd> > > <file>`	Appends the output of `<cmd>` to `<file>`

`<cmd> > <file>`	Direct the output of `<cmd>` into `<file>`

`<cmd1> | <cmd2>`	Direct the output of `<cmd1>` to `<cmd2>`

## Mount (manually) + Externally plugged in things
TODO