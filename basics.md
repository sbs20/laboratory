# Arch install

* https://arch-anywhere.org/#
* http://superuser.com/questions/519784/error-installing-arch-linux
* http://superuser.com/a/1132250
* https://www.howtoforge.com/tutorial/install-arch-linux-server/#step-install-the-ssh-server

# Total basics
If you need this then you may be better off not using Arch

 * [Tutorial](http://www.ee.surrey.ac.uk/Teaching/Unix/)

# Install and remove
sudo pacman -S foobar
sudo pacman -Rs foobar

# Now install ssh server package:

    pacman -S openssh

Enable the ssh service to start automatically when the system is booting:

    systemctl enable sshd.service

# Set up NFS client
See here: https://project.altservice.com/issues/645

## Mount the NFS Share

Install nfs-utils package:

    sudo pacman -S nfs-utils

Start and enable rpcbind.service,nfs-client.target and remote-fs.target services at boot:

    sudo systemctl enable rpcbind.service
    sudo systemctl enable nfs-client.target
    sudo systemctl enable remote-fs.target

    sudo systemctl start rpcbind.service
    sudo systemctl start nfs-client.target
    sudo systemctl start remote-fs.target

# SANE
sudo pacman -S sane
scanimage -L should fail... 
sane-find-scanner should fail... need sudo
sudo scanimage -L

sudo pacman -S nodejs npm

useradd -m scanservjs
sudo usermod -G scanner scanservjs

sudo -i -u scanservjs...
copy files

sudo pacman -Syu

# Network load
    sudo pacman -S nload

# Clone disk

 * List existing partitions: `fdisk -l /dev/sda`
 * Clone from sdX to sdY: `sudo dd if=/dev/sdX of=/dev/sdY bs=64K conv=noerror,sync status=progress`
 * Clonezilla: http://clonezilla.org/fine-print-live-doc.php?path=./clonezilla-live/doc/03_Disk_to_disk_clone/00-prepare-clonezilla-live.doc#00-prepare-clonezilla-live.doc
   use k1 option

# Time
Use network time
`sudo timedatectl set-ntp true`
`timedatectl status`

# github
```
sudo pacman -S git
cd ~
mkdir development
cd development
git clone https://github.com/sbs20/pi-recipes.git
cd pi-recipes
nano README.md
git status
git add . # or specific files
git commit -m "Updated README"
git push origin master
```

You'll be prompted for credentials. If you have 2FA enabled then
[see here](http://stackoverflow.com/a/40166682/1229065)

# Bluetooth audio
https://wiki.archlinux.org/index.php/Bluetooth_headset
