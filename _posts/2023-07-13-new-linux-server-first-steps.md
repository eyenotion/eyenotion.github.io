---
title: First Steps For A New Linux Server Installation
date: 2023-07-13 19:43:00 +0000
categories: [Server, Linux]
tags: [ubuntu, linux, server, debian]     # TAG names should always be lowercase
author: eyenotion
toc: true
comments: false

---

<<<<<<< HEAD
## Ensuring Latest Updates Are Installed

We first need to ensure the latest system updates are installed. They often include security updates so this is especial important.

*I'll be using commands for an Ubuntu 22.04 based system, so these commands should work on any Debian based OS. If you're using something else you'll have to look up the relevant commands for your distro.*
=======
## Ensuring latest updates are installed

We first need to ensure the latest system updates are installed. They often include security updates so this is especial important.

**I'll be using commands for an Ubuntu based system, so these commands will work on any Debian based OS. If you're using something else you'll have to look up the relevant commands for your distro.**
>>>>>>> 571da22b9670b9e342c5cf019c51ac0a142482e8


All we need to do it run the 2 commands below, which checks for updates then applies them. The `apt update` first checks for availble updates, then `apt dist-upgrade` applies them and `-y` accepts any prompts to continue.

```bash
<<<<<<< HEAD
apt update
```

Now we'll run the actual process of downloading and isntalling the availble updates.

```bash
apt dist-upgrade -y
```
> Note you could also run the two commands together in a single prompt by putting `&&` between them like this; `apt update && apt dist-upgrade -y`
=======
apt update && apt dist-upgrade -y
```
> I'm running as `root` user. If you're not you'll need to start each command with `sudo`.
>>>>>>> 571da22b9670b9e342c5cf019c51ac0a142482e8

Now the system is running the latest updates we'll move to the next step.

## Creating A New User

Next we'll create a new user so we're not accessing the server or running commands as root. *You should only log in as the root user if absolutely required.*


```bash
adduser <username>
```

> Any time you see text between `<>`  replace it with relevant content for you.

The `adduser` command will guide you through the basics. It will prompt you to set the users password, then ask optional information like the users name and e-mail address. You can either fill in this optional information or hit Enter to lease it blank.

## Add A User To Sudo

Now we'll add the user we created to the sudo group so they have access to the `sudo` command

```bash
usermod -aG sudo <username>
```
The `-aG` appends, or adds, the user to the Group you've entered. In this case it's the `sudo` group to allow the user to use the sudo command.

## Set A Hostname

Now we'll set the server with a hostname. If this is the only server on your network than it doesn't really matter what this is, you could even skip this step and leave it as whatever the default is. If you have a lot of servers you might want to think carefully what name or naming scheme you use.

```bash
hostnamectl set-hostname <hostname>
```

We can now check the hostname by running `hostname`.

Now we need to edit the `host` file. To do this run;

```bash
nano /etc/hosts
```

You should get something that looks like this;
```bash
# /etc/hosts
127.0.0.1       localhost

# The following lines are desirable for IPv6 capable hosts
::1     ip6-localhost ip6-loopback
fe00::0 ip6-localnet
ff00::0 ip6-mcastprefix
ff02::1 ip6-allnodes
ff02::2 ip6-allrouters
```
We need to add the hostname you chose, we'll put it just under the existing localhost entry. *Note the IP address is different to the existing localhost IP.*

```bash
# /etc/hosts
127.0.0.1       localhost
127.0.1.1       <hostname>

# The following lines are desirable for IPv6 capable hosts
::1     ip6-localhost ip6-loopback
fe00::0 ip6-localnet
ff00::0 ip6-mcastprefix
ff02::1 ip6-allnodes
ff02::2 ip6-allrouters
```
Now we can save the changes and quit. Press `Ctrl + O` to save, then press `Enter` to confirm, then press `Ctrl X` to quit.

## Set An SSH Key

Using an SSH key to connect to your server remotely is a lot more secure then using password access. By using an SSH key we can disable password access and only sign in with the SSH key. This helps prevent potential 3rd parties from trying to gain unauthorised access to your server.

This is probably the most involving step so I have a seperate doc on that.

## Final Step and Conslusion

The last thing you want to do is reboot the server. Some changes won't have completed until you have rebooted, so go ahead and do that.

```bash
reboot
```
And that's it. We've completed the minimal steps needed to set up a new Linux installation.