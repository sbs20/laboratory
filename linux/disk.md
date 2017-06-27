# Extend LVM disk

Set up with LVM and have /home in its own LVM
Go to VMWare - increase disk size
https://www.rootusers.com/how-to-increase-the-size-of-a-linux-lvm-by-expanding-the-virtual-machine-disk/

But where it says do lvdisplay - do lvscan instead


https://help.ubuntu.com/community/Partitioning/Home/Moving


Add a new disk
http://www.tutorialspoint.com/articles/add-new-harddisk-to-linux-system

Remove a disk / partition from a logical volume
https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/5/html/Logical_Volume_Manager_Administration/disk_remove_ex.html


Remove unused....
http://askubuntu.com/questions/477974/how-to-remove-unnecessary-locales

## Extending root partition

In this case the logical volume was not fully allocated. This was visible with either `sudo pvdisplay` and `sudo vgdisplay` which showed it was both allocatable and resizeable.

Decide how much you want to expand the size by (in PEs), then get the path of the volume to expand using `sudo lvdisplay` and use the LV Path. e.g.

```
  --- Logical volume ---
  LV Path                /dev/debian-vg/root
  LV Name                root
  VG Name                debian-vg
```

Then extend with something like:
```
sudo lvextend -l +1033 /dev/debian-vg/root
sudo resize2fs /dev/debian-vg/root
```

Good reference [here](http://geekswing.com/geek/unix/extending-a-linux-disk-with-lvm-extending-root-partition/)