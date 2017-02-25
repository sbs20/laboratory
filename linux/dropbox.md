# Dropbox
http://www.dropboxwiki.com/tips-and-tricks/using-the-official-dropbox-command-line-interface-cli

```
sudo pacman -S python2
sudo nano /bin/dropbox.py
```

You may need to edit dropbox.py and repoint at python2

## Error: echo fs.inotify.max_user_watches=100000

If you get this error then
[see here](http://stackoverflow.com/questions/35711897/dropbox-fs-inotify-error)
to know more.

echo fs.inotify.max_user_watches=131072 | sudo tee -a /usr/lib/sysctl.d/50-default.conf; sudo sysctl -p

## Arch linux....
https://wiki.archlinux.org/index.php/dropbox#Starting_on_boot_with_systemd
https://github.com/joeroback/dropbox/blob/master/dropbox%40.service



## Create a link in the Dropbox folder 
Just because this is possible doesn't mean it should be done

    ln -s /mnt/public ~/Dropbox/Test

