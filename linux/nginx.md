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
