# openmediavault

## "Failed to create a file system"
I was trying to install on a disk which had an existing linux installation - 
omv really didn't like it. When you get to the error, enter into shell:

```
# Find the physical disk
fdisk -l

# Fdisk...
fdisk /dev/sdX
```

Delete the partitions pressing `d` and enter

## Move QNAP NAS RAID disks to openmediavault 
There is a bigger discussion here. I am no expert in RAID so you may find 
better, more reliable witnesses than me. For what it's worth this is what I've
learned:

### Compatibility
  1. RAID needs a controller to mediate disk access.
  1. RAID controllers can be either hardware or software
  1. Hardware RAID controllers are expensive. If you're reading this, then you're
     probably more of the software RAID type.
  1. (A hardware RAID controller for the HP Proliant Servers costs ~$400)
  1. Software RAID is free and is used with less expensive, consumer grade
     devices. One such RAID controller is [mdadm](https://en.wikipedia.org/wiki/Mdadm)
  1. I do not *know* this, but I am willing to speculate that most if not all
     consumer NAS devices use `mdadm`.
  1. I *do* know that both QNAP and openmediavault use mdadm

### QNAP partitions
Just by way of background:
  * Disks from QNAP have three partitions
  * 2 of the partitions are configured to be RAID 1 - that is, they are the
    same across all disks
    * The partitions seem to contain firmware and QTS apps. It makes sense
      as it means that you can pull out any disk you like and maintain
      integrity
    * They are small - of the order of 500mb each
  * The third, large partition is the RAIDn data partition you're most
    interested in

### Hypothesis
It's possible to migrate RAID disks from any proprietory NAS device (QNAP,
Netgear, Synology, WD etc) to any linux host which supports mdadm provided
there is an existing destination host OS.

### Migrating
So, I only did this once. Maybe I was lucky. But in any case, I'd backed
everything up first. Please do the same. Or know that this is now *your*
responsibility.

Also note that you won't be able to migrate from QNAP to another proprietory
manufacturer e.g. Netgear, Synology etc. I expect (but do not know) that they
each store their firmware in a similar way to QNAP. If QNAP doesn't recognise
what's being plugged in it will destroy the data and format. I expect other
NAS devices to do the same.

That said, migrating to a pre-existing omv install, we're not doing anything
too destructive so you can probably abort the process even near the end.

  1. Backup
  1. Move the disks in the correct order. i.e. Bay 1 to bay 1, 2 to 2, etc
  1. Boot the destination (e.g. omv)
  1. Look in `RAID Management` - you should see your filesystem and get its
     device name e.g. /dev/md125
  1. Go to `File Systems`, highlight the device (/dev/md125) and mount. At
     this point you should already be able to look at the data (ssh and look
     around)
  1. Go to `Shared Folders`, add, select device, then the folder... Give it a
     name and save
  1. Go to your services and `SMB/CIFS` then add your share
  1. Double check that you can access your data.
  1. Reboot (mdadm device names appear to change)
  1. If everything is ok.... and you know you do not want to go back.... then
     you can delete the other filesystems on the disks - i.e. the smaller
     (500mb) firmware partitions.

## Filesystem check
Warning - you're about to run a filesystem check with automatic fixing. It
will probably be fine - but might not be. Please understand what you're doing
and take responsibility yourself.

You will need to unmount your share: `umount /dev/md125`

Run fsck and use the -p switch which will automatically fix problems

```
fsck /dev/md125 -f -p
```
