---
title: Tmux配置文件（修复版）
date: 2021-12-21T21:42:26+08:00
lastmod: 2021-12-21T21:42:26+08:00
author: Cai Song
# avatar: /img/author.jpg
# authorlink: https://author.site
cover: /img/cover.jpg
# images:
#   - /img/cover.jpg
categories:
  - category1
tags:
  - tag1
  - tag2
# nolastmod: true
draft: false
---

Cut out summary from your post content here.

<!--more-->

The remaining content of your post.
tmux配置文件（修复版）
```plain
unbind C-b
set -g prefix C-a
bind C-a send-prefix
bind r source-file ~/.tmux.conf \; display "Reloaded!"


# Use Shift-arrow keys to switch panes
bind -n S-Left select-pane -L
bind -n S-Right select-pane -R
bind -n S-Up select-pane -U
bind -n S-Down select-pane -D

# Alt-arrow to switch windows
bind -n M-Left previous-window
bind -n M-Right next-window


#Enable mouse mode (tmux 2.1 and above)
setw -g mouse on
set -g mouse on

#Enable oh my zsh in tmux
#set -g default-command /bin/zsh

# Mouse based copy
bind-key -T copy-mode-vi MouseDragEnd1Pane send -X copy-pipe-and-cancel "reattach-to-user-namespace
pbcopy"
bind-key -T copy-mode MouseDragEnd1Pane send -X copy-pipe-and-cancel "reattach-to-user-namespace pbc
opy"

#开启status-bar uft-8支持
set -g status-utf8 on


#设置终端颜色为256色
set -g default-terminal "screen-256color"
#开启status-bar uft-8支持
set -g status-utf8 on
#设置pan前景色
set -g pane-border-fg green
#设置pane背景色
set -g pane-border-bg black
#设置活跃pane前景色
set -g pane-active-border-fg white
#设置活跃pane背景色
set -g pane-active-border-bg yellow
#设置消息前景色
set -g message-fg white
#设置消息背景色
set -g message-bg black
#设置消息高亮显示
set -g message-attr bright
#设置status-bar颜色
set -g status-fg white
set -g status-bg black
#设置窗口列表颜色
setw -g window-status-style fg=cyan
setw -g window-status-style bg=default
setw -g window-status-style dim
#设置当前窗口在status bar中的颜色
setw -g window-status-current-style fg=white
setw -g window-status-current-style bg=red
setw -g window-status-current-style bright
#设置status bar格式
set -g status-left-length 40
set -g status-left "#[fg=green]Session: #S #[fg=yellow]#I #[fg=cyan]#P"
set -g status-right "#[fg=cyan]%b %d %R"
set -g status-interval 60
set -g status-justify centre
```

Tags:
  tmux