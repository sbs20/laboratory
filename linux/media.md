# Media

## Terminal image viewer
Arch: `sudo pacman -S libcaca`
Debian: `sudo apt-get install caca-utils`
Ref: http://superuser.com/a/378787

`cacaview myimage.jpg`

## Bluetooth audio
https://wiki.archlinux.org/index.php/Bluetooth_headset

## Handbrake
```
sudo apt-get install handbrake handbrake-cli
```
Then
```
HandBrakeCLI -i VIDEO_TS -o movie.mp4 -e x264 -q 20 -B 160
HandBrakeCLI -i input.ts -o movie.mkv -e x264 -q 20 -E copy:*
```

## ffmpeg
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
