---
title: Commitment issue
date: 2025-05-05 11:50:16 +0600
categories: [Pico-CTF, General]
tags: [pico-ctf, easy, general] # TAG names should always be lowercase
description: I accidentally wrote the flag down. Good thing I deleted it!
media_subpath: /images/picoCTF/
image:
  path: /images/picoCTF/picoctf.png 
---

### Getting Start:

This pico-CTF is pretty much tuff you are not use to at git.
to complete this CTF , first know about ==git init,commit,branch,add,merge.==

First download the file and open the hidden ./git file and open the head. here a refshared, Go to that directory.

Here we can see the username picoxyz and email xyz@ctf given  and a ==hash-type== text also, its your ==commit ID==. it's looks like this :

==e720dc26a1a55405fbdf4d338d465335c439fb3e==

now come back to ./git file. and type git config --global user.email "<email we have got>"

also git config --global user.name "<username we got we have got>"

now type git init. you show a message like this git ==reinitialized.==

type git log . you must be show this type of message :

```rust

  commit a6dca68e4310585eac3b5c9caf0f75967dfe972c (HEAD, master)
  Author: picoCTF <ops@picoctf.com>
  Date:   Sat Mar 9 21:10:06 2024 +0000
  
      remove sensitive info
  
  commit e720dc26a1a55405fbdf4d338d465335c439fb3e
  Author: picoCTF <ops@picoctf.com>
  Date:   Sat Mar 9 21:10:06 2024 +0000
  
      create flag
  
 ```

We can see here two commit shows, so, copy the 2nd commit where it shows ==create flag.==

Copy the commit id we need it on future.

type git merge <commit ID> .[we just copied now]

type git add . 

Done. now open the message.txt file you will got the flag...

### HAPPY HUNT..........!
