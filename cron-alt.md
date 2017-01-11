# Cron ish
See https://jason.the-graham.com/2013/03/06/how-to-use-systemd-timers/
and https://wiki.archlinux.org/index.php/Systemd/Timers

## Script
`~/bin/backup`

## Service
Create `/etc/systemd/system/backup.service`

```
[Unit]
Description=Run backup script
After=local-fs.target network.target

[Service]
Type=simple

# Must be an absolute path
ExecStart=/usr/bin/su sbs20 -c "~/bin/backup"

[Install]
WantedBy=multi-user.target
```
## Timer
Create `/etc/systemd/system/backup.timer`

```
[Unit]
Description=Runs backup

[Timer]
# Time to wait after booting before we run first time
OnBootSec=1min

# Time between running each consecutive time
# OnCalendar=DayOfWeek Year-Month-Day Hour:Minute:Second

# Every 5 minutes between 8am and 10pm
#OnCalendar=8..22:0/5

# Every Friday morning at midnight and two seconds
OnCalendar=Fri 0:0:2

Unit=backup.service

[Install]
WantedBy=multi-user.target
```

## Starting
```
# Start timer, as root
sudo systemctl start backup.timer

# Enable timer to start at boot
sudo systemctl enable backup.timer
```

## Debug
`journalctl --unit backup.timer`
`journalctl -xe`

