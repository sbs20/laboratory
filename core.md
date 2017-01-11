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

## As grep
sed -n "/PATTERN/p"
