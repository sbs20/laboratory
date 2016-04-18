# Trying to unmount shares

Information from here: http://forum.qnap.com/viewtopic.php?t=111944

## Stop services:

```
/etc/init.d/services.sh stop
```

## Unmount devices

```
umount /dev/md0
```

if prompted with theses error-messages:

```
umount: /share/MD0_DATA: device is busy
umount: /share/MD0_DATA: device is busy
```

## Check for the service, that will disturb the unmounting of /md0

```
lsof +f -- /dev/md0
```

In the list you will find one ore more PIDs - these must be killed: example, if the PID is '9924':

```
kill 9924
```

then check again with 'lsof +f -- /dev/md0' until you will get an empty list

