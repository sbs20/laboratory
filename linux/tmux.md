## tmux
Install and run [tmux](https://github.com/tmux/tmux/wiki) so that you can 
reconnect if you get cut off. [Good primer](https://robots.thoughtbot.com/a-tmux-crash-course) 

Prefix is usually `ctrl-b`
```
tmux new -s session_name
tmux attach -t session_name
tmux switch -t session_name
tmux list-sessions
tmux detach (prefix + d)
tmux new-window (prefix + c)
tmux select-window -t :0-9 (prefix + 0-9)
tmux rename-window (prefix + ,)
```
