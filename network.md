# Network interface stuff
https://wiki.archlinux.org/index.php/Network_configuration
https://wiki.archlinux.org/index.php/software_access_point
https://wiki.archlinux.org/index.php/Network_bridge
 -> https://wiki.archlinux.org/index.php/Bridge_with_netctl

sudo pacman -S netctl
sudo pacman -S iw
Show adapters `ip addr`
Bringing interfaces up and down `ip link set <interface> up/down`

ip link add name br0 type bridge

