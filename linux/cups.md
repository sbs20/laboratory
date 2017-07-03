# CUPS
```
sudo pacman -S cups
sudo nano /etc/cups/cupsd.conf
sudo usermod -a -G sys sbs20
sudo systemctl start org.cups.cupsd.service
sudo systemctl enable org.cups.cupsd.service
```
Set up a shared, Raw > Raw Queue printer
https://wiki.archlinux.org/index.php/CUPS/Printer_sharing#Sharing_via_IPP

Edit `/etc/cups/cupsd.conf`, change `Listen localhost:631` to `Port 631`, add `ServerAlias server.example.com` then, scroll further down in the config file until you see the location sections. Add the "Allow @local" lines which allow requests from any device on the local network:

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

# Linux drivers
If you want to print from linux then...
`sudo pacman -S ghostscript foomatic-db foomatic-db-engine`

Test print from command line `lp -d Canon-iP90 test.jpg`

# Printing from Windows

On the Windows computer, go to Control Panel->Devices and Printers and choose 'Add a printer'. If on Windows 10, click "The printer that I want isn't listed". Next, choose 'Select a shared printer by name' and type in the location of the printer: 

```
http://hostname:631/printers/printer_name
```

[Reference](https://wiki.archlinux.org/index.php/CUPS/Printer_sharing#Linux_server_-_Windows_client)

# Debugging
Have a look at the logs in `/var/log/cups`

# SAMBA / CUPS

I couldn't get SAMBA printing to work reliably. I don't know whether it's because of
permissions or SMB version. I used IPP

```
sudo pacman -S samba cups ghostscript foomatic-db foomatic-db-engine
cp /etc/samba/smb.conf.default /etc/samba/smb.conf
sudo systemctl start smbd.service
sudo systemctl enable smbd.service
```


Useful:
http://www.tldp.org/HOWTO/Debian-and-Windows-Shared-Printing/sharing_with_windows.html

