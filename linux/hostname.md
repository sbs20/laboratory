# Changing the hostname
You need to edit two files
```
sudo nano /etc/hostname
```
replace `current-host-name` with your new device name

In order to avoid "sudo: unable to resolve host" errors you will also need to
edit your hosts file:
```
sudo nano /etc/hosts
```

and then replace the following line
```
127.0.1.1	`current-host-name`
```
