# CUPS

## Arch
```
sudo pacman -S cups
sudo nano /etc/cups/cupsd.conf
sudo usermod -a -G sys sbs20
sudo systemctl start org.cups.cupsd.service
sudo systemctl enable org.cups.cupsd.service
```

## Debian
```
sudo apt-get install cups
sudo usermod -a -G lpadmin pi
```

Set up a shared, Raw > Raw Queue printer
https://wiki.archlinux.org/index.php/CUPS/Printer_sharing#Sharing_via_IPP

Enable remote access: edit `/etc/cups/cupsd.conf`, change `Listen localhost:631`
to `Port 631`, add `ServerAlias server.example.com` (add multiple lines if
desired) then, scroll further down in the config file until you see the
location sections. Add the "Allow @local" lines which allow requests from any
device on the local network:

```    
<Location / >
    # Restrict access to the server...
    Order allow,deny
    Allow @local
</Location>

<Location /admin>
    # Restrict access to the admin pages...
    Order allow,deny
    Allow @local
</Location>

<Location /admin/conf>
    AuthType Default
    Require user @SYSTEM
    # Restrict access to the configuration files...
    Order allow,deny
    Allow @local
</Location>
```

Now restart CUPS `sudo systemctl restart cups`

## Bad request accessing by DNS instead of IP?
To fix certain cases of Bad Request then also add

    ServerAlias *

See [here](https://bugs.launchpad.net/ubuntu/+source/cups/+bug/516018) for more details 

# SSL certificates
All the defaults point to `/etc/cups/ssl`. Put your key and cert in there.

**The filenames need to match the common name, e.g., for "print.example.com"
cupsd will look for "print.example.com.crt" and "print.example.com.key"**

[Reference](https://lists.cups.org/pipermail/cups/2014-December/072112.html)

You can also disable the creation of self signed certs - edit `cups-files.conf`
and add: `CreateSelfSignedCerts no`

# Linux drivers
If you want to print from linux then...
`sudo pacman -S ghostscript foomatic-db foomatic-db-engine`

Test print from command line `lp -d Canon-iP90 test.jpg`

# Printing from Windows

On the Windows computer, go to Control Panel->Devices and Printers and choose
'Add a printer'. If on Windows 10, click "The printer that I want isn't
listed". Next, choose 'Select a shared printer by name' and type in the
location of the printer: 

```
http://hostname:631/printers/printer_name
```

[Reference](https://wiki.archlinux.org/index.php/CUPS/Printer_sharing#Linux_server_-_Windows_client)

# Debugging
Have a look at the logs in `/var/log/cups`

# SAMBA / CUPS
I couldn't get SAMBA printing to work reliably. I don't know whether it's
because of permissions or SMB version. I used IPP

This is what I did manage:
```
sudo pacman -S samba cups ghostscript foomatic-db foomatic-db-engine
cp /etc/samba/smb.conf.default /etc/samba/smb.conf
sudo systemctl start smbd.service
sudo systemctl enable smbd.service
```

Useful:
http://www.tldp.org/HOWTO/Debian-and-Windows-Shared-Printing/sharing_with_windows.html

## References
 * [http://blog.pi3g.com/2013/08/using-the-raspberry-pi-as-cups-print-server-for-windows-and-apple-mac-airprint/]
 * [http://www.howtogeek.com/169679/how-to-add-a-printer-to-your-raspberry-pi-or-other-linux-computer/]
 * [https://wiki.archlinux.org/index.php/CUPS/Printer_sharing#Linux_server_-_Windows_client]
 * [https://bugs.launchpad.net/ubuntu/+source/cups/+bug/516018] 

