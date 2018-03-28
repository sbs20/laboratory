# sshfs

Mount a remote filesystem with ssh.

```
sudo apt install sshfs
```

Then tou can put something like this in `~/.profile`:
```
# Mount drive
if [ "$(mount | grep ' /home/user/data')" = "" ]; then
    sshfs -o follow_symlinks,no_check_root me@server.example.com:data $HOME/data
fi
```