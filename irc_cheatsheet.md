# IRC Cheatsheet

**Purpose:** This cheatsheet is intended to help N00Bs get familiar with IRC commands, terminology

*Internet Relay Chat: an old school chat protocol that a lot of hackers/devs and gamers use*


## First Time Setup

Create a "nick" and register it with "NickServ" so you can reserve the nickname you want.

**1) Join the freenode network. Open your favorite IRC client and type:**

`/server chat.freenode.net`

**2) Choose a username (called a "nick")**

 `/nick NewNick`

**3) Register your nick**

`/msg NickServ REGISTER password youremail@example.com`

**4) Check your e-mail and verify your account**

**5) Type the command that freenode asks you to type, into the server box.**

`/msg nickserv register your_password your_email_address`

**6) Identify with Nickserv.**

`/msg nickserv identify Your-Nick Your-Password`

---

## Networks & Servers

**An IRC server** is a single machine that's running an IRC daemon which you can connect to.

**An IRC network** is a group of IRC servers which are linked together.

When servers are linked into a network, they behave like a single large server -- usernames and channels are shared within the network, and you can communicate with users on other servers within the network without any special steps.

Users still connect to individual servers, but it's as if they are connected to the whole network.

### Find Networks and/or Servers

You can check what is there by default using `/network list` or `/server list` (eg, FreeNode, GameSurge, QuakeNet, etc)

You can also search for networks and/or servers on Google then add them using `/network add <network deets>`

```
/NETWORK ADD -sasl_mechanism external rizon
/SERVER ADD -auto -tls -tls_verify -tls_cert ~/.irssi/certs/Rizon.pem -network rizon -port 6697 irc.rizon.net
```

Src: https://wiki.rizon.net/index.php?title=SASL

### Connect to Networks and Servers
To connect to a server using a secure cxn make sure you use ...

*Note: usually you can find this on the wiki page or instruction page for accessing the network or server.*

`/CONNECT -tls`

If you are using the IRSSI client you can also double check your `~/.irssi/config` file to make sure your secure cnx settings are saved

```
address = "chat.us.freenode.net";
chatnet = "freenode";
port = "7000";
use_ssl = "yes";
ssl_verify = "yes";
ssl_capath = "/etc/ssl/certs";
autoconnect = "yes";
```
----

## Channels

Each network or server has channels associated with it...these are basically chat topics.

### Find Channels
Finding channels on FreeNode using `alis` (a network service designed for exactly that purpose)

`/msg alis HELP LIST`

Find channels whose name contains the term in question

`/msg alis LIST *searchterm*`

`/msg alis LIST *linux*`

Find all channels in the freenode namespace with at least 10 users.

`/msg alis LIST #freenode* -min 10`

### Join Channels
To join a channel use `/JOIN #channelname`.

`/JOIN #irchelp`

### Auto-join channel
`/CHANNEL ADD -auto #pylowiki freenode`

### Remove channel
`/CHANNEL REMOVE <channel> <network>`

----

## Users

### List all users on a channel
`/names`

This will give you a list of users on the current channel BUT NOT users that are invisible (usermode `+i`).

To find out deets on a particular user type `/whois <user nick>`

---

## Sending and Receiving Messages

`msg <nick> <message>`
Send a private message to a user (as opposed to a channel)

`part [room] [message]`
Leave the current channel, or a specified channel, with an optional message

`ping [nick]`
Asks how much lag a user (or the server if no user specified) has

`query <nick> <message>`
Send a private message to a user (as opposed to a channel)

`quit [message]`
Disconnect from the server, with an optional message

`say <message>`
Send a message normally as if you weren't using a command

----

# ChanServ and NickServ

**NickServ**, is an IRC command that enables users to register their nick, so they are the only user with that name, helping prevent confusion and false identification.

`/nickserv identify password`

`/msg nickserv help`

**ChanServ**, on many IRC networks, is an IRC service which maintains channel registration and access information.

`/msg ChanServ  REGISTER channel password description`

`/msg ChanServ  IDENTIFY channel password`

`/msg ChanServ  SET channel option parameters`

`/msg ChanServ HELP`
