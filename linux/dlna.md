# DLNA

## Server
Install minidlna (new name is ReadyMedia)

```
sudo apt install minidlna
sudo systemctl enable minidlna
```

Decide what files you want to share. Make them available locally somehow - e.g.
mount via NFS or whatever then edit `/etc/minidlna.conf` accordingly e.g.

```
media_dir=V,/media/Film
media_dir=V,/media/Television
friendly_name=MyNewDLNAServer
```

The database is stored in `/var/cache/minidlna/files.db`.

To rebuild the datbase:
```
sudo minidlnad -R
sudo systemctl restart minidlna
```

## Console Client
Use `djmount`.

```
sudo apt install djmount
sudo modprobe fuse
sudo mkdir -p /media/upnp

# Mount
sudo djmount -o allow_other /media/upnp

# Unmount
sudo fusermount -u /media/upnp
```
