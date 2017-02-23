# git

```
sudo pacman -S git
cd ~
mkdir development
cd development
git clone https://github.com/sbs20/pi-recipes.git
cd pi-recipes
nano README.md
git status
git add . # or specific files
git commit -m "Updated README"
git push origin master
```

You'll be prompted for credentials. If you have 2FA enabled then
[see here](http://stackoverflow.com/a/40166682/1229065)
