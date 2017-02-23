# Clone disk

 * List existing partitions: `fdisk -l /dev/sda`
 * Clone from sdX to sdY: `sudo dd if=/dev/sdX of=/dev/sdY bs=64K conv=noerror,sync status=progress`
 * [Clonezilla](http://clonezilla.org/fine-print-live-doc.php?path=./clonezilla-live/doc/03_Disk_to_disk_clone/00-prepare-clonezilla-live.doc#00-prepare-clonezilla-live.doc). Use k1 option

