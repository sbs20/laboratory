# Use SSH keys for authentication

## Steps
Create the keys on your favourite client
`ssh-keygen`

Copy the public keys to a remote server
`ssh-copy-id user@remotehost.com`

## Disable passwords
Make sure you have tested SSH keys first!

Disable password authentication for SSH on the remote server
`sudo nano /etc/ssh/sshd_config`

Find
`#PasswordAuthentication yes`

Remove # and change yes to no...
`PasswordAuthentication no`

Restart SSH:

Debian: `sudo service ssh restart`
CentOS: `sudo service sshd restart`
Arch:   `sudo systemctl restart sshd`

## Bad IP address / hosts
If you've changed the IP address of a host and you have the incorrect known_host then:
```
ssh-keygen -R host-or-ip
```

## References
https://www.digitalocean.com/community/tutorials/how-to-configure-ssh-key-based-authentication-on-a-linux-server

http://stackoverflow.com/questions/3818886/how-do-i-add-a-password-to-an-openssh-private-key-that-was-generated-without-a-p
