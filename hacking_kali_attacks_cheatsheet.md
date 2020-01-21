# Hacking ATTACKS Cheatsheet

**Purpose:** Because I have trouble keeping all this shit in my head (tools, usages, tips/tricks, key info/resources, etc). Not an exhaustive cheatsheet, just my favs and things I find most useful.

---

# Hacking Phases

## Stage 1: Recon (passive + active)

Also called footprinting, or information gathering we passively and actively collect as much information as possible about the TARGET (network, host, people involved)

**Tools:**
`ARIN`
`dnsrecon`
`goofile`
`goog-mail`
`goohost`
`theHarvester`
`metasploit`
`URLCrazy`
`whois`
`recon-ng`
`dnsrecon`
`WAF00W`
`traceroute`
`Whatweb`

## Step 2: Scanning and Enumeration

**Port scanning:** Scanning the target for the information like open ports, Live systems, services running on the host.

**Vulnerability Scanning:** Checking the target for weaknesses or vulnerabilities which can be exploited

**Network Mapping:** Finding the topology of network, routers, firewalls servers if any, and host information and drawing a network diagram with the available information.

**Tools:**
`nmap`
`nessus`
`nikto`
`openbox`
`metasploit`

## Step 3: Gaining Access

Break into the system/network, then increase his privilege to administrator (so we can install scripts needed to modify or hide data)

**Tools:**
`metasploit`

## Step 4: Maintaining Access

Maintain or persist the connection in the background without the knowledge of the user (via trojans, rootkits, malicious files, etc).

**Tools:**
`metasploit`

## Step 5: Covering Tracks

Clear all evidence so that in the later point of time, no one will find any traces leading to him (ie modifying/corrupting/deleting logs, modifying registry values and uninstalling stuff)

**Tools:**

---

# Password Cracking

## Cracking Shadow File Passwords

https://resources.infosecinstitute.com/hashcat-tutorial-beginners/
https://github.com/Mebus/cupp
http://wiki.securityweekly.com/wiki/index.php/Episode129
https://adaywithtape.blogspot.com.au/2011/05/creating-wordlists-with-crunch-v30.html
https://wiki.skullsecurity.org/Passwords
http://wiki.securityweekly.com/wiki/index.php/Episode129
http://www.netmux.com/blog/cracking-12-character-above-passwords
https://null-byte.wonderhowto.com/how-to/hack-like-pro-crack-passwords-part-3-using-hashcat-0156543/

## Cracking Network Passwords

## Hiding/Masking/Disappearing/Obfuscation
How to hide your computer/identity; avoiding detection

## Wireless Connect without GUI
```bash
# turn wireless card on:
ifconfig wlan0 # wlan0 is your wireless interface

# connect to network
iwconfig wlan0 essid <name> key <password>
    # Here
    # <name> -- your access point name
    # <password> -- your password

# Then obtain IP address:
dhclient wlan0
```

## Keylogger

## Spear Phishing
