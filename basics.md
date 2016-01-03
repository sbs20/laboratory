# Basics
This outlines various common tasks which all rely on your having terminal access to your pi.
If you don't have that then go and download PuTTY or something similar and then come back.
If you've just got your Pi out of the box and vaguely know about linux then start here.

## Inital login
Default username and password for raspbian are:

    username: pi
    password: raspberry

## Reboot
    sudo reboot

## Changing the hostname
You need to edit two files

    sudo nano /etc/hostname

replace "raspberrypi" with your new device name

In order to avoid "sudo: unable to resolve host" errors you will also need to edit your hosts file:
    sudo nano /etc/hosts

and then replace the following line
    127.0.1.1	raspberrypi

## Update your password
    passwd

## Network
### Network interfaces
    ifconfig

### IP addresses
    ip addr show eth0

### Bindings
    # All
    netstat -ltunp
    
    # Just for port 631
    netstat -ltunp | grep 631

## Updating packages
    sudo apt-get update

