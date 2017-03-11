# Virtualisation
As a developer I increasingly needed access to different operating
environments for testing, experimentation, learning and generally
mucking around. I'd outgrown just being able to tinker with Raspberry
Pis but at the same time wanted (needed?) to keep existing machines
running even though their hardware requirements were very modest.

I'd already bought a NUC to play with. I went for the cheapest new
one I could find and ended up with the Celeron - NUC5CPHY. I added
8gb of RAM and found an old 120gb laptop drive (which I later upgraded
to a 1gb drive)

So I eventually decided to get it running some virtual machines.

# Other places to look
These people are amazing. They are your friends:

  * http://www.virten.net/
  * https://www.v-front.de/

# Terminology
I recommend doing your own research with all this but since I struggled
to understand all the new terminology I thought I'd cover a few basic
points here.

## Hypervisor
This is essentially a thin operating system which sits underneath all
the actual virtual machines (VMs) that run. This is typically referred
to as the _host_. Baremetal is a slightly fuzzy marketing term which
as far as I can tell just means it's a bit thinner and gets the _guests_
as close to the _hosts_ hardware as possible.

## Guest
These are the virtual machines which run within the host.

# Specific vendors
The big names are:
  * VMWare (ESXi / vSphere)
  * Oracle (VirtualBox)
  * Citrix (Xen)
  * Microsoft (Hyper V)
  * KVM

And
  * Proxmox

After trying Proxmox and failing I went with VMWare because it wasn't
any of the others.

# VMWare marketing terms
Marketing is obviously too strong a division in VMWare as it's taken me
an age to work out what on earth everything does. In short:

  * ESXi is the name of the hypervisor - like a low level OS. you
    will definitely want this. It has its own web interface.
  * VMWare Player - simple free player which allows you to create
    or run VMs on your OS of choice. e.g. Windows. Great for initial
    setups of new guests
  * VMWare vCenter Converter - The easiest way to take an existing
    VM (from player) and load it into ESXi. Also great for converting
    an existing physical machine into a VM. There is only a Windows
    version of this software (but which can acticaly convert running
    Linux boxes, which is quite neat)
  * VMWare vSphere Client - now discontinued but a good piece of 
    desktop software for remote management of ESXi 
  * vSphere is marketing and exists to confuse you. I think it's their
    suite of management products and servers and stuff.
