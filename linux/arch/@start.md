# Arch install

* https://arch-anywhere.org/#
* http://superuser.com/questions/519784/error-installing-arch-linux
* http://superuser.com/a/1132250
* https://www.howtoforge.com/tutorial/install-arch-linux-server/#step-install-the-ssh-server

# Now install ssh server package:

`pacman -S openssh`

Enable the ssh service to start automatically when the system is booting:

`systemctl enable sshd.service`

# Install and remove
`sudo pacman -S foobar`
`sudo pacman -Rs foobar`
`sudo pacman -Syu`


