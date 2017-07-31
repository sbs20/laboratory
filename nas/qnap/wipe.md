# Wiping data

## Linux / NAS
Unmount the disks you want to wipe. If they're part of a RAID array you need to unmount the array. This may cause issues on a NAS

`umount /dev/mdX` or `umount /dev/sdX`

Then write a random stream of data to disk. Older systems have no means of showing progress (see docs on `dd`)

```
dd if=/dev/urandom of=/dev/sdc bs=1M
```

More here: https://forum.qnap.com/viewtopic.php?t=104161

## Windows
Or pull out the drive and plug it into windows...

### Cipher
Remove all partitions and then create on big new partition.

Open a cmd prompt: `cipher /w:{DRIVE}`

### Diskpart
I've not used it.
