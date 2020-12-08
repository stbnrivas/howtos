# tmux

a multiplexor of terminals that use process client-server

## advantages

- restore sessions for example a network error
- arrange terminals
- change of environment


## concepts

- session (a collection of windows managed by tmux one session. a session is full screen divided by panels)
- window (its a fullscreen and can devide by single or multiples panels)
- panel (every panel is a bash session terminal)


## configuration

```
# see config
tmux show -g

# you could create a ~/.tmux.conf with the default settings
tmux show -g | cat > ~/.tmux.conf


# history file to save commands
set -g history-file ~/.tmux_history
```

- problem missing commands to history solve by adding to `~/.bashrc`

```bash
# Avoid duplicates
export HISTCONTROL=ignoredups:erasedups
# When the shell exits, append to the history file instead of overwriting it
shopt -s histappend
# After each command, append to the history file and reread it
export PROMPT_COMMAND="${PROMPT_COMMAND:+$PROMPT_COMMAND$'\n'}history -a; history -c; history -r"
```


## running tmux

```bash
tmux
tmux list-sessions
tmux attach-session -t $session_name

tmux kill-pane
tmux kill-session
tmux kill-window

```


## prefix of command

```bash
# prefix of command
# ctrl + B + command

# example
# ctrl+b : detach

#ctrl + E
#ctrl + 1
#ctrl + 2

```

```bash
# create a session
# ctrl + B + : new

tmux list-sessions
#0: 1 windows (created Wed Jul  3 12:18:26 2019) [118x58] (attached)
tmux ls
tmux attach -t --target 0

```

```bash
#rename session
# CTRL+D $

# change between sessions
# CTRL+B (          previous session
# CTRL+B )          next session
# CTRL+B L          ‘last’ (previously used) session
# CTRL+B s          choose a session from a list



CTRL+B : kill-session

# rename a window
CTRL+B ,

# create a new window
CTRL+B c
CTRL+B p  # previous
CTRL+B n  # next
CTRL+B [0-9]  # go to X window
CTRL+B &  # close windows


```





panels

```bash
# scroll into window
# ctrl + b [
# q to exit
```


divide a panel horizontally

ctrl + b + "

divide a panel vertical

ctrl + b + %

switch between panels with

ctrl + b + ↑
ctrl + b + →
ctrl + b + ←
ctrl + b + ↓

close panel

ctrl + b x


swith between 5 layout

ctrl + b  "space"

even horizontal
even vertical
main horizontal
main vertical
tiled


modo copia

ctrl + b + [
q







## Sharing a read-only tmux session

* Start it with
```
./ttyd -R tmux new -A -s ttyd bash
```
* Join it with
```
tmux new -A -s ttyd
```
* Share with public ip
```
ssh -R 80:localhost:7681 ssh.localhost.run
```