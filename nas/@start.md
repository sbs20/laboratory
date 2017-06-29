# NAS

You can buy ready made NAS devices which are supported and updated. I have used QNAP devices for years (since 2007) and have always been happy with them. I had begun to find, though, that the firmware (QTS) for the devices was being end-of-lifed; no new feature updates. I understand this from a commercial perspective but dislike it from a consumer perspective.

Instead I bought my own hardware - an [HP ProLiant Microserver Gen 8](https://www.hpe.com/uk/en/product-catalog/servers/proliant-servers/pip.hpe-proliant-microserver-gen8.5379860.html) and decided to install firmware myself. [Mondaiji says it well here](http://www.mondaiji.com/blog/other/it/10210-the-hunt-for-the-ultimate-free-open-source-nas-distro). 

## NAS firmware I looked at
* [Rockstor](http://rockstor.com/): CentOS based. Free but with suggestions to upgrade to paid. [More](http://opensourceforu.com/2016/01/rockstor-the-rockstar-among-nas-solutions/)
* [openmediavault](http://www.openmediavault.org/): Fork of FreeNAS on to Debian (rather than FreeBSD). Will even run on a Raspberry Pi
* [FreeNAS](http://www.freenas.org/): Seems to be "the" one to have. BSD based, with ZFS - appears to have greater hardware needs
* [Nas4free](https://www.nas4free.org/): FreeBSD fork of FreeNAS

## What I chose
openmediavault. I didn't need ZFS. I know and like debian. It has good heritage. I should add that I didn't actually install anything else in my evaluation - I just looked at other people's reviews

## NAS Manufacturers to consider
* [QNAP](https://www.qnap.com/)
* [Synology](https://www.synology.com)
* [Thecus](http://www.thecus.com/)
* [Netgear](https://www.netgear.com/business/products/storage/)
