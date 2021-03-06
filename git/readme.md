# Git

## Basics
```
# Clone a repo
git clone https://github.com/sbs20/pi-recipes.git

# Change dir and edit a file
cd pi-recipes
nano README.md

# See status
git status

# Stage the changes
git add . # or specific files

# Commit
git commit -m "Updated README"

# Or as different user
git commit -m "Updated README" --author="sbs20 <you@domain.com>"

# Sync
git push origin master
```

## 2FA
You'll be prompted for credentials. If you have 2FA enabled then
[see here](http://stackoverflow.com/a/40166682/1229065)

## Undo commit
```
git reset HEAD~
```

  * [Undo last commit](https://stackoverflow.com/questions/927358/how-do-i-undo-the-last-commits-in-git)
  * [How to undo more or less anything](https://blog.github.com/2015-06-08-how-to-undo-almost-anything-with-git/)
  * [Delete local branch and get from server](https://stackoverflow.com/a/9210786)

## Switch remote repo
```
# If it's the same repo
git remote set-url origin https://example.com/repo.git

# Alternatively
git remote rm origin
git remote add origin https://example.com/repo.git
```

## Merging two repositories

It's possible to do this and maintain version history. However,
the remote repo that you're copying will end up in the root of
the local one. So be careful of name collisions which cause git
grief.

http://stackoverflow.com/questions/13040958/merge-two-git-repositories-without-breaking-file-history/

## Migrating from SVN
http://stackoverflow.com/questions/79165/how-to-migrate-svn-repository-with-history-to-a-new-git-repository
