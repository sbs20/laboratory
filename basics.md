# Basics

## Inital login
Default username and password for raspbian are:
```
username: pi
password: raspberry
```
## Reboot
sudo reboot

## Changing the hostname
You need to edit two files
```
sudo nano /etc/hostname
```
replace "raspberrypi" with your new device name

In order to avoid "sudo: unable to resolve host" errors you will also need to edit your hosts file:
```
sudo nano /etc/hosts
```
and then replace the following line
```
127.0.1.1	raspberrypi
```

## Update your password
```
passwd
```

## Network
### Network interfaces
```
ifconfig
```
### IP addresses
```
ip addr show eth0
```
## Updating packages
```
sudo apt-get update
```
