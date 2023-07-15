---
title: Setting Up SSH Key For Secure Remote Access
date: 2023-07-15 13:54:00 +0000
categories: [Server, Linux]
tags: [ubuntu, linux, server, debian, ssh, keygen, remote, security]     # TAG names should always be lowercase
author: eyenotion
toc: true
comments: false

---

By default most people use their username and password to connect to their servers via SSH. While this works, it's not secure as passwords can be broken. 

By generating an SSH key and using this to connect, it makes it not only more secure, but can save time as you no longer need to enter a password ever time you connect.