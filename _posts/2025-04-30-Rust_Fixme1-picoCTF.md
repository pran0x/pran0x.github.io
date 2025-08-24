---
title: Rust Fixme 1
date: 2025-04-30 07:32:42 +0600
categories: [Pico-CTF, General]
tags: [pico-ctf, easy, general] # TAG names should always be lowercase
description: Have you heard of Rust? Fix the syntax errors in this Rust file to print the flag!
media_subpath: /assets/img/picoctf/
image:
  path: picoctf.png
---

### Getting Start

Another Rust program ctf. its very easy and simple.. all though if you stuck , here it the solve

First open the main.rs file. if you don't know how to open then first solve previous 2 rust fixme3 & rust fixme2.
After open the main.rs file check the comments , you need to fix 3 thing
end of the program or in  short missing semicolon (;)
look at the return , its ret . replace it with return.
and the end, look at the ``println!()`` function. here on the function ``:?``. replace it with ``{:?}``.

### Ref :[why we use "{:?}"](https://doc.rust-lang.org/book/ch04-02-references-and-borrowing.html#:~:text=Note%20that%20a,%22%7Br3%7D%22%29%3B)

### Ans

run the file and it's done.
