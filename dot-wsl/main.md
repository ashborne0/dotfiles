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

# ----------------------------------------------------------------------------------------------------------------
# [2]. UBUNTU | TMUX Keys 
# ----------------------------------------------------------------------------------------------------------------

| Keys | Action |
|---|---|
| Ctrl+b c | Create a new window |
| Ctrl+b n / p | Next / previous window |
| Ctrl+b 0–9 | Jump to window by number |
| Ctrl+b % | Split pane left/right |
| Ctrl+b " | Split pane top/bottom |
| Ctrl+b arrow key | Move between panes |
| Ctrl+b x | Close the current pane |
| Ctrl+b , | Rename the current window |
| Ctrl+b d | Detach from the session |
| Ctrl+b [ | Scroll mode (press q to exit) |

# ----------------------------------------------------------------------------------------------------------------
# [3]. UBUNTU | Core Tooling (Gcloud CLI, Kubectl, Terraform, K9s, git, kubectx, kubens, watch, screen/tmux)
# ----------------------------------------------------------------------------------------------------------------

### 1. Installation
sudo apt update

sudo apt install -y git curl gnupg ca-certificates apt-transport-https procps tmux screen kubectx fzf

##### Google Cloud repo (gcloud, kubectl, GKE auth plugin)

curl -fsSL https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo gpg --dearmor -o /usr/share/keyrings/cloud.google.gpg

echo "deb [signed-by=/usr/share/keyrings/cloud.google.gpg] https://packages.cloud.google.com/apt cloud-sdk main" | sudo tee /etc/apt/sources.list.d/google-cloud-sdk.list

##### HashiCorp repo (Terraform)

curl -fsSL https://apt.releases.hashicorp.com/gpg | sudo gpg --dearmor -o /usr/share/keyrings/hashicorp-archive-keyring.gpg

echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/hashicorp.list

sudo apt update

sudo apt install -y google-cloud-cli google-cloud-cli-gke-gcloud-auth-plugin kubectl terraform

# k9s (use arm64 instead of amd64 on an ARM laptop)
curl -fsSL -o /tmp/k9s.deb https://github.com/derailed/k9s/releases/latest/download/k9s_linux_amd64.deb
sudo apt install -y /tmp/k9s.deb

### 2. Verify
```bash
git --version; gcloud version; kubectl version --client; terraform version; k9s version; kubectx -h; kubens -h; watch --version; tmux -V; screen --version
```

### 3. Post Installation
```bash
gcloud auth login
gcloud auth application-default login   # used by Terraform
gcloud config set project <PROJECT_ID>
gcloud container clusters get-credentials <CLUSTER> --region <REGION>
git config --global user.name "Your Name"
git config --global user.email "you@company.com"
```
