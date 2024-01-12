---
title: "Ranger a command-line file manager"
date: 2023-10-19T03:12:10+03:00
description: 'ranger is a commandline based application for viewing files on linux inspired keybindings'
tags: 
     - "opensource"
     - "file manager"
     - "cli-based"
image: images/cctv.jpeg
draft: true
---

## A command-line based file manager for the power user(kind of)
Ranger is a free and opensource versatile file manager designed for the command-line
. It provides a user-friendly interface for efficiently navigating, manipulating, and
organizing files and directories on linux. Ranger is also vim inspired and uses 
vim keybindings, this was one of the main reasons I started using it.

Developed by Roman Zimbelmann ranger offers features like customizable keybindings
and file previewing, making it a preferred choice for tech enthusiasts and
power users seeking an effective and streamlined file management solution.

To support the project visit their [page]("https://ranger.github.io/contact.html")

### how do I install ranger on linux
Ranger is availabe in most linux distribution package managers. So just run the
command to install it whichever distro you use.

In my case for fedora i run the following command.
```bash
sudo dnf install ranger
```

On ubuntu
```bash
sudo apt-get update
sudo apt-get install ranger
```

### Features
ranger supports a multitude of very important features which are not just cool
but very important.
**bulk rename** this is the first feature I look for in any file manager. I just 
cannot be understated how convinient and time saving the ability to rename 

### configurations
- ranger loads it's configurations from /home/user/.config/ranger/rc.conf
- the file manager is highly customizable with the ability to change multiple 
  things like keybindings, colorschemes, layouts, etc
