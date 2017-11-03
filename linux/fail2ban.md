# fail2ban
Install fail2ban. Institutes a firewall block if `x` fails occur in `y`
seconds. This is well worth it. Even with private key authentication and
a hidden port, some twat will keep trying. I configured 5 bad attempts in
60 seconds for a 15 minute ban.

```
sudo apt-get install fail2ban
cd /etc/fail2ban
sudo nano jail.local
```
Change: `ignoreip`, `bantime` and `maxretry`

e.g.
```
# GLOBALS
[DEFAULTS]
bantime  = 3600
findtime  = 3600
maxretry = 2

# JAILS
#; sshd is already enabled by default

[recidive]
enabled = true
```

Monitor current rules: `sudo iptables -L`

## References
[fail2ban](https://www.digitalocean.com/community/tutorials/how-to-protect-ssh-with-fail2ban-on-debian-7)

