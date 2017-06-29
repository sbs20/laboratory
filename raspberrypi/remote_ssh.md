# Remote / external access

## !!! Warning !!!
You are exposing your private network to the outside world. Please be aware of what you are doing
and take ownership of it. Please ensure that:

1. You have configured [SSH authentication using keys](../linux/ssh-keygen.ssh)
1. You have disabled SSH by password
1. You have disabled root by SSH access

[More about SSH port forwarding](http://blog.trackets.com/2014/05/17/ssh-tunnel-local-and-remote-port-forwarding-explained-with-examples.html)

## Dynamic DNS
* Register at the Dynamic DNS provider of your choosing. I chose [FreeDNS](https://freedns.afraid.org/)
* Register a subdmain
* Navigate to [Dynamic DNS](https://freedns.afraid.org/dynamic/)
* Click the "Direct URL" link to get the URL required to update your subdomain. It will look something like: https://freedns.afraid.org/dynamic/update.php?abcdefghijklmnopqrstuvwxyz - copy this to use in the script below

When you request this link, the DDNS service will associate the remote IP address (i.e. your external IP) with the subdomain.

## Install upnpc
This is the program which asks your firewall to open a port
```
sudo apt-get install miniupnpc
```

## Create a script
Create a script file e.g. `nano configure_access.sh` and make it executable (chmod +x)
```
#!/bin/bash

# Register myself with FreeDNS - use your direct URL from above
curl -ks https://freedns.afraid.org/dynamic/update.php?abcdefghijklmnopqrstuvwxyz > /dev/null

# Get my local IP address
# NOTE: only works if you have a single IP. If you have more then you probably
# know enough about working round this.
LOCAL_IP=$(hostname -I)
LOCAL_PORT=22

# Choose an external port. 22 is fine but obvious
REMOTE_PORT=21122

# Punch a hole
upnpc -e 'RPi SSH' -a $LOCAL_IP $LOCAL_PORT $REMOTE_PORT 'TCP' > /dev/null
```

## References
[Access your Raspberry Pi from Anywhere](https://pavelfatin.com/access-your-raspberry-pi-from-anywhere/)

## Tunnel to other machines
* You are working on a remote device (X) with access to the internet
* You have SSH access to a device (A) on a network (N) behind a firewall
* (A) can access other devices on (N)
* You want access to another device (D) e.g. intranet site or Windows RDP on network (N) from (X)
* Use SSH tunneling
* In the example below:
    * REMOTE_HOST_PORT is (D) from the point of view of (A)
    * SSH_USER_HOST is (A) from the point of view of "the internet"
    * LOCAL_HOST_PORT is anything you want really - but you use this to connect

So if you run
```
ssh -L 9001:192.168.0.10:443 user@server.example.com -p 2323
```

Then you can think of this as connecting your local port 9001 to the remote network's 192.168.0.10:443; and you're SSHing into `user@server.example.com` on port 2323 to achieve it. Once you've SSHed then you can open a browser and navigate to `https://localhost:9001/` ... it will be as if you are on the remote network

### Useful script to create tunnel 
```
#!/bin/bash
# By default only bind the tunnel to the loopback address
LOCAL_HOST_PORT=9001

# If you know what you're doing then you can make it available to the local net
#LOCAL_HOST_PORT=0.0.0.0:9001

REMOTE_HOST_PORT=$1
SSH_USER_HOST=user@server.example.com
SSH_PORT=22222
ssh -L $LOCAL_HOST_PORT:$REMOTE_HOST_PORT $SSH_USER_HOST -p $SSH_PORT
```
References:
* [Simple forwarding](https://serverfault.com/a/214847)
* [Binding to address](https://superuser.com/a/591963/682739)
