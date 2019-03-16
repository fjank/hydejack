---
layout: post
title: OverTheWire
description: >
  A walkthrough of OverTheWire natas 0-4 with tool recommendations,
  recommendations for further reading, recommendations for protecting your server
  against attackers, failures and wins. Natas level 0-4 is quite easy,
  giving you a very gentle introduction to this wargame.
---
# OverTheWire natas 0-4

## Introduction
[OverTheWire](http://overthewire.org) is a wargame site with several challenges.
For a beginner like me, it contains several challenges with a nice increase in
difficulty.
This is the first entry of a writeup of the [natas](http://overthewire.org/wargames/natas/)
challenges, which teaches the basics of serverside web-security. I will not
expose the actual passwords, but rather walk you through the mind-process
of searching for and finding vulnerabilities.

By going through all the levels of these challenges, you will learn how to
break basic security (and protect against these attacks!), gain basic knowledge on various
tools such as: html, server configuration, browser developer tools,
basic shell commands, vulnerability checker tools, kali linux and get some basic
programming experience.

## Level 0
**Tools recommended:** A browser. I use [Chrome](https://www.google.com/chrome/)
or [Firefox](https://www.mozilla.org/en-US/firefox/new/).
{:.message}
View [the source](https://www.w3schools.com/html/html_intro.asp),
and look for the comment with the password for the next level.

_Lessons learned: Don't leave comments with sensitive data, they are easy to find._

## Level 1
Use the web developer tools ([Chrome DevTools](https://developers.google.com/web/tools/chrome-devtools/),
[Firefox developer tools](https://developer.mozilla.org/en-US/docs/Tools))
to show the source where you will find the password.

_Lessons learned: Blocking right-click is useless._

## Level 2
**Tools recommended:** [A shell](http://linuxcommand.org/lc3_lts0010.php).
{:.message}
As the page says, there is nothing on this page.
As in the previous level, I started by looking at the source, this time there
was nothing hidden in the source, except a reference to an image.  
I inspected the [response headers](https://code.tutsplus.com/tutorials/http-headers-for-dummies--net-8039)
to see if anything was hidden there, nada.  
I downloaded the image and displayed the raw data to see if there was something hidden
in the image, nada.
~~~shell
$ cat pixel.png
~~~
Perhaps there are other files in the same folder as the image? Lets try to open
the folder in the browser: http://natas2.natas.labs.overthewire.org/files/.  
Directory browsing is allowed, thus we see all the files including a file
containing the password to the next level.

_Lessons learned: Make sure directory browsing is disabled._

## Level 3
**Tools recommended:** [dirb](https://tools.kali.org/web-applications/dirb)/[dirbuster](https://www.owasp.org/index.php/Category:OWASP_DirBuster_Project)/[Kali linux](https://www.kali.org/).
You can manage nicely at this point
without using any of these tools, but everything will be easier if you install
Kali linux, as it contains massive amount of tools, almost everything you need.
{:.message}
Another page where there is nothing on the page.
The source contains a comment with a hint. Since I hate to guess, I used `dirb`
to enumerate all common files/directories that may be found on a server.
~~~shell
$ dirb http://natas3.natas.labs.overthewire.org -u natas3:<passwd>
~~~
Amongst the output you should find an interesting file: `robots.txt`  
The [robots file](http://www.robotstxt.org/) revealed a hidden directory (still with directory browsing enabled),
where a file containing the password to the next level can be found.

_Lessons learned: robots.txt should not expose sensitive information._

## Level 4
**Tools recommended:** [wget](https://www.gnu.org/software/wget/manual/wget.html)
{:.message}
The text on the page says it all. The way the page knows where we are coming
from is usually by inspecting the [Referer header](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Referer).
This can easily be faked, and there are tons of tools that can do this for us.
There is no need to bring up the big cannons yet, so we just use a "simple" tool
like `wget`. It seems simple enough, but there is enormous power hiding behind
the four letters. I recommend to use `wget` as a first "go-to-tool"
when you need to do simple request manipulation, as that will let you experiment
very quickly with various variables.
~~~shell
# The standard get of the page with no referer.
# --quiet to stop wget's output, you may want to skip this to see what wget is doing.
# -O - Will write the output to the standard out instead of a file.
$ wget --quiet -O - http://natas4:<passwd>@natas4.natas.labs.overthewire.org/
# A get with a faked referer header.
$ wget --quiet --referer=http://natas5.natas.labs.overthewire.org/ -O - http://natas4:<passwd>@natas4.natas.labs.overthewire.org/
~~~
It seems the referer header was the correct assumption, and the page delivered
the password for the next level.

_Lessons learned: Do not trust the browser, everything can be faked._
