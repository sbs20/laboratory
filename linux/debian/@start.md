# Packages
* Get latest information: `sudo apt-get update`
* Install updates: `sudo apt-get upgrade`
* Install nano: `sudo apt-get install nano`

# Disable X server
From [here](http://unix.stackexchange.com/a/264417)
```
systemctl set-default multi-user.target
```

# Getting XRDP working
Useful reference [here](https://www.reddit.com/r/Lubuntu/comments/2qxacn/getting_xrdp_working_on_lubuntu/) and also [here](https://bbs.archlinux.org/viewtopic.php?id=182374)

Install xrdp and lxde
```
sudo apt-get install xrdp lxde lightdm
```

Edit `/etc/xrdp/startwm.sh` and make it look like this (i.e. comment out Xsession)
```
#. /etc/X11/Xsession
. /usr/bin/startlxde
```

Change resolutions by editing ~/.Xdefaults and adding `Xft.dpi: 192`

Then change icons and taskbar [through the UI](https://askubuntu.com/questions/103807/how-can-i-change-the-icon-size-on-lubuntus-desktop)
