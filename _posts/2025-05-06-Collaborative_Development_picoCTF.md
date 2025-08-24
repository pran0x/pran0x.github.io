---
title: Collaboarative Development
date: 2025-05-05 11:50:16 +0600
categories: [Pico-CTF, General]
tags: [pico-ctf, easy, general] # TAG names should always be lowercase
description: My team has been working very hard on new features for our flag printing program! I wonder how they'll work together?
media_subpath: /assets/img/picoctf/
image:
  path: picoctf.png
---

### Getting Start

Here 3 branches in a working process without main branch, so our job is to do merge all  the branches to the main branch and print out the flag.py file.

1. download the file and open the .git folder. find the username and email for connect with the git   branch. connect to the git branch

        git config --global user.name 'username'                git config --global user.email 'email'

2. Here I follow one thing. I have created an another branch called pran and merge all the other three branches to it and then merge the pran branch to the main branch .

3. you need to know those things like git commit and  merge.

First go to the ./git main folder and type git branch -a. you will show a the  main branch along with the side three branches. - type git  branch <name> , here i wanted to just create an another branch for merge all the branches together. - after created type git branch -a  you will show the name which you created. now git switch <name> . you will switch to main to the branch you have created. here I have created a branch named pran - now git merge feature/part-1 . it will merge without showing any error. then type git commit -m "merged part-1". 

```rust
Completing local head
HEAD            feature/part-1  feature/part-3  pran                                                      
ORIG_HEAD       feature/part-2  main                                                                   
Completing recent commit object name
8395824  -- [8395824] add part 3 (1 year, 1 month ago)

```
same way feature/part-2,3 also be merged .

after all has been merged, type git log . you will see all the merge you have created.
then switch to main branch type git switch main . then merge the pran branch -> main branch type git merge pran

then type python3 flag.py . you will get your flag.

```rust
Printing the flag...
picoCTF{t3@mw0rk_m@k3s_th3_dr3@m_w0rk_2c91ca76}

 ```

 

### HAPPY HUNTING.....
