---
title: Tmux
layout: default
nav_order: 1
parent: Essential Tools

---

# Tmux
## **<ins>Tmux Installation</ins>**
`tmux` conf that allows for copy/pasting and other convenient options within Tmux 

1. Install `tmux`
```bash
sudo apt install tmux -y
```

2. Create a `~/.tmux.conf` file
```bash
touch ~/.tmux.conf
```

3. Source the newly created tmux conf file
```bash
source ~/.tmux.conf
```

## **<ins>Tmux configuration file</ins>**
```bash
# Linux only
set -g mouse on
bind -n WheelUpPane if-shell -F -t = "#{mouse_any_flag}" "send-keys -M" "if -Ft= '#{pane_in_mode}' 'send-keys -M' 'select-pane -t=; copy-mode -e; send-keys -M'"
bind -n WheelDownPane select-pane -t= \; send-keys -M
bind -n C-WheelUpPane select-pane -t= \; copy-mode -e \; send-keys -M
bind -T copy-mode-vi    C-WheelUpPane   send-keys -X halfpage-up
bind -T copy-mode-vi    C-WheelDownPane send-keys -X halfpage-down
bind -T copy-mode-emacs C-WheelUpPane   send-keys -X halfpage-up
bind -T copy-mode-emacs C-WheelDownPane send-keys -X halfpage-down

# To copy, left click and drag to highlight text in yellow, 
# once you release left click yellow text will disappear and will automatically be available in clibboard
# # Use vim keybindings in copy mode
setw -g mode-keys vi
# Update default binding of `Enter` to also use copy-pipe
unbind -T copy-mode-vi Enter
bind-key -T copy-mode-vi Enter send-keys -X copy-pipe-and-cancel "xclip -selection c"
bind-key -T copy-mode-vi MouseDragEnd1Pane send-keys -X copy-pipe-and-cancel "xclip -in -selection clipboard"
set-option -g default-shell /bin/zsh
set -g @plugin 'tmux-plugins/tpm'
set -g @plugin 'tmux-plugins/tmux-sensible'
set -g @plugin 'tmux-plugins/tmux-resurrect'
set -g @plugin 'tmux-plugins/tmux-continuum'

set -g @continuum-restore 'on'
run '~/.tmux/plugins/tpm/tpm'
```




## **<ins>Mini Tmux Cheatsheet</ins>** 
Reference - [https://tmuxcheatsheet.com/](https://tmuxcheatsheet.com/)

### <ins>Synchronize Panes</ins>
1. `CTRL-B` 
2. `SHIFT` + `:`
3.  
```bash
setw sychronize-panes on
```

### <ins>Make split panes default in shell</ins>
1. Add split session setting in `~/.zshrc`
```bash
echo "tmux new-session \; split-window -v\; split-window -h \; split-window -h" >> ~/.zshrc
```

2. Source zsh file
```bash
source ~/.zshrc
```

### <ins>De-synchronize Panes</ins>
1. `CTRL-B`
2. `SHIFT` + `:`
3. 
```bash
setw synchronize-panes off
```


### <ins>Copy and paste</ins>
1. `CTRL` + `B` + `[`
2. `Space`
3. Then, press `y` to paste 


### <ins>Scroll Mode</ins>
1. Scroll up mode: `CRTL` + `B` + `]`
2. To quit: `q`


### <ins>Start Tmux</ins>
1. `$ tmux`

### <ins>Rename Tmux Session</ins>
1. `CTRL b`
2. `Shift $`


### <ins>Spawn New TMUX Session without attaching</ins>
1. `$ tmux new -s newshell -d`

### <ins>List TMUX sessions</ins>
1. `$ tmux ls`


### <ins>Exit TMUX session without closing session</ins>
1. `CTRL b`
2. `d`

### <ins>Re-attach to TMUX session by name</ins>
1. `tmux attach -t <SessionName>`


### <ins>Delete TMUX session by session name</ins>
1. `tmux kill-session -t <SessionName>`

### <ins>Swap TMUX session</ins>
1. `CTRL b`
2. `s`


### <ins>Close all TMUX sessions all but one</ins>
1. `tmux kill-session -t <SessionName> -a`



### <ins>Change current directory of TMUX session</ins>
1. `CTRL b`
2. `Shift:`
3. `attach -c ~/Your/Directory/Here`