# Install desktop (18.04)
```
sudo tasksel install ubuntu-desktop
```

# systemd-resolved DNS bug (Ubuntu)

[See here](https://askubuntu.com/a/974482)

```
sudo rm -f /etc/resolv.conf
sudo ln -s /run/systemd/resolve/resolv.conf /etc/resolv.conf
sudo systemctl restart systemd-resolved
```
