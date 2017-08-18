# HP ProLiant Microserver Gen 8

## Attempting to boot from MicroSD
Short version: if you want to use the MicoSD - buy it from HP.

More:
  * http://www.channelpronetwork.com/blog/entry/booting-hp-proliant-server-sd-card
  * https://www.aroundmyroom.com/2016/03/03/hp-microserver-gen8-g1610t-booting-with-usb-odd/
  * https://www.eteknix.com/everybody-can-nas-beginners-guide-openmediavault/
  * http://wiki.openmediavault.org/index.php?title=Install_on_usb_drive

## Boot from ODD SATA
You want to boot from the Optical Disk Drive (ODD) but you also have disks
in the RAID caddy. The server is trying to boot from the wrong place:

  * F9
  * Enable SATA Legacy. 
  * Esc, F10, Reboot
  * F9
  * Boot order: Start from \2

[Reference](https://community.hpe.com/t5/ProLiant-Servers-Netservers/Microserver-Gen8-Boot-order-from-different-SATA-Drive/td-p/6909839)

