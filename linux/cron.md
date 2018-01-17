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

## cron-apt
By default cron-apt only does "update" and not "upgrade". I think this is good.
Basically, just install it e.g. `sudo apt cront-apt`. You then need to update
`/etc/cron-apt/config` and include:

```
MAILON="upgrade"
SYSLOGON="always"
OPTIONS="-o Acquire::http::Dl-Limit=25"
MAILTO="me@gmail.com"
```
