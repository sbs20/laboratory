# Running WSL SSHD on Windows 10 with Ubuntu 18.04 LTS

## Configure WSL
```
sudo apt remove openssh-server
sudo apt install openssh-server
sudo sed -i "$ a $USER ALL=(root) NOPASSWD: /etc/init.d/ssh" /etc/sudoers
sudo service ssh start
```

This reinstalled SSHD, updates sudoers so that you don't need to use a password
to start it and then starts it.

Try SSHing in to see if it works.

## Open your firewall
**CAUTION**: This should be fine on a home network, but please understand what
you're doing here.

  1. Run: Windows Defender Firewall with Advanced Security
  1. Create "New Rule": Allow port 22 and call it `sshd`

## Create a script and task to start bash
Create `sshd.cmd` in a location of your choosing e.g. `%USERPROFILE%\sshd.cmd`
and add the following
```
C:\Windows\System32\bash.exe -c "sudo /etc/init.d/ssh start"
```

Run `sshd.cmd` to check it works. (You may need to kill previous instances of 
`bash.exe` which are already running)

Then create a scheduled task in `Task Scheduler` which points to `sshd.cmd` and
runs on boot.

## Final thoughts
Consider updating SSHD to disallow passwords and use keys instead.

[Reference](https://gist.github.com/harleyday/76a103a1a0ca97c6f33706e4a8cc3307)

## Other notes
  * https://superuser.com/questions/1112007/how-to-run-ubuntu-service-on-windows-at-startup
