# ESXi

## Installation

There are plenty of resources available to install ESXi. I had some
difficulties with my low-end celeron NUC. If you're interested in
how I got that going then [see here](esxi-nuc5cpyh.md).

## Initial set up
Navigate to the vSphere web-app ...

    https://<host-ip>/ui

## Set hostname:
From https://kb.vmware.com/selfservice/microsites/search.do?language=en_US&cmd=displayKC&externalId=1010821
`esxcli system hostname set --host=hostname`

## Install vSphere Client
VMWare is trying to push its web app for ESXi management. I think this is
ultimately a good thing. However, there are still some shortcomings with the
web interface so it can be useful to have the native Windows client.

Get it here:
https://kb.vmware.com/selfservice/microsites/search.do?language=en_US&cmd=displayKC&externalId=2089791

## Missing NTP servers
[See here](https://communities.vmware.com/thread/505146?tstart=0) for more
details but in short connect using the vSphere client:

Host > Configuration > Time configuration > General > Options... > NTP Settings

Add these three servers:

0.it.pool.ntp.org
1.it.pool.ntp.org
2.it.pool.ntp.org

## Restart services

SSH in and `services.sh restart`
[See here](https://serverfault.com/questions/196928/cant-connect-to-esxi-with-vsphere-client)


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

## Arch linux guest
You will have used the standard VM converter to create a new VM.
It will probably fail at 98%.

Create a new VM but re-use the disk
This will probably fail to boot too...

Do this: 
  * `e` at GRUB...
  * Find and change `initramfs-linux.img` to `initramfs-linux-fallback.img`
  * Login
  * Then `sudo mkinitcpio -p linux`

[Reference](https://wiki.archlinux.org/index.php/Moving_an_existing_install_into_\(or_out_of\)_a_virtual_machine#.22Waiting_10_seconds_for_device_.2Fdev.2Fsda1.3B_ERROR:_Unable_to_find_root_device_.27.2Fdev.2Fsda1.27.22)
