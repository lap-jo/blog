---
title: "Change Lid Close Behaviour On Ubuntu and Fedora"
date: 2023-12-07T09:18:09+03:00
description: 'In this tutorial I show you how to disable or enable suspend on lid close on linux'
image: images/laptop-nikita.webp
draft: false
---

## Default behaviour
On most linux distributions the default behaviour is that when you close you laptop
lid the computer will suspended all processes inorder to save power. 

This is very useful as it reduces battery usage incase you unknowingly forgot to
turn off your computer before a long trip or in any other situation.

## But
There are situations where you will want this behaviour changed so that you can
tasks running with the lid closed.

Maybe you are trying to download a show late in the night on some crappy internet,
maybe you are compiling some applications while on your way to the cafe. Such things
would require you to have your pc running.

## How to actually change lid-close behaviour on linux
### 1. Using the commandline with systemd
  - using your favourite text editor (vim) edit the **logind.conf** file
    ```bash
    vim /etc/systemd/logind.conf 
    ```
- look for the line that says **HandleLidSwitch**
    ```bash
    #HandleLidSwitch=suspend ##by default it is set to suspend
    ```
- uncomment the line and change it to one of the below options depending on what you want
    ```bash
    HandleLidSwitch=ignore ##this will do nothing on lid close
    HandleLidSwitch=lock ## this will lock requiring you to input a password when you open the lid
    HandleLidSwithc=poweroff ## do not know what kind of psycho would use this
    ```
- save your changes and restart systemd login service with the command
```bash 
sudo systemctl restart systemd-logind.service
```
- this will likely log you out of your system and display a selinux error.
- switch to one of your tty with *Ctrl-Alt-F3* for tty3
- restart gdm.service from the tty3
- switch to the default tty1 and you should be able to login normally
