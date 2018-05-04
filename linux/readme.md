# Total basics
[Tutorial](http://www.ee.surrey.ac.uk/Teaching/Unix/)

# Packages
This documentation refers interchangebly between the various linux package
managers, `yum`, `apt-get` / `apt` and `pacman` according to which system I was
using at the time. While bigger packages tend to have consistent names across
distros this isn't always true... and certainly not for the smaller packages.
Google will be your friend.

# Sudo not found
See [here for reference](https://www.cyberciti.biz/faq/debian-ubuntu-rhel-centos-linux-bash-sudo-command-not-found/)

Change to root and install sudo e.g.

```
su - root
apt-get install sudo
```

Add your user to the sudo group
```
usermod -aG sudo username
``` 

Log out and back in again

# Time
Show now
```
date
```

Use network time
`sudo timedatectl set-ntp true`
`timedatectl status`

# Update password
Your own: `passwd`

Someone else's: `passwd <their-username>`

# My favourite prompt

Add this to .bashrc

```
if [ -f "$HOME/.prompt" ]; then
    . "$HOME/.prompt"
fi
```

Then add this to `$HOME/.prompt`:
```
title='\[\e]0;\u@\h: \w\a\]'
bo='\[\e[96m\]['
bc='\[\e[21;96m\]]'
user='\[\e[92m\]\u'
at='\[\e[96m\]@'
host='\[\e[1;97m\]\h'
path='\[\e[93m\]\w'
arrow='\[\e[96m\]>'
bang='\[\e[92m\]\$'
clear='\[\e[0m\]'

prompt="${title}${bo}${user} ${at} ${host}${bc}: ${path}${arrow} ${bang} ${clear}"
#echo $prompt

PS1=${prompt}
```

Then `source ~/.bashrc`

[Reference](http://misc.flogisoft.com/bash/tip_colors_and_formatting)

# You have mail
Use the `mail` command. Tutorial [here](http://www.johnkerl.org/doc/mail-how-to.html).
But to delete all: `d*` then `q` to quit.
