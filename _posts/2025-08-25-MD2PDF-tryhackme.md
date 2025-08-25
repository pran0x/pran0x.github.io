---
title: TryHackMe - MD2PDF
date: 2025-08-25 1:10:01 +0600
categories: [Try Hack Me, easy]
tags: [tryhackme, web, linux] # TAG names should always be lowercase
description: Hello Hacker!TopTierConversions LTD is proud to announce its latest and greatest product launch 'MD2PDF'. This easy-to-use utility converts markdown files to PDF and is totally secure! Right...?
media_subpath: /assets/img/tryhackme/
image:
  path: md2pdf/Writeups.png
  
---

![Tryhackme Room Link](md2pdf/room.png)
_<https://tryhackme.com/room/md2pdf>_

### Reconaissance
Fist recon the website and look which ports are open 
I can see  there are three open ports :
![recon](md2pdf/recon.png)

Checks every ports and we can see in `port:5000` it looks like both `port:80` and `port:5000` are same.


### Directory Fuzzing

Lets `fuzz` the website.
![dirbuster](md2pdf/dirbus.png)
Looks like we got some hidden info. let's access it. it says: `only localhost can access it`
![admin portal](md2pdf/admin.png)

### Verdict
so we can't access the localhost. let's try some other way.
After some research, I have found and artical [`Here`](https://www.intigriti.com/researchers/blog/hacking-tools/exploiting-pdf-generators-a-complete-guide-to-finding-ssrf-vulnerabilities-in-pdf-generators#what-are-pdf-generators)
So, basically i need to do [`SSRF`](https://www.intigriti.com/researchers/blog/hacking-tools/ssrf-a-complete-guide-to-exploiting-advanced-ssrf-vulnerabilities).

### Approch
I have tried some basic way like `img` tag but failed then tried `xss` with `javascript` but could works. Finally tried the `<iframe>` tag and it's worked.
![injection](md2pdf/injection.png)
![flag](md2pdf/flag.png)


### Conclusion

When a service developed, it's need to sanitize the user inputs, otherwise a simple injection can break the system.

### Reference 

- [PDF injection](https://www.intigriti.com/researchers/blog/hacking-tools/exploiting-pdf-generators-a-complete-guide-to-finding-ssrf-vulnerabilities-in-pdf-generators#what-are-pdf-generators)

- [SSRF](https://www.intigriti.com/researchers/blog/hacking-tools/ssrf-a-complete-guide-to-exploiting-advanced-ssrf-vulnerabilities)
