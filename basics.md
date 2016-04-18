# The basics
For any of the recipes here make sure you have at least followed these steps

## Install Qnapware (Optware is no longer supported).
You can [find out more](http://forum.qnap.com/viewtopic.php?f=320&t=100843&sid=f723c2548796d064fee91a603c3e573f)
or download the install for [x86](http://qnapware.zyxmon.org/binaries-x86/installer/Qnapware_0.90_x86.qpkg)
or [ARM](http://qnapware.zyxmon.org/binaries-arm/installer/Qnapware_0.90_arm-x19.qpkg). Login to
your NAS, load App Center and choose "Install manually".

## Connect via SSH
2. Enable SSH server
3. Install putty and connect (use your admin account)

## Check and update Qnapware
```
opkg -version
opkg update
```

## Install nano
```
opkg install nano
```