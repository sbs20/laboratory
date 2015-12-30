# Setting up a DHCP / DNS server
This is a simple DHCP and DNS server using dnsmasq. This allows you to reliably name your
local network machines as well taking away control of DHCP from your router. You may want 
to do this for a variety of reasons - whether just for the hell of it or because your ISP 
keeps resetting your router - or because your ISP has crappy and unreliable DNS servers. 
This fixes all of that.

## Update packages and install dnsmasq
```
sudo apt-get update
sudo apt-get install dnsmasq
```

## Setting a static IP address
You will want to do this to avoid having to rescan your network all the time and also
to give clients with cached DNS entries a chance.

### Edit your interfaces files
```
sudo nano /etc/network/interfaces
```
and make it look like the following. For more information about where to get network,
broadcast and gateway addresses see here: http://www.modmypi.com/blog/tutorial-how-to-give-your-raspberry-pi-a-static-ip-address
```
auto lo
iface lo inet loopback

# The following line is important. Without it things don't work
# Not completely sure why. Consider investigating further.
auto eth0
iface eth0 inet static
address 192.168.0.2
netmask 255.255.255.0
network 192.168.0.0
broadcast 192.168.0.255
gateway 192.168.0.1

allow-hotplug wlan0
iface wlan0 inet manual
    wpa-conf /etc/wpa_supplicant/wpa_supplicant.conf
```
### Disable the dhcp client daemon config
This is important because otherwise it will be requesting an address from itself
and it will also end up having two IP addresses; not the end of the world but also
not very tidy.
```
sudo nano /etc/dhcpcd.conf 
```
and append the following line
```
denyinterfaces *
```
## Create files
### dnsmasq.conf
```
sudo nano /etc/dnsmasq.conf
```
... and make it look like this ...
```
# Never forward plain names (without a dot or domain part)
domain-needed

# Never forward addresses in the non-routed address spaces.
bogus-priv

# Change this line if you want dns to get its upstream servers from
# somewhere other that /etc/resolv.conf
resolv-file=/etc/dnsmasq-resolv.conf

# Add local-only domains here, queries in these domains are answered
# from /etc/hosts or DHCP only.
local=/your_domain.com/

# If you don't want dnsmasq to read /etc/hosts, uncomment the
# following line.
# I suggest you leave this as is - the hosts file has a 127.0.1.1 address
# for your local machine and will banjax the shite out of everything
no-hosts

# Read another file, as well as or instead of /etc/hosts
addn-hosts=/etc/dnsmasq-hosts.conf

# Set this (and domain: see below) if you want to have a domain
# automatically added to simple names in a hosts-file.
expand-hosts

# Set the domain for dnsmasq. this is optional
domain=your_domain.com

# Uncomment this to enable the integrated DHCP server, you need
# to supply the range of addresses available for lease and optionally
# a lease time.
dhcp-range=192.168.0.32,192.168.0.128,12h

# Override the default route supplied by dnsmasq, which assumes the
# router is the same machine as the one running dnsmasq.
dhcp-option=3,192.168.0.1

# Your DNS servers
dhcp-option=6,0.0.0.0,192.168.0.5

# The DHCP server needs somewhere on disk to keep its lease database.
# This defaults to a sane location, but if you want to change it, use
# the line below.
dhcp-leasefile=/etc/dnsmasq.leases

# assign names to fixed ip address
address=/router.your_domain.com/192.168.0.1

# assign ip address to fixed names
dhcp-host=tau,192.168.0.3,infinite
``` 
### /etc/dnsmasq-resolv.conf
```
# google
nameserver 8.8.8.8
nameserver 8.8.4.4

# virgin
nameserver 194.168.4.100
#nameserver 194.168.8.100

search your_domain.com
```
### /etc/dnsmasq-hosts.conf
```
# [pi IP address]   [pi machine name]
# [other fixed IP address]    [other name]
# This circumvents /etc/hosts having a 127.0.1.1 address - dnsmasq will
# reply with THESE addresses instead
192.168.0.2	pi
```
## Service control commands
```
sudo systemctl status dnsmasq.service
sudo systemctl stop dnsmasq.service
sudo systemctl start dnsmasq.service
sudo systemctl restart dnsmasq.service
```
