# Nano colour coding
See here: http://worklog.kevinclarke.info/2014/09/25/color-coding-in-nano/

Summary:

 * Look around here `/usr/share/doc/nano/examples/nanorc.sample`
 * Copy the file to `~/.nanorc`
 * edit `.nanorc`

To add JSON, add this to `.nanorc`

    ## JSON-type files
    include "/usr/share/nano/json.nanorc"

Then put this in that file

syntax "json" "\.json$"
header "^\{$"

    color blue   "\<[-]?[1-9][0-9]*([Ee][+-]?[0-9]+)?\>"  "\<[-]?[0](\.[0-9]+)?\>"
    color cyan  "\<null\>"
    color brightcyan "\<(true|false)\>"
    color yellow ""(\\.|[^"])*"|'(\\.|[^'])*'"
    color brightyellow "\"(\\"|[^"])*\"[[:space:]]*:"  "'(\'|[^'])*'[[:space:]]*:"
    color magenta   "\\u[0-9a-fA-F]{4}|\\[bfnrt'"/\\]"
    color ,green "[[:space:]]+$"
    color ,red "    +"


# Terminal image viewer
Arch: `sudo pacman -S libcaca`
Debian: `sudo apt-get install caca-utils`
Ref: http://superuser.com/a/378787

`cacaview myimage.jpg`

# 7zip
```
sudo pacman -S p7zip

# Create archive
7z a archive.7z *

# No compression
7z a -mx0 archive.7z *

# Extract
7z e archive.7z ./
```

# Network load
`sudo pacman -S nload`

# Network scan
```
sudo apt-get install nmap
nmap -sn 192.168.0.0/24
sudo nmap -sU -p 137,5353 --script nbstat,dns-service-discovery 192.168.0.0/24
```

# Torrent
From: https://askubuntu.com/a/683468

```
sudo apt-get install deluge deluged deluge-console
deluged
deluge-console
```
You can then add torrents like:

```
add -p /user/Downloads your.torrent
```

# Bluetooth audio
https://wiki.archlinux.org/index.php/Bluetooth_headset

# Handbrake
```
sudo apt-get install handbrake handbrake-cli
```
Then
```
HandBrakeCLI -i VIDEO_TS -o movie.mp4 -e x264 -q 20 -B 160
HandBrakeCLI -i input.ts -o movie.mkv -e x264 -q 20 -E copy:*
```

# FFMpeg
Or just  use ffmpeg. Multi process files...
```
find . -name "*.dvr-ms" -exec ffmpeg -i {} -c:a copy -c:v copy -f dvd "{}.mpg" \;
```

Snip files
```
ffmpeg -ss 00:00:30.0 -i input.wmv -c copy -t 00:00:10.0 output.wmv
ffmpeg -ss 30 -i input.wmv -c copy -t 10 output.wmv
```
[From here](https://superuser.com/a/141343/682739)

Encode
```
ffmpeg -i file.mpg -ss 00:02:25.0 -t 60 -crf 23 -c:a aac "file.mkv"
```
