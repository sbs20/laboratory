# Find and wc
List all files `find . -type f`
Count all files `find Dropbox/ -type f | wc -l`

# sed
http://www.grymoire.com/Unix/Sed.html

## Rename files in directories using sed
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

## As grep
sed -n "/PATTERN/p"

## Remove
cat domains.txt | sed -n "1,20s/^\t\t//p" | sed -n "s/\t.*/\t192.168.0.1/p"
