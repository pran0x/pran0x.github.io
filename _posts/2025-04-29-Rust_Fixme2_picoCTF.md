---
title: Rust Fixme 2
date: 2025-04-29 2:22:17 +0600
categories: [Pico-CTF, General]
tags: [pico-ctf, easy, general] # TAG names should always be lowercase
description: The Rust saga continues? I ask you, can I borrow that, pleeeeeaaaasseeeee?
media_subpath: /images/picoCTF/
image:
  path: picoctf.png
---

### Reference: 

same as [Rust_Fixme3](/_posts/2025-04-28-Rust_Fixme3_picoCTF.md) Here we just need to  find out the pass by reference was currently referenced or not! that's it...

Need solve!? Here it is: 

### Getting Start:

First do same as Rust-fixme3 . then open the ``main.rs`` file and look at the string ref as &string . here just add &mut after the string as shows &mut string . then go to end of the code as line 34 . Here look string is without mut(mutable) reference . add &mut string   . Done 

Now run the file and you got it....


