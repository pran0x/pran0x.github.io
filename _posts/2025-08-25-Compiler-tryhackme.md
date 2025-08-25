---
title: TryHackMe - Compiler
date: 2025-08-25 3:42:03 +0600
categories: [Try Hack Me, easy]
tags: [tryhackme, easy, reverse] # TAG names should always be lowercase
description: Strings can only help you so far.
media_subpath: /assets/img/tryhackme/
image:
  path: Compiler/Writeups.png
  
---

![Tryhackme Room Link](Compiler/room.png)
_<https://tryhackme.com/room/compiled>_

### Reconaissance
We have given the `Downloadable` file. let's open and observe it.
this is an compailer file with unreadable `texts`.
After run the compailer it's asking for the password:
![task](Compiler/task.png)
we don't know the password let's try to understand the file by using `cat` 
![logic](Compiler/logic.png)
We have got a logic. 

### Logic
So, basically we need to enter the  password  with this keyphrase `DoYouEven(sometext)`. we don't know what the last text it is. let's debug the compailer. 

Here i used [`ghidra`](https://dogbolt.org/) to Debug  the code. 
Close looks, we got and hint i guess.
look at the `logic part`
![clue](Compiler/clue.png)
We have got it. if the given password is == `DoYouEven__init` then the password is correct. if isn't then it will show `Try_again`

Let's try it.
![flag](Compiler/flag.png)
We have got the flag/answer.


### Vardict 
 the ans are alsow shown in the file when we opened it. 
![vardict](Compiler/vardict.png)
