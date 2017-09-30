# Installation

There are plenty of resources available to install ESXi. I had some
difficulties with my low-end celeron NUC. If you're interested in
how I got that going then [see here](esxi-nuc5cpyh.md).

# Initial set up
Navigate to the vSphere web-app ...

    https://<host-ip>/ui

# Set hostname:
From https://kb.vmware.com/selfservice/microsites/search.do?language=en_US&cmd=displayKC&externalId=1010821
`esxcli system hostname set --host=hostname`

# Install vSphere Client
VMWare is trying to push its web app for ESXi management. I think this is
ultimately a good thing. However, there are still some shortcomings with the
web interface so it can be useful to have the native Windows client.

Get it here:
https://kb.vmware.com/selfservice/microsites/search.do?language=en_US&cmd=displayKC&externalId=2089791

# Missing NTP servers
[See here](https://communities.vmware.com/thread/505146?tstart=0) for more
details but in short connect using the vSphere client:

Host > Configuration > Time configuration > General > Options... > NTP Settings

Add these three servers:

0.it.pool.ntp.org
1.it.pool.ntp.org
2.it.pool.ntp.org

# Restart services

SSH in and `services.sh restart`
[See here](https://serverfault.com/questions/196928/cant-connect-to-esxi-with-vsphere-client)
