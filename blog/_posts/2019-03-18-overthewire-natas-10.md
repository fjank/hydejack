---
layout: post
title: Walkthrough - OverTheWire natas 10
description: >
  A walkthrough of OverTheWire natas 10 with tool recommendations,
  recommendations for further reading, recommendations for protecting your server
  against attackers, failures and wins. Natas level 10 is quite easy,
  giving you a very gentle introduction to this wargame.
---
# OverTheWire natas 10

[Read Previous - OverTheWire level 5-9 walkthrough.](2019-03-17-overthewire-natas-5-9.md)
## Introduction
[OverTheWire](http://overthewire.org) is a wargame site with several challenges.
For a beginner like me, it contains several challenges with a nice increase in
difficulty.
This is the second entry of a writeup of the [natas](http://overthewire.org/wargames/natas/)
challenges, which teaches the basics of serverside web-security. I will not
expose the actual passwords, but rather walk you through the mind-process
of searching for and finding vulnerabilities.

By going through all the levels of these challenges, you will learn how to
break basic security (and protect against these attacks!), gain basic knowledge on various
tools such as: html, server configuration, browser developer tools,
basic shell commands, vulnerability checker tools, kali linux and get some basic
programming experience.

## Level 10
Desc.
![Natas 5 landing page](/assets/img/overthewire-natas5-1.png)
OMG, `"" /etc/natas_webpass/natas11 #`
_Lessons learned: whitelist, not blacklist_
