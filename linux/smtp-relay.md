# Postfix
_Reference source_: [Linode: Configure Postfix to Send GMail](https://www.linode.com/docs/email/postfix/configure-postfix-to-send-mail-using-gmail-and-google-apps-on-debian-or-ubuntu)

Postfix is a network SMTP MTA (relay) daemon. You can therefore use it to
relay email from various other devices in your network.

## Install
`sudo apt-get install postfix`
Choose `2) Internet site`
Enter your local domain `example.com`

## Add your username and password
* `sudo nano /etc/postfix/sasl/sasl_passwd`
* Add `[smtp.gmail.com]:587 username@gmail.com:password` and save
* Run `sudo postmap /etc/postfix/sasl/sasl_passwd`

## Secure passwords
```
sudo chown root:root /etc/postfix/sasl/sasl_passwd /etc/postfix/sasl/sasl_passwd.db
sudo chmod 0600 /etc/postfix/sasl/sasl_passwd /etc/postfix/sasl/sasl_passwd.db
```

## Configure: `/etc/postfix/main.cf`
```
# CUSTOM SETTINGS HERE
# sets gmail as relay
relayhost = [smtp.gmail.com]:587

#  use tls
smtp_use_tls=yes

# Enable SASL authentication
smtp_sasl_auth_enable = yes

# Disallow methods that allow anonymous authentication
smtp_sasl_security_options = noanonymous

# Location of sasl_passwd
smtp_sasl_password_maps = hash:/etc/postfix/sasl/sasl_passwd

# Enable STARTTLS encryption
smtp_tls_security_level = encrypt

# Location of CA certificates
smtp_tls_CAfile = /etc/ssl/certs/ca-certificates.crt
```

_If you want to allow messages to be sent from your local network or specific
machines then you need to update `$mynetworks`

```
mynetworks = 127.0.0.0/8 [::ffff:127.0.0.0]/104 [::1]/128 192.168.0.3
```

## Aliasing (forwarding)
Add the following to `main.cf`
```
# Enable aliasing (overrides "alias_maps")
virtual_alias_domains = mydomain.com
virtual_alias_maps = hash:/etc/postfix/virtual
```

Now add `/etc/postfix/virtual`
```
# "Address you want to forward"   "Address to forward to"
@example.com     me@gmail.com
```

You now have to build the virtual.db `sudo postmap /etc/postfix/virtual` then
restart postfix

## Debug
```
sudo tail -f /var/log/syslog
```

# SSMTP
Use ssmtp to send an email to a relay. It is not a daemon.

## Install
* Install e.g. `sudo apt-get install ssmtp mailutils`
* Configure `sudo nano /etc/ssmtp/ssmtp.conf`

## ssmtp.conf for gmail
```
# The full hostname
hostname=device.example.com

# Your email address
AuthUser=yourname@gmail.com

# Password - if you have 2FA then app-specific password
AuthPass=yourpassword
FromLineOverride=YES
mailhub=smtp.gmail.com:587
UseSTARTTLS=YES
```

## ssmtp.conf for local postfix
```
# The full hostname
hostname=device.example.com
mailhub=postfix-server.example.com
```

## Test
`echo "Test text" | mail -s "Test Mail" me2@gmail.com`
