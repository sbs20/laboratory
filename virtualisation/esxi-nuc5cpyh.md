# Installing ESXi on a NUC5CPYH

VMWare does not support this machine out of the box. Thankfully
there are a lot of clever and dedicated enthusiasts who are here
to help.

## Overview
  * You need to create a custom ISO install with additional NIC
    and SATA drivers
  * Even then you won't be able to run the install on the NUC
    itself because VMWare pukes at the video controller
  * Pull your HDD out of the NUC, connect it to a host machine
    (it was a laptop in my case) using a USB SATA connection
  * Create a new VM in VMPlayer using your custom ESXi ISO and
    install ESXi onto the SATA disk by directly connecting the
    USB SATA drive *to the VM*
  * Unplug the SATA drive, put in the NUC and boot

## Custom ISO  
Download script from here: https://www.v-front.de/p/esxi-customizer-ps.html#download
Install VMWare PowerCLI

Run
`.\Scripts\ESXi-Customizer-PS-v2.5.ps1 -v60 -vft-load sata-xahci,net55-r8168 -outDir c:\Users\YOUR_PROFILE\`

_TODO_

## What if I don't want to do all that?
You'll get errors all over the place
503 Service Unavailable (Failed to connect to endpoint: [N7Vmacore4Http16LocalServiceSpecE:0x1f075f20] _serverNamespace = / _isRedirect = false _port = 8309)
Found this: https://kb.vmware.com/selfservice/microsites/search.do?language=en_US&cmd=displayKC&externalId=2121043


http://www.howtogeek.com/97923/how-to-boot-a-vmware-virtual-machine-from-a-usb-drive/

