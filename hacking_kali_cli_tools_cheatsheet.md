# CLI Hacking TOOLS Cheatsheet

**Purpose:** Because I have trouble keeping all this shit in my head (tools, usages, tips/tricks, key info/resources, etc). Not an exhaustive cheatsheet, just my favs and things I find most useful.

---

## `grep` `egrep` `fgrep`
Find search patterns

`egrep` == `grep -E`: --extended-regexp
`fgrep` == `grep -F`: --fixed-strings

```bash
#TODO
```

## `tr`
Translate characters (replace chars)

```bash
#TODO
```

## `cut`
Cut out sections

```bash
# Cut using delimeter
cut -d " "
```

## `chmod`
Change access perms (change mode)

Add/remove execute perms for everyone
```bash
chmod +x script.sh
chmod -x script.sh
```

Add/remove execute (x) perms for owner/current user (u)
```bash
chmod u+x script.sh
chmod u-x script.sh
```

Add/remove execute (x) perms for user (u), group (g), owner (o)
```bash
chmod ugo+x script.sh
chmod ugo-x script.sh
```
*Note: `ugo` can be replaced with `a` for all*

Numerical notation permissions

- 4 = r (Read)
- 2 = w (Write)
- 1 = x (eXecute)

Create triplets for your user by adding above digits:

To represent rwx triplet use 4+2+1=7

To represent rw- triplet use 4+2+0=6

To represent r– triplet use 4+0+0=4

To represent r-x triplet use 4+0+1=5

```bash
$ chmod 750 script.sh
# 7 – Full permission for owner (rwx = 4+2+1=7)
# 5 – Only read and execute perms to group (rx = 4+0+1=5)
# 0 – Remove world permission (— = 0+0+0=0)

$ chmod 0700 file.txt
# 0 – Use set setuid, setgid, or sticky bit
# 7 – Full permission for owner (rwx = 4+2+1=7)
# 0 – Remove group permission (— = 0+0+0=0)
# 0 – Remove world permission (— = 0+0+0=0)

```

## `chown`
Change owner

List all changes made
```bash
$ chown -v -R guest:friends linux
# changed ownership of `linux/redhat/rh7' to guest:friends
# changed ownership of `linux/redhat' retained to guest:friends
# ownership of `linux/redhat_sym' retained as guest:friends
# ownership of `linux/ubuntu_sym' retained as guest:friends
# changed ownership of `linux/linuxKernel' to guest:friends
# changed ownership of `linux/ubuntu/ub10' to guest:friends
# ownership of `linux/ubuntu' retained as guest:friends
# ownership of `linux' retained as guest:friends
```

Change owner to root
```bash
$ ls -lart tmpfile
# -rw-r--r-- 1 himanshu family 0 2012-05-22 20:03 tmpfile

$ chown root tmpfile

$ ls -l tmpfile
# -rw-r--r-- 1 root family 0 2012-05-22 20:03 tmpfile
```

Change file ownership group to friends
```bash
$ ls -l tmpfile
# -rw-r--r-- 1 himanshu family 0 2012-05-22 20:03 tmpfile

$ chown :friends tmpfile

$ ls -l tmpfile
# -rw-r--r-- 1 himanshu friends 0 2012-05-22 20:03 tmpfile
```

Change file owner and group owner
```bash
$ ls -l tmpfile
# -rw-r--r-- 1 root family 0 2012-05-22 20:03 tmpfile

$ chown himanshu:friends tmpfile

$ ls -l tmpfile
# -rw-r--r-- 1 himanshu friends 0 2012-05-22 20:03 tmpfile

```

Change owner IF file is owned by particular user
```bash
$ ls -l tmpfile
# -rw-r--r-- 1 root friends 0 2012-05-22 20:03 tmpfile

$ chown --from=guest himanshu tmpfile
# doesn't work because file is owned by root, not guest

$ ls -l tmpfile
# -rw-r--r-- 1 root friends 0 2012-05-22 20:03 tmpfile

$ chown --from=root himanshu tmpfile
# works because file is owned by root

$ ls -l tmpfile
# -rw-r--r-- 1 himanshu friends 0 2012-05-22 20:03 tmpfile
```

Change group IF file is already owned by certain group
```bash
$ ls -l tmpfile
# -rw-r--r-- 1 himanshu friends 0 2012-05-22 20:03 tmpfile

$ chown --from=:friends :family tmpfile

$ ls -l tmpfile
# -rw-r--r-- 1 himanshu family 0 2012-05-22 20:03 tmpfile
```

Copy owner/group settings from one file to another
```bash
$ ls -l file
# -rwxr-xr-x 1 himanshu family 8968 2012-04-09 07:10 file

$ ls -l tmpfile
# -rw-r--r-- 1 root friends 0 2012-05-22 20:03 tmpfile

$ chown --reference=file tmpfile

$ ls -l tmpfile
# -rw-r--r-- 1 himanshu family 0 2012-05-22 20:03 tmpfile

```

Change the owner/group of the files by traveling the directories recursively
```bash
$ ls -l linux/linuxKernel
# -rw-r--r-- 1 root friends 0 2012-05-22 21:52 linux/linuxKernel

$ ls -l linux/ubuntu/ub10
# -rw-r--r-- 1 root friends 0 2012-05-22 21:52 linux/ubuntu/ub10

$ ls -l linux/redhat/rh7
# -rw-r--r-- 1 root friends 0 2012-05-22 21:52 linux/redhat/rh7

$ chown -R himanshu:family linux/

$ ls -l linux/redhat/rh7
# -rw-r--r-- 1 himanshu family 0 2012-05-22 21:52 linux/redhat/rh7

$ ls -l linux/ubuntu/ub10
# -rw-r--r-- 1 himanshu family 0 2012-05-22 21:52 linux/ubuntu/ub10

$ ls -l linux/linuxKernel
# -rw-r--r-- 1 himanshu family 0 2012-05-22 21:52 linux/linuxKernel
```

## `su`
Switch user

Become super user
```bash
$ su
```

Switch to someotheruser
```bash
$ su someotheruser
```

## `curl`
Data transfer in terminal (using MANY diff options and protocols)

Get page source
```bash
$ curl example.com
```

Get response headers
```bash
curl --head http://www.facebook.com/
```

Most often, we aren’t interested in the response body. You can simply hide it by “saving” the output to the null device

```bash
$ curl -vo /dev/null https://www.booleanworld.com/
```

Download files
```bash
# Name the file to be downloaded
curl -o vlc.dmg http://ftp.belnet.be/mirror/videolan/vlc/3.0.4/macosx/vlc-3.0.4.dmg

# Use default name
curl --remote-name http://ftp.belnet.be/mirror/videolan/vlc/3.0.4/macosx/vlc-3.0.4.dmg
```

## `wget`
Like `curl` but supports only HTTP , HTTPS and FTP

Download single file and stores in a current directory
```bash
wget http://ftp.gnu.org/gnu/wget/wget-1.5.3.tar.gz
```

Downloads file with different file name
```bash
wget -O wget.zip http://ftp.gnu.org/gnu/wget/wget-1.5.3.tar.gz
```

Download multiple files
```bash
wget http://ftp.gnu.org/gnu/wget/wget-1.5.3.tar.gz ftp://ftp.gnu.org/gnu/wget/wget-1.10.1.tar.gz.sig
```

## `cewl`
Creates custom word lists for password cracking using words gathered from crawling websites

Create custom words list given target website
```bash
# NOTE: MAY TAKE SEVERAL HOURS
cewl -w customwordlist.txt -d 5 -m 7 www.sans.org
```
- `-w customwordlist.ext`: the `-w` means write to the file name that follows
- `-d 5`: the depth (in this case, 5) that CeWL will crawl to website
- `-m 7`: the minimum word length; in this case it will grab words of 7 characters minimum.

## `crunch`
Generates wordlists for password cracking

```bash
crunch <min> max<max> <characterset> -t <pattern> -o <output filename>
```
- `<min>` `<max>`= password length
- `<characterset>` = The character set to be used in generating the passwords
- `-t <pattern>` = The pattern of the generated passwords
- `-o <outputfile>` = This is the file you want your wordlist written to

Generate all possible passwords between 4 and 8 characters
```bash
crunch 4 8
```

Generate a complete list of password possibilities between 6 and 8 chars and send them to file
```bash
crunch 6 8 1234567890 -o /root/numericwordlist.lst
```

If we know birthday is July 28 we could generate all passwords of 10 chars that end in 0728 (@ is wildcard)
```bash
crunch 10 10 -t @@@@@@0728 -o /root/birthdaywordlist.lst
```

Generate all 8 character passwords with only alphabetic chars
```bash
crunch 8 8 -f /usr/share/rainbowcrack/charset.txt mixalpha -o /root/alphawordlist.lst
```
- `-f /path/to/charset.lst <charactersetname>` switch allows us to choose the character set we want to use to generate our wordlist

## `hashcat`
Password cracker (uses precomputed dictionaries, rainbow tables and bruteforce)

```bash
hashcat -h
```

 Dictionary attack
```bash
hashcat -m 0 -a 0 -o cracked.txt target_hashes.txt /usr/share/wordlists/rockyou.txt

cat cracked.txt
# dc647eb65e6711e155375218212b3964:Password
# eb61eead90e3b899c6bcbe27ac581660:HELLO
# 75b71aa6842e450f12aca00fdf54c51d:P455w0rd
# 2c9341ca4cf3d87b9e4eb905d6a3ec45:Test1234
# 958152288f2d2303ae045cffc43a02cd:MYSECRET
```
- `-m 0` hash types --> MD5
- `-a 0` attach mode --> dictionary attack
- `-o cracked.txt` is the output file for the cracked passwords
- `target_hashes.txt` is our input file of hashes
- `/usr/share/wordlists/rockyou.txt` is the absolute path to the wordlist file for this dictionary attack.

Dictionary attack with rules
```bash
hashcat64.exe -a 0 -m 0 example_md5_hashes.txt combined_seclists_password_list.txt -r rules\d3ad0ne.rule -O
```

## `john`
Finds weak passwords

Simple mode
```bash
# Create passwd file with >=1 hashed pswds (if you dont have one already)
echo -n "SecRet" | md5sum | tr -d ” -” >> target_hashes.txt

# Make sure its there
cat target_hashes.txt

# User john on the hashed password file
john target_hashes.txt
john --show mypasswdfile2crack
```
- `-n` removes the new line added to the end (important as we don’t want the new line characters to be hashed with our password)
- `tr –d " -"` removes any characters that are a space or hyphen from the output

Crack with wordlist
```bash
john passwordfile –wordlist=”wordlist.txt”
```

Using wordlist and rules
```bash
john --wordlist=”wordlist.txt” --rules --passwordfile
john --format=krb5tgs ticket.txt --wordlist=rockyou.txt --progress-every=3
```

Show results
john –show passwordfile
john --show --users=0 passwordfile
john –-show –-groups=0,1 passwordfile

```bash
#TODO
```

## `service` `systemctl`
Use `service` to start, stop, restart or examine the status of a service.

For more complex tasks, however, the actual command being used, be that `initctl` or `systemctl` or the `/etc/init.d` script might have to be used directly.

Using `service`
```bash
service apache2 status
service apache2 start
service apache2 stop
service apache2 restart
```

Using `systemctl`
```bash
systemctl status apache2
systemctl start apache2
systemctl stop apache2
systemctl restart apache2
```
So that we don’t have to start the service each time we log in
```bash
systemctl enable ssh postgresql
```

```bash
# Restarts a service only if it is running.
systemctl try-restart name.service

# Reloads configuration if it's possible.
systemctl reload name.service

# try to reload but if it's not possible restarts the service
systemctl reload-or-restart name.service
```

```bash
systemctl is-active name.service # running
systemctl is-enabled name.service # will be activated when booting
systemctl is-failed name.service # failed to load
```

## `netcat` or `nc`
Establish a listening port

```bash
# Listen on any iface, port 7777 for any connections
nc -nvlp 7777
```

## `netstat`
Display's network statistics about how your computer is communicating with other computers or network devices

```bash
# Show active connections on your machine
netstat -anl
```

```bash
netsat --all
netstat --listening
netstat --interfaces
netstat --route
```

List all known services, find port conflicts, detecting if you've been compromised
```bash
# TODO
```

## `traceroute`
Shows the route packets take to network host

```bash
traceroute geekflare.com
# OR
traceroute 291.284.29.2
```

## `iwconfig` `ifconfig`
Configure network interfaces

`iwconfig` only deals with the wireless elements of a wireless card: the ESSID, WEP keys, etc. All the normal attributes of the network card (IP address, subnet mask etc) are assigned through `ifconfig`.

Note: loopback address == localhost

Show network interfaces
```bash
ifconfig
```

Change interface IP address manually
```bash
ifconfig eth0 192.168.1.115
```

Change interface MAC Address
```bash
ifconfig eth0 hw ether AA:BB:CC:DD:EE:FF
```

Change the netmask and broadcast address
```bash
ifconfig eth0 192.168.1.115 netmask 255.255.255.0 broadcast 192.168.1.255
```

Enable/disable network interface
```bash
ifconfig eth0 up
ifconfig eth0 down
# OR
ifup eth0
ifdown eth0
```

Enable/Disable Promisc Mode
```bash
ifconfig eth0 promisc
ifconfig eth0 -promisc
```

```bash
# TODO iwconfig
```

## `dhclient`
Linux has a DHCP server that runs a daeman called dhcpd. It's this DHCP server that assigns IP addresses to all the systems on the subnet. It also keeps logs files of which machines had which IP addresses at which time.

*Note: Its this log that is often used to trace hackers in a forensic analysis after an attack*

The `dhclient` command sends out `DHCPDISCOVER` request from the default NIC.

It then gets an offer (DHCPOFFER) of 192.168.1.114 from the DHCP server, then confirms the IP assignment to the DHCP server.

To release the current lease
```bash
dhclient -r
```

When you want to be assigned a new address from the DHCP server
```bash
dhclient
```
*Note: Type `ifconfig` to check that the DHCP server has assigned a new IP address.*

Renew/release for a specific interface
```bash
dhclient -r eth0
dhclient eth0
```

## `dig` `nslookup`
DNS (Domain Name Services) enables us to type in a domain name like www.wonderhowto.com, which it then translates to the appropriate IP address.

`nslookup` is for Windows-based systems, gives only basic info

Get info on WonderHowTo's name servers
```bash
dig wonderhowto.com ns
```

Get info on WonderHowTo's email servers
```bash
dig wonderhowto.com mx
```

## `scp` `ftp` `sftp`
`scp` (non-interactive) Securely copy files to and from another host in the network

`ftp` (interactive) Copying files to and from other computers

`sftp` (interactive) Securely copy files

Copy file from local to server
```bash
scp report.doc username@remote.host.net:
```

Copy file from server to local
```bash
scp username@remote.host.net:report.doc report.doc
```

Specify a new name for the file
```bash
scp report.doc username@remote.host.net:monday.doc
```

Copy file to a directory relative to the home directory
```bash
scp report.doc username@remote.host.net:reports/monday.doc
```

Copy a directory recursively to a remote location
```bash
scp -r mail username@remote.host.net:
```
*Note: Use the `-p` flag to preserve timestamps of file and dirs users, groups, perms*

## `telnet` `ssh`

`telnet` unencrypted remote login --> OLD / VELNERABLE

`ssh` encrypted remote login (uses symetrical encryption or asymetrical encr, or hashing)

General syntax: `ssh {user}@{host}`
```bash
# TODO
```

Generating a key
```bash
ssh-keygen -b 4096
```

```bash
ssh-add
```

## `w`
Prints a summary of activity on system (including each user)
```bash
w
```

## `route` `ip route`
Display or modifies the IP routing table

`route` was replaced by `ip route`

Display routing table
```bash
# TODO
```

Add flush delete change monitor

## `arp`
Address resolution protocol to resolve internet layer addresses (IP addresses) into link layer addresses (MAC addresses)

*Note: ARP Spoofing works by sending fake MAC addresses to the switch*

Display all of arp cache
```bash
arp -a
```
Add static arp entry
```bash
arp –s  192.168.1.38 60-36-DD-A6-C5-43
```

Delete arp cache entry
```bash
arp –d 192.168.1.38
```

## `nmap`
nmap -Pn -sSU -sV --top-ports 20
nmap -n -Pn -T5 -sS <current_IPrange>
nmap NSE scripts

## `netdiscover`
netdiscover -r <current_IPrange>


## `tcpdump`
Sniffing and analyzing packets via command line

Basic sniffing
```bash
tcpdump -n

 # Verbose
tcpdump -v -n
```
- `-n` don't resolve ip addresses to hostnames

Get ethernet headers (link layer headers)
```bash
tcpdump -vv -n -e
```

Sniffing a particular interface
```bash
tcpdump -D
# 1.eth0
# 2.usbmon1 (USB bus number 1)
# 3.usbmon2 (USB bus number 2)
# 4.any (Pseudo-device that captures on all interfaces)
# 5.lo

tcpdump -i 1
tcpdump -i eth0
```

Sniff specific protocol
```bash
tcpdump -n tcp
```

Sniff specific host or port
```bash
tcpdump -n 'src 192.168.1.101'
tcpdump -n 'udp and dst port 53'
```

Sniff FTP packets coming from 192.168.1.100 to 192.168.1.2
```bash
tcpdump 'src 192.168.1.100 and dst 192.168.1.2 and port ftp'
```

Sniffing w/ grep search
```bash
tcpdump -n -A | grep -e 'POST'
```

Sniff anything on eth0 with credentials
```bash
tcpdump -i eth0 port http or port ftp or port smtp or port imap or port pop3 -l -A | egrep –i 'pass=|pwd=|log=|login=|user=|username=|pw=|passw=|passwd=|password=||name=|name:|pass:|user:|username:|password:|login:|pass |user ' --color=auto --line-
```
# `ngrep`
`ngrep` (network grep) is a network packet analyzer (a grep-like tool applied to the network layer – it matches traffic passing over a network interface)

```bash
ngrep -q -W byline "GET|POST HTTP"
```

## `exiftool`
Extract/insert information from a file (meta-information)

```bash
exiftool a.jpg
```

## `strings`
Look inside a binary/executable file to grab human-readable strings

```bash
strings testfile
```

Custom char limit
```bash
strings -n 2 test
```

## `recon-ng`
Recon-ng is a reconnaissance tool with an interface similar to Metasploit.

```bash
[recon-ng][default] > help
[recon-ng][default] > marketplace search
```

Install Module
```bash
[recon-ng][default] > marketplace install hackertarget
[*] Module installed: recon/domains-hosts/hackertarget
[*] Reloading modules...
[recon-ng][default] >
```
Load Module
```bash
[recon-ng][default] > modules load hackertarget
[recon-ng][default][hackertarget] >
```

```bash
[recon-ng][default][hackertarget] > show options

  Name    Current Value  Required  Description
  ------  -------------  --------  -----------
  SOURCE  default        yes       source of input (see 'show info' for details)
```

Set Source
```bash
[recon-ng][default][hackertarget] > options set SOURCE tesla.com
SOURCE => tesla.com

[recon-ng][default][hackertarget] > info

Options:
  Name    Current Value  Required  Description
  ------  -------------  --------  -----------
  SOURCE  tesla.com      yes       source of input (see 'info' for details)

Source Options:
  default      SELECT DISTINCT domain FROM domains WHERE domain IS NOT NULL
  string       string representing a single input
  path         path to a file containing a list of inputs
  query sql    database query returning one column of inputs
```

```bash
  econ-ng][default][hackertarget] > input

    +---------------+
    | Module Inputs |
    +---------------+
    | tesla.com     |
    +---------------+
```

Run Module
```bash
[recon-ng][default][hackertarget] > run

---------
TESLA.COM
---------
[*] [host] tesla.com (209.133.79.61)
[*] [host] sjc04d1rsaap02.tesla.com (205.234.27.206)
[*] [host] model3.tesla.com (205.234.27.221)
[*] [host] marketing.tesla.com (13.111.47.196)
[*] [host] email.tesla.com (136.147.129.27)
[*] [host] mta2.email.tesla.com (13.111.4.231)
[*] [host] mta.email.tesla.com (13.111.14.190)
[*] [host] xmail.tesla.com (204.74.99.100)
[*] [host] comparison.tesla.com (64.125.183.133)
[*] [host] na-sso.tesla.com (209.133.79.81)
[*] [host] edr.tesla.com (209.133.79.33)
[*] [host] mta2.emails.tesla.com (13.111.88.1)
[*] [host] mta3.emails.tesla.com (13.111.88.2)
[*] [host] mta4.emails.tesla.com (13.111.88.52)
[*] [host] mta5.emails.tesla.com (13.111.88.53)
[*] [host] mta.emails.tesla.com (13.111.62.118)
[*] [host] click.emails.tesla.com (13.111.48.179)
[*] [host] view.emails.tesla.com (13.111.49.179)
[*] [host] events.tesla.com (13.111.47.195)
[*] [host] shop.eu.tesla.com (205.234.27.221)
[*] [host] sso-dev.tesla.com (209.133.79.66)

-------
SUMMARY
-------
[*] 21 total (0 new) hosts found.
```

Show Hosts
```bash
[recon-ng][default][hackertarget] > show hosts

  +------------------------------------------------------------------------------------------------------------+
  | rowid |           host           |   ip_address   | region | country | latitude | longitude |    module    |
  +------------------------------------------------------------------------------------------------------------+
  | 1     | tesla.com                | 209.133.79.61  |        |         |          |           | hackertarget |
  | 2     | sjc04d1rsaap02.tesla.com | 205.234.27.206 |        |         |          |           | hackertarget |
  | 3     | model3.tesla.com         | 205.234.27.221 |        |         |          |           | hackertarget |
  | 4     | marketing.tesla.com      | 13.111.47.196  |        |         |          |           | hackertarget |
  | 5     | email.tesla.com          | 136.147.129.27 |        |         |          
```

## `metasploit`
[Metasploit Scanning](https://www.metasploit.com/):
`auxiliary/scanner/*`,
`portscan/tcp`,
`http/http_version`,
`http/tomcat_enum`,
`http/trace_axd`

[Discover](https://github.com/leebaird/discover):
Custom bash scripts used to automate various penetration testing tasks including recon, scanning, parsing, and creating malicious payloads and listeners with Metasploit.

---

# Additional Resources

## TODO
