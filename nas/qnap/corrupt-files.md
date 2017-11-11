# rsync errors / unable to delete file

I was getting an rsync failure. This happened soon after a disk failure (and
replacement of that disk)

```
rsync: readlink_stat("/share/MD0_DATA/.../PackageLayout") failed: Input/output
error (5)
```

I logged into a terminal and navigated to the directory in question

```
# rm PackageLayout
rm: unable to stat `PackageLayout': Input/output error
```

Checking the filesystem using the standard GUI did not fix the issue.

## *** This may signal the beginning of the end of your disks. BACKUP ***

In my case I think it was a result of a catastrophic disk failure and a slightly
unclean slip into degraded RAID. I'd already replaced the disk and rebuilt the
array. Further, I already had backups of all my data. I just wanted to fix the
issue so I could delete the rogue file.

## Filesystem check

Warning - you're about to run a filesystem check with automatic fixing. It will
probably be fine - but might not be. Please understand what you're doing and
take responsibility yourself.

You will almost certainly need to [unmount your shares](unmount-share.md) first.

Run fsck (e2fsck on qnap) and use the -p switch which will automatically fix
problems

```
e2fsck_64 /dev/md0 -p
```

If that's not available then 
```
e2fsck /dev/md0 -p
```
