# Setting up a wireless access point
These instructions create a simple wireless access point. It creates a bridge between
your ethernet (eth0) and wireless (wlan0) which means that the wireless clients will
be on the same network and using the same DHCP / DNS server as everything else.

There are alternatives which create a separate network and rely on another DHCP server
and NAT - but I think they're a bit over the top.
[See here](https://learn.adafruit.com/setting-up-a-raspberry-pi-as-a-wifi-access-point/)
if that sort of thing excites you: 

## Update system
```
sudo apt update
```
## Get access point daemon and bridge-utils
```
sudo apt install hostapd bridge-utils
```
## Shutdown wireless lan adapter in case it's running
```
sudo ifdown wlan0
```
## Edit the access point daemon config
```
sudo nano /etc/hostapd/hostapd.conf
```
And replace its contents (if there are any) with this...
```
interface=wlan0
# You will need to change your driver to the correct one
driver=nl80211
# And your SSID
ssid=your_ssid
hw_mode=g
channel=6
macaddr_acl=0
auth_algs=1
ignore_broadcast_ssid=0
wpa=2
# And password
wpa_passphrase=your_password
wpa_key_mgmt=WPA-PSK
wpa_pairwise=TKIP
rsn_pairwise=CCMP
bridge=br0
```

And add this if you're doing this on a Raspberry Pi 3
```
ieee80211n=1
wmm_enabled=1
ht_capab=[HT40][SHORT-GI-20][DSSS_CCK-40]
```

## Edit the access point startup
We need to set it up to point to our config file ...
```
sudo nano /etc/default/hostapd
```
... uncommenting this line ...
```
DAEMON_CONF="/etc/hostapd/hostapd.conf"
```
## Edit the network interfaces file
```
sudo nano /etc/network/interfaces
```
... and replace its contents with ...
```
# interfaces(5) file used by ifup(8) and ifdown(8)

# Please note that this file is written to be used with dhcpcd
# For static IP, consult /etc/dhcpcd.conf and 'man dhcpcd.conf'

# Include files from /etc/network/interfaces.d:
source-directory /etc/network/interfaces.d

auto lo
iface lo inet loopback

# eth0 to have no IP at all
auto eth0
iface eth0 inet manual

# wlan0 not required for bridge

# bridge
auto br0

# Use this line if you're happy to run it on DHCP
iface br0 inet dhcp

# Uncomment the following lines if you want a static IP. If you do this then
# you will probably also want to add
# denyinterfaces *
# to the end of /etc/dhcpcd.conf
#iface br0 inet static
#address 192.168.0.20
#dns-nameservers 8.8.4.4 8.8.8.8

netmask 255.255.255.0
gateway 192.168.0.1

# Link eth and wlan
bridge_ports eth0 wlan0
```
## 

# Reboot
sudo reboot
