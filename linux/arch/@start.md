# Arch install
Arch prides itself on not being easy to install. On the one hand I
think this is funny and part of the whole hacker culture. On the other
I just think it's stupid and exclusive. A bit like an operating system
entry to the Darwin awards. Yeah let's make an OS which no one can be
arsed to install but which is like really pure and shit.

I guess it depends on whether you think Open Source should be a force
for good: driving competition, sharing and non-proprietory standards; which
in turn sort of implies that the way to achieve that is through
accessibility for the masses. Or whether you just want to be apart from
all those sheep who suck at the evil teat of M$ etc.

The thing is, I like Arch. I like that it's always new and there's no
version. I like a lot of the culture. That it's lean and mean - my install
flies along on a single core Celeron VM with 512mb!. I just wish it learned
to love itself and make itself more likeable.

* https://arch-anywhere.org/#
* http://superuser.com/questions/519784/error-installing-arch-linux
* http://superuser.com/a/1132250
* https://www.howtoforge.com/tutorial/install-arch-linux-server/#step-install-the-ssh-server

# Packages
install foobar: `sudo pacman -S foobar`
Remove foobar: `sudo pacman -Rs foobar`
Update all: `sudo pacman -Syu`
Purge unused: `sudo pacman -Sc`

# Now install ssh server package:

`pacman -S openssh`

Enable the ssh service to start automatically when the system is booting:

`systemctl enable sshd.service`
