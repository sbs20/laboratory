# ESXi

## Install VMWare tools
```
sudo apt-get install open-vm-tools
sudo systemctl start vmtoolsd.service
sudo systemctl enable vmtoolsd.service
```

## Transfer VMs
[Download ovftool](https://www.vmware.com/support/developer/ovf/)

```
ovftool -dm=thin vi://user@esxi1.example.com/<vmname>
vi://user@esxi2.example.com
```

Debug with `--X:abc=xyz` e.g.

```
ovftool --X:logFile=ovf.log --X:logLevel=verbose -dm=thin vi://user@esxi1.example.com/<vmname>
vi://user@esxi2.example.com
```

## Backup
See here: http://www.virten.net/2016/04/backup-solutions-for-free-esxi/

## Missing ethernet device after clone

These pages are useful. Particularly the first. Notably...

Shutdown the VM, ensure the network device is "e1000" and add the
following settings:

`ethernet0.virtualDev = "e1000"`

Either add it to the vmx file (for workstation player) or in ESXi
go to VM > Edit > VM Options > Advanced > Edit Configuration...

See here:
  * https://www.centos.org/forums/viewtopic.php?t=47118
  * https://blog.rabahi.net/?page_id=197
  * http://unix.stackexchange.com/questions/81834/how-can-i-change-the-default-ens33-network-device-to-old-eth0-on-fedora-19

## Arch linux
You will have used the standard VM converter to create a new VM.
It will probably fail at 98%.

Create a new VM but re-use the disk
This will probably fail to boot too...

But see here: 
https://wiki.archlinux.org/index.php/Moving_an_existing_install_into_(or_out_of)_a_virtual_machine#.22Waiting_10_seconds_for_device_.2Fdev.2Fsda1.3B_ERROR:_Unable_to_find_root_device_.27.2Fdev.2Fsda1.27.22

`e` at GRUB...
change `initramfs-linux.img` to `initramfs-linux-fallback.img`
then `mkinitcpio -p linux`

