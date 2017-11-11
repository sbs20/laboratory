# Creating a TLS reverse proxy

Want to secure a Kodi HTTP service? with TLS? Nginx.

nginx fails on boot because of host not found upstream...

```
Oct 08 22:52:32 pi nginx[582]: nginx: [emerg] host not found in upstream "host.example.com" in /etc/nginx/sites-enabled/sb...
Oct 08 22:52:32 pi nginx[582]: nginx: configuration file /etc/nginx/nginx.conf test failed
Oct 08 22:52:32 pi systemd[1]: nginx.service: Control process exited, code=exited status=1
Oct 08 22:52:32 pi systemd[1]: Failed to start A high performance web server and a reverse proxy server.
```

You need to start nginx after your DNS service?

```
sudo nano /lib/systemd/system/nginx.service
```

Then
```
[Unit]
After=... dnsmasq.service
```

[Reference](https://serverfault.com/a/482760/428070)

# Kodi behind a proxy
[See here](https://github.com/xbmc/chorus2/issues/133)

# Getting PHP working
```
sudo apt install php
```

Edit `/etc/nginx/sites-available/your_site.conf` and add:

```
    location ~ \.php$ {
        fastcgi_split_path_info ^(.+\.php)(/.+)$;
        # You may need to alter the following line according to your install
        fastcgi_pass unix:/var/run/php/php7.0-fpm.sock;
        fastcgi_index index.php;
        include fastcgi_params;
        fastcgi_param SCRIPT_FILENAME $document_root/$fastcgi_script_name;
    }
```
Then restart nginx

[Reference](https://askubuntu.com/a/134676)

## Emailing with SSMTP
Edit `/etc/php/7.0/fpm/php.ini` and set `sendmail_path = /usr/sbin/ssmtp -t`.
You may need to restart php `sudo systemctl restart php7.0-fpm.service`. Then
test: `php -r "mail('email@gmail.com', 'hello', 'hello from php');"`.

