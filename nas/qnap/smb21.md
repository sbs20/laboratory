# Enabling SMB greater than 1.0

You need to [disable SMB / CIFS 1.0 on Windows](https://www.saotn.org/disable-smbv1-windows-10-windows-server/) because
Ransomware. But this means that all of a sudden you can't access your QNAP NAS.
You've tried [following the instructions](https://www.qnap.com/en/how-to/tutorial/article/how-to-use-smb-3-0-in-qts-4-2)
on the QNAP site and yet you don't have any fancy SMB version options on your
networking page.

The [solution](https://forum.qnap.com/viewtopic.php?t=125875) is to log in using
SSH and then:

```
[~] # smb2status
smbd (samba daemon) Version 3.6.25
smbd (samba daemon) is running.
max protocol SMB 1.0 enabled.

[~] # smb21enable
Shutting down SMB services: smbd nmbd.
Shutting down winbindd services: winbindd.
max protocol SMB 2.1 ... enabled.
locks path was set to /share/MD0_DATA/.locks
Shutting down winbindd services: winbindd.
Starting winbindd services:Starting SMB services:.
```

