# Setting up a DHCP / DNS server
This is a simple DHCP and DNS server using dnsmasq. This allows you to
reliably name your local network machines as well taking away control
of DHCP from your router. You may want to do this for a variety of
reasons - whether just for the hell of it or because your ISP keeps
resetting your router - or because your ISP has crappy and unreliable
DNS servers. This fixes all of that.

## Update packages and install dnsmasq
```
sudo apt-get update
sudo apt-get install dnsmasq
```

## Setting a static IP address
You will want to do this to avoid having to rescan your network all
the time and also to give clients with cached DNS entries a chance.

### Edit your interfaces files
```
sudo nano /etc/network/interfaces
```

and make it look like the following. For more information about where
to get network, broadcast and gateway addresses see
[here](http://www.modmypi.com/blog/tutorial-how-to-give-your-raspberry-pi-a-static-ip-address)
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

# I had some trouble getting name resoltion calls to work from the server itself.
# I did set the first line of resolv.conf to point at localhost but it still didn't
# work. I also added the google DNS servers to resolv.conf which works.... until you
# reboot. The following line fixes
dns-nameservers 8.8.8.8

allow-hotplug wlan0
iface wlan0 inet manual
wpa-conf /etc/wpa_supplicant/wpa_supplicant.conf
```

### Disable the dhcp client daemon config
This is important because otherwise it will be requesting an address from itself
and it will also end up having two IP addresses; not the end of the world but also
not very tidy. So `sudo nano /etc/dhcpcd.conf` and append the following line:
```
denyinterfaces *
```    
    
## Create and manage files
I do not use a single `dnsmasq.conf` but instead split the configuration into
various functions inside `/etc/dnsmasq.d/`. I have the following:

  * `dhcp.conf` which contains DHCP settings only. This is separate so that
    it can be excluded from secondary DNS servers
  * `dns.conf` contains the addresses for all your domain
  * `blacklist.conf` contains a list of bad addresses you want to direct to
    a sinkhole. See [here](https://pgl.yoyo.org/as/) or [here](https://pi-hole.net/)
    for other ideas
  * `log.conf` which contains just logging settings in case of debugging
  * `.resolve` upstream DNS servers
  * `.hosts` use this for localhost and your local DNS servers

### dhcp.conf
```
dhcp-range=192.168.0.128,192.168.0.192,12h

# Override the default route supplied by dnsmasq, which assumes the
# router is the same machine as the one running dnsmasq.
dhcp-option=3,192.168.0.1

# DHCP settings
dhcp-option=6,0.0.0.0,192.168.0.3
dhcp-leasefile=/etc/dnsmasq.d/.leases

# Fixed addresses
dhcp-host=server1,192.168.0.3,infinite
dhcp-host=A0:A0:A0:A0:A0:A0,192.168.0.10
```

### dns.conf
```
domain-needed
bogus-priv
resolv-file=/etc/dnsmasq.d/.resolv
local=/your-example.com/
no-hosts
addn-hosts=/etc/dnsmasq.d/.hosts
expand-hosts
domain=your-example.com

# Passthrough : https://serverfault.com/a/420748/428070
server=/server-x.your-example.com/8.8.8.8

# Local
address=/media.your-example.com/192.168.0.50

# Aliases
# cname=newalias.domain,existingname
cname=print.your-example.com,server1
```

### .resolv
```
# google
#nameserver 8.8.8.8
#nameserver 8.8.4.4

# virgin
#nameserver 194.168.4.100
#nameserver 194.168.8.100

# opendns
nameserver 208.67.222.222
nameserver 208.67.220.220

search your-example.com
```

### .hosts
```
127.0.0.1       localhost       localhost
192.168.0.2     server0         server0.your-example.com
```

## Service control commands
```
sudo systemctl status dnsmasq.service
sudo systemctl stop dnsmasq.service
sudo systemctl start dnsmasq.service
sudo systemctl restart dnsmasq.service
```
