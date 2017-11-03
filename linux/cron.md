# Cron
Use cron for scheduling tasks. To manage tasks one needs to edit the crontab
file. The best way to do this is:

```
crontab -e 
```
or for root
```
sudo crontab -e
```

## Creating a task 
```
# Every five minutes change directory and then run sudo ./autosync 
*/5 * * * * cd /home/pi && sudo ./autosync
# At 7 and 37 past the hour ...
7,37 * * * * cd /home/pi && sudo ./backup
```

## Settings (disabling) the mailout
```
MAILTO="alerts@myaddress.com"

# Disable ...
MAILTO=""
```