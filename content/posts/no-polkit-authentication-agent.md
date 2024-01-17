---
title: "Fix i3 window manager error 'No Polkit Authentication Agent'"
date: 2024-01-17T16:04:20+03:00
description: 'in this article I show you how to fix the no polkit authentication agent error on linux if you are using i3 window manager | the steps may help you with another window manager'
image: 
draft: true
---

So, I recently switched to i3wm and ran into a small issue with running virt-manager
from the desktop entry. Turns out, I need root access for it to work. In my previous
setup with Fedora GNOME, I would simply get a password prompt with gnome-polkit.

But here's the thing: polkit-gnome only works with GNOME, so if you're using i3wm,
you'll need a different polkit manager. The most popular one for i3wm is lxpolkit. 

To fix the issue, you can easily install lxpolkit from your Linux distribution's
package manager which in my case is fedora. So I run 
```bash
sudo dnf install lxpolkit
```
Once that's done, just add the following
line to your i3config:
```i3
exec --no-startup-id lxpolkit
```

And voila! You're good to go.

Now, you might wonder why it's important to fix the issue this way instead of 
just running the app with sudo or doas in the terminal.

Well, the thing is, polkit acts as a middleman between privileged and unprivileged processes. 
It allows unprivileged applications to access privileged operations in a secure
manner. By using polkit instead of running everything with full root permissions,
we mitigate potential security risks.

Hope this explanation helps! Let me know if you have any more questions.
