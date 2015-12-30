# Setting up a wireless access point

## Update system
```
sudo apt-get update
```
## Get access point daemon and bridge-utils
```
sudo apt-get install hostapd
sudo apt-get install bridge-utils
```
## Shutdown wireless lan adapter in case it's running
```
sudo ifdown wlan0
```
## Edit the access point daemon config
sudo nano /etc/hostapd/hostapd.conf
```
interface=wlan0
driver=nl80211
ssid=your_ssid
hw_mode=g
channel=6
macaddr_acl=0
auth_algs=1
ignore_broadcast_ssid=0
wpa=2
wpa_passphrase=your_password
wpa_key_mgmt=WPA-PSK
wpa_pairwise=TKIP
rsn_pairwise=CCMP
bridge=br0
```

## Edit the access point startup
We need to set it up to point to our config file ...
```
sudo nano /etc/default/hostapd
```
... incommenting this line ...
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
#address 192.168.0.4

netmask 255.255.255.0
gateway 192.168.0.1
bridge_ports eth0 wlan0
```
## 

# Reboot
sudo reboot
