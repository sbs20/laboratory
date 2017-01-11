# sed
http://www.grymoire.com/Unix/Sed.html

# Rename files in directories using sed
[This is useful](http://unix.stackexchange.com/a/162121)

`find . -type f | sed "s:\(.*/\)\([^/]*\):mv \1\2 \1new_\2:" | sh`

## List files
`find . -type f`

## And pipe to sed
`sed "s:\(.*/\)\([^/]*\):mv \1\2 \1new_\2:"`

Use `:` delimiter

`substitute:` s
`find:` \(.*/\)\([^/]*\)
    `match1:` \(.*/\)
    `match2:` \([^/]*\)
`replace:` mv \1\2 \1new_\2:

## And pipe to sh to execute
`sh`

# Terminal image viewer
`sudo pacman -S libcaca`

Ref: http://superuser.com/a/378787

`cacaview myimage.jpg`

`sudo pacman -S mplayer`

# 7zip
    sudo pacman -S p7zip
    
    # Create archive
    7z a archive.7z *

    # No compression
    7z a -mx0 archive.7z *

    # Extract
    7z e archive.7z ./

