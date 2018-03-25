# Set up as a CIFS / SMB client
Reference here: http://geeks.noeit.com/mount-an-smb-network-drive-on-raspberry-pi/

```
sudo apt-get install cifs-utils
```

## Quick command line check

```
sudo apt install smbclient
smbclient //server/path -U username
```

## If you're using account credentials...
```
sudo nano ~/.smbcredentials
```
Then enter the following:
```
username=your_account_username
password=your_account_password
```
Update the permissions so that they're not visible to other users
```
sudo chmod 600 ~/.smbcredentials
```
## Create a stub folder to be your share location
```
sudo mkdir -p /mnt/public
```
## Edit your fstab
```
sudo nano /etc/fstab
```
Append lines this like
```
# This uses a guest account
//server_ip/Public /mnt/public cifs vers=2.0,guest,uid=1000,gid=1000,iocharset=utf8 0 0

# This uses a credentials file
//server_ip/Private /mnt/public cifs vers=2.0,credentials=/home/pi/.smbcredentials,uid=1000,gid=1000,iocharset=utf8 0 0
```
## Then mount
```
sudo mount -a
```
