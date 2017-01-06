# CUPS print server
This has been covered in lots of different places - see references below.
If you want to access the CUPS web console using a name rather than IP address then see the
ServerAlias reference below.

## Install the package
    sudo apt-get install cups

## Add current user to print group
    sudo usermod -a -G lpadmin pi

## Enable remote access to CUPS
The final thing to do before we start configuring the printer server itself, is to enable 
remote access to CUPS server. At the terminal, enter the following command:

    sudo nano /etc/cups/cupsd.conf

Inside the file, we comment out (add # sign in front of a line) or delete a line:

    Listen localhost:631

and replace it with:

    Port 631

Then, scroll further down in the config file until you see the 
location sections. Add the "Allow @local" lines which allow
requests from any device on the local network:
    
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

## Bad request accessing by DNS instead of IP?
To fix certain cases of Bad Request then also add

    ServerAlias *

See [here](https://bugs.launchpad.net/ubuntu/+source/cups/+bug/516018) for more details 

## Add your printer
Navigate to http://{ip-address}:631 - and follow your nose. I am using an old Canon iP90. 
In spite of there being a Canon PIXMA iP90 listed, I found that it didn't work and I had 
to use the [Canon PIXMA iP2000](http://www.michaelwood.me.uk/blag/2008/01/30/canon-ip90-gnu-linux-ubuntu/) 
driver even though this is January 2016.

## Get it working in Windows
See [here](https://wiki.archlinux.org/index.php/CUPS/Printer_sharing#Linux_server_-_Windows_client) for useful info.

In short, though, follow the settings for IPP and use the IP address - unless you can figure out how
to make windows play ball with nameservers

## References
 * [http://blog.pi3g.com/2013/08/using-the-raspberry-pi-as-cups-print-server-for-windows-and-apple-mac-airprint/]
 * [http://www.howtogeek.com/169679/how-to-add-a-printer-to-your-raspberry-pi-or-other-linux-computer/]
 * [https://wiki.archlinux.org/index.php/CUPS/Printer_sharing#Linux_server_-_Windows_client]
 * [https://bugs.launchpad.net/ubuntu/+source/cups/+bug/516018] 


