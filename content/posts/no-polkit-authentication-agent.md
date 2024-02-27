---
title: "Fix i3 window manager error 'No Polkit Authentication Agent'"
date: 2024-01-17T16:04:20+03:00
description: 'in this article I show you how to fix the no polkit authentication agent error on linux if you are using i3 window manager | the steps may help you with another window manager'
image: 
draft: false
---
## A little introduction
So, I recently switched to i3wm and ran into a small issue with running virt-manager
from the desktop entry. Turns out, I need root access for it to work. In my previous
setup with Fedora GNOME, I would simply get a password prompt with polkit-gnome.
Running it in the terminal without root gives me the *No Polkit Authentication*
error after it fails.

## Why do I get the "No Polkit Authentication Agent" error?
First you need to know what polkit does. Polkit, to put it simply grants access 
to privileged operation for unprivileged applications by acting as a framework 
for centralizing the decision making process.

It is more likely than not nowadays that you are running a linux distribution with
a full on  default desktop environment, let's use gnome here to get you on board.
Gnome being a desktop environment comes with a set of applications chosen
specifically to give you the "gnome experience" and this includes it's own polkit
authentication agent called polkit-gnome. And if you are reading this article it
probably means you have switched from gnome (or some other desktop environment)
to a window manager.

Now window managers too come with a set of dependencies, but most window managers
are built with minimalism in mind. This means less dependencies are downloaded 
allowing you the user are left to add whichever applications you need to perform
certain functions.

So it is likely that switching from gnome to i3 window manager will break certain
application functions. Like in this particular situation i3wm did not automatically
install a polkit authentication manager so you will need to install one yourself.

One I have tried and can recommend is **lxpolkit** but you can choose whichever
you want (this is why you switched to linux anyways).

You can easily install lxpolkit from your Linux distribution's package manager
which in my case is fedora. Run the below commands in your terminal emulator;

*Fedora*
```bash
sudo dnf install lxpolkit
```

*Ubuntu (or Debian and it's derivatives)
```bash
sudo apt install lxpolkit
```

Once that's done, just add the following
line to your i3config:

```i3
exec --no-startup-id lxpolkit
```

Now restart your i3 configuration and get to enjoying the full power of virtual
machines. Experiment, love and most importantly break as many virtual machines
as you can because that is what they are made for after all.

**NOTE:**
lxpolkit of course is not the only option and if it does not work well for you
there are many other options which you can find by searching your linux distributions
repositories or by reading the archwiki.

### Why fix the issue this way rather than just running as root?
You might wonder why it's important to fix the issue this way instead of 
just running the app with sudo or doas in the terminal.

Thing is, polkit acts as a middleman between privileged and unprivileged processes. 
It allows unprivileged applications to access privileged operations in a secure
manner. By using polkit instead of running everything with full root permissions,
you mitigate potential security risks.

### Conclusion
If you are new to i3 window manager or window managers in general

Hope this explanation helps! Let me know if you have any more questions by
messaging me on twitter through the link in the footer or by ![emailing](lapjo@tutanota.com) me

Also you can support the writing of these articles 

<a href="https://www.buymeacoffee.com/lapjo"><img src="https://img.buymeacoffee.com/button-api/?text=Buy me a beer&emoji=🍺&slug=lapjo&button_colour=FFDD00&font_colour=000000&font_family=Cookie&outline_colour=000000&coffee_colour=ffffff" /> </a> <br>
