# KVM

## Install
```
sudo apt install kvm
```

Then install [kimchi](https://github.com/kimchi-project/kimchi/releases/latest)

But you have to do things in a particular way...
```
sudo apt install nginx
sudo dpkg -i <wok.deb>
sudo apt-get install -f
sudo service wokd start
sudo reboot now

sudo dpkg -i kimchi-2.5.0-0.noarch.deb
sudo apt-get install -f
sudo reboot now
```

Then navigate to https://<address>:8001

## Installing within ESXi
It looks like some brave souls have done this - but KVM doesn't like it. I gave
up after a few hours.

## Migrating VMs
See [virt-v2v](http://libguestfs.org/virt-v2v.1.html)

If you are copying from ESXi and have a new version of virt-v2v (1.37+) then
you can copy direct from the disk

```
virt-v2v -i vmx -it ssh "ssh://user@esxi1.exmaple.com/vmfs/volumes/datastore1/<vmname>/<vmanem>.vmx" -o local -os ~/
```

[Otherwise you need to:](http://libguestfs.org/virt-v2v.1.html#input-from-vmware-esxi-hypervisor)

```
virt-v2v-copy-to-local -ic esx://user@esxi1.example.com?no_verify=1 <vmname>
virt-v2v -i disk <vmname>.vmx -o local -os /var/tmp/
```
