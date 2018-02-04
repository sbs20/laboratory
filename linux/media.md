# Media

## Terminal image viewer
Arch: `sudo pacman -S libcaca`
Debian: `sudo apt-get install caca-utils`
Ref: http://superuser.com/a/378787

`cacaview myimage.jpg`

## Exiftool
[See here for more info](https://www.sno.phy.queensu.ca/~phil/exiftool/index.html)

Download

    cd <your download directory>
    wget https://www.sno.phy.queensu.ca/~phil/exiftool/Image-ExifTool-10.78.tar.gz
    tar -xf Image-ExifTool-10.78.tar.gz
    cd Image-ExifTool-10.78

Rewrite filenames based on exif date

    exiftool "-FileName<CreateDate" -d "%Y%m%d_%H%M%S.%%e" <YOUR_PHOTO_DIR>


## Bluetooth audio
https://wiki.archlinux.org/index.php/Bluetooth_headset

## Handbrake
```
sudo apt-get install handbrake handbrake-cli
```
Then
```
HandBrakeCLI -i VIDEO_TS -o movie.mp4 -e x264 -q 20 -B 160
HandBrakeCLI -i input.ts -o output.mp4 --decomb -e x264 -q 20 -E copy --stop-at duration:20
```

Or batch...
```
find . -name "*.ts" -exec HandBrakeCLI -i {} -o {}.mp4 --decomb -e x264 -q 20 -E copy \;
```

## ffmpeg
Or just use ffmpeg. Multi process files...
```
find . -name "*.dvr-ms" -exec ffmpeg -i {} -c:a copy -c:v copy -f dvd "{}.mpg" \;
```

Snip files
```
ffmpeg -ss 00:00:30.0 -i input.wmv -c copy -t 00:00:10.0 output.wmv
ffmpeg -ss 30 -t 10 -i input.wmv -c copy output.wmv
```
[From here](https://superuser.com/a/141343/682739)

De-interlace
```
ffmpeg -i file.mpg -crf 23 -c:a aac -vf yadif "file.mkv"
```

[Useful reference](https://superuser.com/a/550764/682739)