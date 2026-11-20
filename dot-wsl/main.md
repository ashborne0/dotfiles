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

### 6. Skip the password prompt for sudo
```bash
yourname ALL=(ALL) NOPASSWD:ALL
```
