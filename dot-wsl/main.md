*Will be updated regularly

# ----------------------------------------------------------------------------------------------------------------
# [1]. UBUNTU | Make Default User to sudo group (Caution: security, better not) 
# ----------------------------------------------------------------------------------------------------------------

### 1. Check your group
```bash
groups
```

### 2. If sudo isn’t listed, open a root shell and add yourself. From Windows PowerShell:
```bash
wsl -u root
```

### 3. Then, inside WSL (replace yourname with your username):
```bash
usermod -aG sudo yourname
exit
```

### 4. Restart the WSL instance so the group change takes effect:
```bash
wsl --terminate Ubuntu
```

### 5. Skip the password prompt for sudo
```bash
sudo visudo -f /etc/sudoers.d/yourname
```
# ----------------------------------------------------------------------------------------------------------------
# [1]. UBUNTU | TMUX Keys 
# ----------------------------------------------------------------------------------------------------------------

Tmux
Keys	Action
Ctrl+b c	Create a new window
Ctrl+b n / p	Next / previous window
Ctrl+b 0–9	Jump to window by number
Ctrl+b %	Split pane left/right
Ctrl+b "	Split pane top/bottom
Ctrl+b arrow key	Move between panes
Ctrl+b x	Close the current pane
Ctrl+b ,	Rename the current window
Ctrl+b d	Detach from the session
Ctrl+b [	Scroll mode (press q to exit)

### 6. Skip the password prompt for sudo
```bash
yourname ALL=(ALL) NOPASSWD:ALL
```
