# Total basics
[Tutorial](http://www.ee.surrey.ac.uk/Teaching/Unix/)

# Packages
This documentation refers interchangebly between the various
linux package managers, `yum`, `apt-get` and `pacman` according
to which system I was using at the time. While bigger packages
tend to have consistent names across distros this isn't always
true... and certainly not for the smaller packages. Google will
be your friend.

# Time
Show now
```
date
```

Use network time
`sudo timedatectl set-ntp true`
`timedatectl status`

# Changing the hostname
You need to edit two files

    sudo nano /etc/hostname

replace `current-host-name` with your new device name

In order to avoid "sudo: unable to resolve host" errors you will also need to edit your hosts file:

    sudo nano /etc/hosts

and then replace the following line
    127.0.1.1	`current-host-name`

# Update password
Your own: `passwd`

Someone else's: `passwd <their-username>`

# My favourite prompt

Add this to .bashrc

```
export PS1='\[\e]0;\u@\h: \w\a\]\[\e[94m\][\[\e[92m\]\u\[\e[94m\] @ \[\e[1;97m\]\h\[\e[21;94m\]]: \[\e[93m\]\w\[\e[94m\]>\[\e[92m\]\$\[\e[0m\] '
```


or
```
export PS1='\[\e]0;\u@\h: \w\a\]\[\033[38;5;12m\][\[\]\[\033[38;5;10m\]\u\[\]\[\033[38;5;12m\]@\[\]\[\033[38;5;7m\]\h\[\]\[\033[38;5;12m\]]\[\]\[\033[38;5;15m\]: \[\]\[\033[93m\]\w\[\]\[\033[38;5;12m\]>\[\]\[\033[38;5;10m\]\$\[\]\[\033[38;5;15m\]\033[0m\[\] '

export PS1='\[\e]0;\u@\h: \w\a\]\[\e[94m\][\[\]\[\e[92m\]\u\[\]\[\e[94m\]@\[\]\[\e[1;97m\]\h\[\]\[\e[21;94m\]]\[\]: \[\]\[\e[93m\]\w\[\]\[\e[94m\]>\[\]\[\e[92m\]\$\[\]\e[0m\[\] '
```

Then `source ~/.bashrc`

[Reference](http://misc.flogisoft.com/bash/tip_colors_and_formatting)
