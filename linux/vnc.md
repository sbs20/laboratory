# Running VNC

A few points worth knowing. VNC isn't all that secure on its own; don't expose
it outside your network. In fact, to be honest you shouldn't expose it beyond
localhost - and then port forward over SSH.

You'll also need a display manager and desktop environment - especially if
you've been running a lite distro. 

  * Setup: `sudo apt install tightvncserver lxde lightdm`
  * Test: `vncserver :1 -geometry 1366x768 -depth 24 -dpi 96` then use your
    viewer to connect to `{host}:5901`
  * Secure: `vncserver :1 -geometry 1366x768 -depth 24 -dpi 96 -nolisten tcp -localhost`

# References
  * [Localhost](https://superuser.com/questions/715604/vncserver-localhost-and-ssh-tunneling)
  * [General](https://www.raspberrypi.org/forums/viewtopic.php?f=91&t=147884)

# XRDP (flakey)
Useful reference [here](https://www.reddit.com/r/Lubuntu/comments/2qxacn/getting_xrdp_working_on_lubuntu/) 
and also [here](https://bbs.archlinux.org/viewtopic.php?id=182374)

Install xrdp and lxde
```
sudo apt install xrdp lxde lightdm
```

Edit `/etc/xrdp/startwm.sh` and make it look like this (i.e. comment out Xsession)
```
#. /etc/X11/Xsession
. /usr/bin/startlxde
```

Change resolutions by editing ~/.Xdefaults and adding `Xft.dpi: 192`

Then change icons and taskbar [through the UI](https://askubuntu.com/questions/103807/how-can-i-change-the-icon-size-on-lubuntus-desktop)
