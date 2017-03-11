# Enable ethernet
Find your ethernet adapter name
`ip link`

Mine was ens33
`sudo nano /etc/sysconfig/network-scripts/ifcfg-ens33`

Change
`ONBOOT=no`

to
`ONBOOT=yes`

# Update all packages
`sudo yum install nano wget`
`sudo yum update`

# How To Enable EPEL Repository
`wget http://dl.fedoraproject.org/pub/epel/7/x86_64/e/epel-release-7-9.noarch.rpm`
`sudo rpm -ivh epel-release-7-9.noarch.rpm`

# Set timezone
https://www.cyberciti.biz/faq/centos-linux-6-7-changing-timezone-command-line/
