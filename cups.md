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

# Linux drivers
If you want to print from linux then...
`sudo pacman -S ghostscript foomatic-db foomatic-db-engine`

# SAMBA / CUPS
sudo pacman -S samba cups ghostscript foomatic-db foomatic-db-engine


cp /etc/samba/smb.conf.default /etc/samba/smb.conf

sudo systemctl start smbd.service
sudo systemctl enable smbd.service

BJC-8200

Test print from command line `lp -d Canon-iP90 sam-nice3x.jpg`

Useful:
http://www.tldp.org/HOWTO/Debian-and-Windows-Shared-Printing/sharing_with_windows.html

