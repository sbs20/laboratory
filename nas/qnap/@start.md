# The basics
For any of the recipes here make sure you have at least followed these steps

## Connect via SSH
1. Enable SSH server
2. Install putty and connect (use your admin account)

## Install Entware (Optware is no longer supported).
 * Latest Entware download : http://entware.zyxmon.org/binaries/other/Entware-ng_0.97.qpkg
 * Entware forum details : https://forum.qnap.com/viewtopic.php?f=351&t=116737&sid=b7d21ac543b1e3c41ac2a2d0ab0ae51e
 * You can [find out more](http://forum.qnap.com/viewtopic.php?f=320&t=100843&sid=f723c2548796d064fee91a603c3e573f)
    or download the install for [x86](http://qnapware.zyxmon.org/binaries-x86/installer/Qnapware_0.90_x86.qpkg)
    or [ARM](http://qnapware.zyxmon.org/binaries-arm/installer/Qnapware_0.90_arm-x19.qpkg).
 * Login to your NAS, load App Center and choose "Install manually".

### Check and update Entware
(You may need to restart your current shell in order to pick up the new $PATH)
```
opkg -version
opkg update
```

## Install nano
```
opkg install nano
```

## Consider installing Optware anyway
Optware is no longer supported - but it might still be better for you. Have a
look [here](http://forum.qnap.com/viewtopic.php?t=111389) for more detail or
just download the [package](http://download.qnap.com/QPKG/Optware_0.99.163.zip)
and install it manually.

You can find a list of packages for your architecture from the links below:

(arm) http://qnapware.zyxmon.org/binaries-arm/Packages.html
(x86) http://qnapware.zyxmon.org/binaries-x86/Packages.html

Check ipkg installation by typing ipkg –version. Also see [using ipkg](http://wiki.qnap.com/wiki/Using_IPKG)
Update pkgmgr

