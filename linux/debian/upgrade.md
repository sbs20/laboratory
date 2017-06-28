# Upgrade from Jessie to Stretch

```
apt-get update
apt-get upgrade
apt-get dist-upgrade
sudo cp /etc/apt/sources.list /etc/apt/sources.list.backup
sudo sed -i 's/jessie/stretch/g' /etc/apt/sources.list
apt-get update
apt-get upgrade
apt-get dist-upgrade
```

[Reference](https://linuxconfig.org/raspbian-gnu-linux-upgrade-from-jessie-to-raspbian-stretch-9)
