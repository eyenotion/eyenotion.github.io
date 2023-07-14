---
title: First Steps For A New Linux Server Installation
date: 2023-07-13 19:43:00 +0000
categories: [Server, Linux]
tags: [ubuntu, linux, server, debian]     # TAG names should always be lowercase
author: eyenotion
toc: true
comments: false

---

## Ensuring latest updates are installed

We first need to ensure the latest system updates are installed. They often include security updates so this is especial important.

**I'll be using commands for an Ubuntu based system, so these commands will work on any Debian based OS. If you're using something else you'll have to look up the relevant commands for your distro.**


All we need to do it run the 2 commands below, which checks for updates then applies them. The `apt update` first checks for availble updates, then `apt dist-upgrade` applies them and `-y` accepts any prompts to continue.

```bash
apt update && apt dist-upgrade -y
```
> I'm running as `root` user. If you're not you'll need to start each command with `sudo`.

Now the system is running the latest updates we'll move to the next step.

## Creating a new user

Next we'll create a new user so we're not accessing the system or running commands as root. *You should only log in as the root user if absolutely required.*


```bash
adduser <username>
```

> Any time you see `<username>`  replace it with the name of your user.

The `adduser` command will guide you through the basics. It will prompt you to set the users password, then ask optional information like the users name and e-mail address. You can either fill in this optional information or hit Enter to lease it blank.

Now we'll add the user we created to the sudo group so they have access to the `sudo` command

```bash
usermod -aG sudo <username>
```

