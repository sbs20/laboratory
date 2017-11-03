# Enable ethernet
Find your ethernet adapter name

`ip link`

Mine was `ens33`. Edit the config file for that adapter...

`sudo nano /etc/sysconfig/network-scripts/ifcfg-ens33`

Change `ONBOOT=no` to `ONBOOT=yes`

# Packages
```
sudo yum update
sudo yum install nano wget
```

## How To Enable EPEL Repository
```
wget http://dl.fedoraproject.org/pub/epel/7/x86_64/e/epel-release-7-9.noarch.rpm
sudo rpm -ivh epel-release-7-9.noarch.rpm
```

# Set timezone
[Instructions](https://www.cyberciti.biz/faq/centos-linux-6-7-changing-timezone-command-line/)


# Weird caret / cursor behaviour in nano in some terminals
See [this](https://github.com/Microsoft/WSL/issues/1436) for details.

In summary add this to .bashrc
```
stty sane
export TERM=linux
```
