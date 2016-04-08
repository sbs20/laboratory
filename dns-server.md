# Installing dnsmasq
Instructions from here: http://wiki.iccode.net/qnap/dnsmasq_config

Please note - there appears to be a whole new qpkg with a nice GUI for dnsmasq.
I have not tested it but it looks good: https://github.com/variab1e/dnsmasq-qpkg

## Prerequisites
[ipkg, putty, nano etc](basics.md)

## Install

```
    /opt/bin/ipkg install dnsmasq 
```

## hosts and resolve files
Copy files to a place where they won’t be overwritten at boot. See 
http://forum.qnap.com/viewtopic.php?f=90&t=24512 

```
    mkdir /etc/config/dnsmasq 
    cp /etc/hosts /etc/config/dnsmasq/hosts.conf
    cp /etc/resolv.conf /etc/config/dnsmasq/resolv.conf
```

### Edit hosts and resolv files to contain your data
This document doesn't go into detail regarding host and resolv configurations.
You will need to edit the following files
 
```
    nano /etc/config/dnsmasq/hosts.conf
    nano /etc/config/dnsmasq/resolv.conf
```

## dnsmasq kill
By default there doesn't appear to be a way of stopping dnsmasq. I created
the following file which seems to work
```
    nano /opt/etc/init.d/K56dnsmasq
```
    
Then paste this (it's a copy of S56dnsmasq without the "restart" lines)

```
    #!/bin/sh

    if [ -f /var/run/dnsmasq.pid ] ; then
    kill `cat /var/run/dnsmasq.pid`
    fi

    rm -f /var/run/dnsmasq.pid
```

And set permissions so it's executable
```
    chmod 755 K56dnsmasq
```

## Autostart
You need to make this run when your device reboots. See [autostart](autostart.md).
