# Packages
* Get latest information: `sudo apt-get update`
* Install updates: `sudo apt-get upgrade`
* Install nano: `sudo apt-get install nano`

# Disable X server
From [here](http://unix.stackexchange.com/a/264417)
```
systemctl set-default multi-user.target
```

# systemd-resolved DNS bug (Ubuntu)

[See here](https://askubuntu.com/a/974482)

```
sudo rm -f /etc/resolv.conf
sudo ln -s /run/systemd/resolve/resolv.conf /etc/resolv.conf
sudo systemctl restart systemd-resolved
```
