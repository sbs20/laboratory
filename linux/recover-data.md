# Data recovery
First, unmount any disk. Then get a direct image of it to a file so we have
a safe copy of it.

    dd if=/dev/hdb > /myimage.img

# Recover data
Use testdisk - `sudo apt install testdisk`. Then run it directly on the image

    testdisk myimage.img

Choose Analyse, then Advanced, then Undelete

# Mount image
Image files are not images of a partition, but of a whole disk. That means they
start with a bootloader and a partition table. You have to find out the offset
of the partition and mount it with the offset option of mount.

    fdisk -l /path/to/image

it will show you the block-size and the start-block of the partition. You can
use that to calculate the offset. For example, I have an image of a bootable
stick with a 4GB FAT32 partition. The output of the fdisk command is

```
Disk Stick.img: 3984 MB, 3984588800 bytes
249 heads, 6 sectors/track, 5209 cylinders, total 7782400 sectors
Units = sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disk identifier: 0x0004bfaa

    Device Boot      Start         End      Blocks   Id  System
Stick.img1   *         128     8015999     4007936    b  W95 FAT32
```

So I have a block-size of 512 bytes and the start-block is 128. The offset is
512 * 128 = 65536.

So the mount command would be

    mount -o loop,offset=65536 Stick.img /mnt/tmp
