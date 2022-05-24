# Cheatsheets Tool

SOME TEMP CHANGE

## Purpose

A terminal tool that allows you to easily peek at some custom notes or cheatsheets while you are working. Its also really useful if you are working without an internet connection.

I use this tool to remember my useful things that I always forget like how to configure routing tables, nmap switches, sign into a network without a gui, etc. 

Feel free to steal it, make it better, whatever.

## Usage

From terminal type:
`$ cheat <keyword>`

where `<keyword>` is vim, tmux, bash, or anything else you might have a cheatsheet for

## Instructions to make it work

1) make the `cheat` script executable (`chmod +x cheat`) the put it in the local bin folder (`user/local/bin`)
2) make sure bin is in your path (user/local/bin already in path on osx by default)
3) run it by typing `cheat <keyword>` or just `cheat` and it will prompt you for the cheatsheet you are looking for
