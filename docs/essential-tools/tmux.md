---
title: Tmux
layout: default
nav_order: 1
parent: Essential Tools

---

# Tmux
### Tmux Installation
`tmux` conf that allows for copy/pasting and other convenient options within Tmux 

1. Install tmux
```bash
sudo apt install tmux -y
```

2. Create a ~/.tmux.conf file
```bash
touch ~/.tmux.conf
```

3. Source the newly created tmux conf file
```bash
source ~/.tmux.conf
```

### Tmux configuration file
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




### Mini Tmux Cheatsheet 
Reference - https://tmuxcheatsheet.com/

#### Synchronize Panes
1. `CTRL-B` 
2. `SHIFT` + `:`
3.  
```bash
setw sychronize-panes on
```

#### Make split panes default in shell

1. Add split session setting in `~/.zshrc`
```bash
echo "tmux new-session \; split-window -v\; split-window -h \; split-window -h" >> ~/.zshrc
```

2. Source zsh file
```bash
source ~/.zshrc
```

#### De-synchronize Panes
1. `CTRL-B`
2. `SHIFT` + `:`
3. 
```bash
setw synchronize-panes off
```


#### Copy and paste
1. `CTRL` + `B` + `[`
2. `Space`
3. Then, press `y` to paste 


#### Scroll Mode
1. Scroll up mode: `CRTL` + `B` + `]`
2. To quit: `q`


#### Start Tmux
1. `$ tmux`

#### Rename Tmux Session
1. `CTRL b`
2. `Shift $`


#### Spawn New TMUX Session without attaching

1. `$ tmux new -s newshell -d`

#### List TMUX sessions

1. `$ tmux ls`


#### Exit TMUX session without closing session

1. `CTRL b`
2. `d`

#### Re-attach to TMUX session by name
1. `tmux attach -t <SessionName>`


#### Delete TMUX session by session name
1. `tmux kill-session -t <SessionName>`

#### Swap TMUX session
1. `CTRL b`
2. `s`


#### Close all TMUX sessions all but one
1. `tmux kill-session -t <SessionName> -a`



#### Change current directory of TMUX session
1. `CTRL b`
2. `Shift:`
3. `attach -c ~/Your/Directory/Here`

