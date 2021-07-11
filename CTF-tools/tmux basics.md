# Tmux

This is the tmux basics memo that I have created for myself. 

Nothing Extensive or Hard.

Just a memo.

## config file
```~./tmux.conf```

## prefix change

```ctrl + b``` change to ```ctrl + a``` 

## Horizontal and Vertical split change

vertical split ```|```

horizontal split ```-```

## commands
```tmux ls``` for seeing sessions

```prefix + c``` for creating a new window.

```prefix + number``` to switch windows.

```prefix + ,``` to change window name.

```prefix + d``` to detach session. 

```tmux attach -t``` number to attach session.

```tmux rename-session -t number <name>``` to rename session.

```tmux new -s <name>``` to create session with custom name from the first time.

```tmux kill-session -t <name>``` to kill the session.

```hold prefix + arrow``` to resize the pane.

```prefix + [``` to go copy mode. type q to quit out of it. 
