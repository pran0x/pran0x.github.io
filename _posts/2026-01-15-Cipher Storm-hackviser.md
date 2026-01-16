---
title: Hackviser - Cipher Storm
date: 2026-01-15 10:30:00 +0600
categories: [Hackviser, Scenarios]
tags: [hackviser, web, linux, privilege, system, exploit] # TAG names should always be lowercase
description: Recent work by our team has revealed that a group called 'Cipher Storm' has been developing and selling ransomware and has seen a recent increase in activity. We know that this group writes and sells malware used in many ransomware attacks. To stop the group's activities, we need to reach the people behind it. The first step is to start analyzing the team's website. Good luck with your mission!
media_subpath: /assets/img/hackviser/scenarios
image:
  path: cipher-storm/cipher-storm.png
  
---

![Hackviser Scenarios Link](cipher-storm/room.png)
_<https://app.hackviser.com/scenarios/cipher-storm>_

### Reconnaissance

### Task : 1
#### What is the Telegram address used to communicate with the ransomware team?

First, we recon the website and found the `telegram link`

![Telegram link](cipher-storm/telegram.png)  

`t.me/FMBJmTEvVmGL_bot`

And also run `nmap` to check what's running.

```bash
nmap -A -sC -p- -v -T 5 <url>
```

![Nmap Command](cipher-storm/nmap-vuln.png)

We can see that two ports `80` and `22` are active. Also, the web server is running on an outdated Apache2 version `Apache/2.4.50 (Unix)`.

So, we're looking for its vulnerable CVE. We found CVE `CVE-2021-42013` for it: [Apache HTTP Server 2.4.50 - Remote Code Execution (RCE)](https://www.exploit-db.com/exploits/50446)


### Initial Access

### Task : 2
#### What is the full name of the first customer in the customer list?

We use `metasploit/msfconsole` for exploitation.

Run `msfconsole` and search for `apache 2.4.50`. Here we have get the payload with `excellent` rank.

![msfconsole](cipher-storm/msfconsole.png)

Select the exploit with `use 0`:

![POC](cipher-storm/msfconsole2.png)

Set the `RHOSTS`, `LHOST`, and `RPORT = 80`:

![POC setup](cipher-storm/msfconsole-c2.png)

> If you have connectivity issue then switch `set SSL false`.
{: .prompt-info }

![POC setup 2](cipher-storm/msfconsole-c2-2.png)

Great! We have successfully connected to the server

![C2](cipher-storm/shell-1.png)

Convert the `basic shell` to `interactive shell`

![C2](cipher-storm/shell-2.png)


Check to `home/black` for `sales.txt` file for solve 



![sales check](cipher-storm/shell-3.png)

### Task : 3
#### What is the 'IP:username:password' for the C2 server of customer 'Amelia Allen'?

![sales check 2](cipher-storm/shell-4.png)


### Privilege Escalation

### Task : 4
#### What is the 'Key' in the source code file of the ransomware the team developed?

After exploitation, we'll check for `SUID` binaries:

```bash
find / -user root -perm -4000 -exec ls -ldb {} \; 2>/dev/null
```

![SUID-CHECK](cipher-storm/suid.png)

Here we can see `screen 4.5.0` is set with SUID. After some research, we found an escalation method: [GNU Screen 4.5.0 - Local Privilege Escalation](https://www.exploit-db.com/exploits/41154)

We directly paste the exploitable scripts and check the `/tmp` folder to find `rootshell`. Run it and we'll see we have successfully switched from `daemon` user to `root` user.

![Escalate to root](cipher-storm/normal-to-root.png)

Now we go to the `/root` folder and check the `Dev` and `Document` folder.
For view the data of `/root` folder we use `python server`.In server terminal

```bash
python -m http.server 8080
```
![Python Server](cipher-storm/python.png)

Now I can access it from the browser at `http://cipherstorm.hv:8080/`

![Python Server](cipher-storm/python-server.png)

Now check the `dev/ransomware.java` for the key:

![key](cipher-storm/key.png)

### Task : 5
#### What is the name of one of the members of the ransomware team?