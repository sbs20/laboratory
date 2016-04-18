# Run on startup / Autostart
This has been documented [elsewhere](http://wiki.qnap.com/wiki/Running_Your_Own_Application_at_Startup).
My preference is the second way.

## Prerequisites
[opkg, putty, nano etc](basics.md)

## Edit the qpkg config file
```
    nano /etc/config/qpkg.conf
```
Add a custom section something like
```
    [start_custom]
    Name = start_custom
    Version = 0.1
    Author = admin
    Date = 2015-06-26
    # The shell location needs to be somewhere available before share mounting takes place
    Shell = /share/MD0_DATA/.init/start.sh
    Install_Path = /share/MD0_DATA/.init/
    Enable = TRUE
```

## The start script
The configuration above points to this...
```
    nano /share/MD0_DATA/.init/start.sh
```

Enter the following (I am autostarting dnsmasq)
```
    #!/opt/bin/bash
    /opt/etc/init.d/S56dnsmasq start
```

Set permissions
```
    chmod 755 /share/MD0_DATA/.init/start.sh
```
    
## Then?
If you need to add anything else to your startup, just add it to this "start.sh" script