# KVM

Installing KVM and Kinchi on Ubuntu isn't straightforward. And nor is migrating
VMs over from ESXi. Or rather, it isn't unless you've spent a few days trying.

## Install QEMU on Ubuntu 17.10
[Instructions for ubuntu 17.10](https://www.hiroom2.com/2017/11/30/ubuntu-1710-kvm-en/)

```
sudo apt install -y qemu-kvm libvirt0 libvirt-bin virt-manager bridge-utils
sudo systemctl enable libvirtd.service
```

Edit your `/etc/network/interfaces`
```
auto lo
iface lo inet loopback
auto br0
iface br0 inet dhcp
      # Choose your network interface here.
      bridge_ports <eno1>
      bridge_stp off
      bridge_maxwait 0
```
You need to reboot after this. I tried just restarting `networking` and it
didn't go well... but was fine after a hard reset.

The user in libvirt group can run libvirt command without sudo
```
sudo gpasswd libvirt -a <username>
```

## Kimchi (web UI)
Then install [kimchi](https://github.com/kimchi-project/kimchi/releases/latest)

But you have to do things in a particular way. Download the two `.deb` packages
from the link above. Then...
 
```
sudo apt install nginx
sudo dpkg -i wok-2.5.0-0.noarch.deb
sudo apt-get install -f
sudo service wokd start
sudo reboot now

sudo dpkg -i kimchi-2.5.0-0.noarch.deb
sudo apt-get install -f
sudo reboot now
```

Then navigate to `https://<address>:8001`

### Change SSL port
Edit `/etc/nginx/conf.d/wok.conf` change `listen 0.0.0.0:8001 ssl;`, the
`location / proxy_redirect` and the HTTP server rewrite.

Then edit `/etc/wok/wok.conf`, uncomment `proxy_port = 8001` and change to `443`

Finally
```
sudo systemctl restart wokd
sudo systemctl restart nginx
```

## Uninstall
```
sudo dpkg -r kimchi wok
sudo apt remove nginx kvm qemu-kvm libvirt0 libvirt-bin virt-manager bridge-utils
sudo apt autoremove
```

## Installing within ESXi
It looks like some brave souls have done this - but KVM didn't seem to like it.
I gave up after a few hours.

## Installing VMs
See [virt-v2v](http://libguestfs.org/virt-v2v.1.html)

### From ESXi
Install
```
sudo apt install libguestfs-tools
```

If you are copying from ESXi then
[you need to:](http://libguestfs.org/virt-v2v.1.html#input-from-vmware-esxi-hypervisor)

```
virt-v2v-copy-to-local -ic esx://user@esxi1.example.com?no_verify=1 <vmname>
sudo virt-v2v -i libvirtxml <vmname>.xml -o libvirt -of qcow2
```

Then log in to kimchi, edit the new guest and
  * Remove the existing storage device
  * Add, `disk`, Select existing, `default` storage
  * Interface, remove, then add

### From OVF
Or import an ovf - which *just works*:
```
sudo virt-convert my.ovf -D qcow2
```

### Existing qcow2
```
virt-install \
        --name guest-name \   
        --memory 1024 \
        --disk /var/lib/libvirt/images/guest.qcow2 \
        --import
```

## Troubleshooting migrated VMs

[Reference](https://possiblelossofprecision.net/?p=2293)

Booting the newly created virtual machine might not work straight away, e.g. on
Fedora, RHEL and CentOS the UUID of the hard drive is included in the initial
RAM file system. The easiest way to fix this is to boot into rescue mode
(there’s usually a rescue mode entry in the grub boot menu) and run

```
dracut --regenerate-all --force
```

to recreate the initramfs. You might also have to edit the network configuration
since your network device usually gets a different name.

## Sparsify
There are a couple of disk formats: raw and qcow2. If you're using raw then
convert to qcow
```
qemu-img convert -f raw -O qcow2 guest-disk.img guest-disk-copy.qcow2
```

Otherwise just
```
virt-sparsify 
```
https://www.certdepot.net/kvm-thin-provisioning-tip/

## Change Spice to VNC
I've found spice to be terribly unreliable. Maybe it's just an old version or
that I'm using it through the kimchi web console - but VNC works better for me.
To change it for an existing VM, find the name of your VM using
`virsh list --all` then
```
virsh edit guest-name
```

Find the `<graphics type='spice' ...` attribute and change spice to vnc. You might
get some funny warnings about saving and XML validation. I just forced it through.

## Rename VM

```
virsh dumpxml machine.example.com > machine.xml
editor machine.xml
```

```xml
<domain type='kvm' id='24'>
  <name>machine-new.example.com</name>  <== edit the name here
  <uuid>cadb89df-574e-ec7e-31fe-31a33d7934f5</uuid>
```

```
virsh undefine machine.example.com
virsh define machine.xml
```

[Reference](https://www.blunix.org/renaming-virtual-machine-domain-virsh/)

## References
  * [Ubuntu KVM hypervisor setup](http://www.ubuntuboss.com/ubuntu-server-16-04-as-a-hypervisor-using-kvm-and-kimchi-for-vm-management/)
  * [Centos doesn't like migration](https://www.centos.org/forums/viewtopic.php?t=63988)
  * [Graceful shutdown](https://www.itfromallangles.com/2012/02/kvm-guests-graceful-shutdown/)
