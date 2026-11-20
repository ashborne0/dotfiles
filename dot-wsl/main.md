*Will be updated regularly

### ----------------------------------------------------------------------------------------------------------------
# [1]. UBUNTU | Make Default User to sudo group (Caution: security, better not) 
### ----------------------------------------------------------------------------------------------------------------

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
```bash
```
### 1. Installation

```bash
sudo apt update
```

```bash
sudo apt install -y git curl gnupg ca-certificates apt-transport-https procps tmux screen kubectx fzf
```

##### Google Cloud repo (gcloud, kubectl, GKE auth plugin)

```bash
curl -fsSL https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo gpg --dearmor -o /usr/share/keyrings/cloud.google.gpg
```

```bash
echo "deb [signed-by=/usr/share/keyrings/cloud.google.gpg] https://packages.cloud.google.com/apt cloud-sdk main" | sudo tee /etc/apt/sources.list.d/google-cloud-sdk.list
```

##### HashiCorp repo (Terraform)

```bash
curl -fsSL https://apt.releases.hashicorp.com/gpg | sudo gpg --dearmor -o /usr/share/keyrings/hashicorp-archive-keyring.gpg
```

```bash
echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/hashicorp.list
```

```bash
sudo apt update
```

```bash
sudo apt install -y google-cloud-cli google-cloud-cli-gke-gcloud-auth-plugin kubectl terraform
```

##### k9s (use arm64 instead of amd64 on an ARM laptop)
```bash
curl -fsSL -o /tmp/k9s.deb https://github.com/derailed/k9s/releases/latest/download/k9s_linux_amd64.deb
sudo apt install -y /tmp/k9s.deb
```

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

### ----------------------------------------------------------------------------------------------------------------
# [4]. UBUNTU | Network Tooling
### ----------------------------------------------------------------------------------------------------------------
these are in the dnsutils, traceroute, iputils-tracepath, mtr-tiny, netcat-openbsd, and net-tools packages

##### 1. Install:
```bash
sudo apt update
sudo apt install -y dnsutils traceroute iputils-tracepath mtr-tiny netcat-openbsd net-tools whois tcpdump openssl curl
```

##### 2. Usage
1. DNS
```bash
dig example.com              # full answer
dig +short example.com       # just the IPs
dig example.com MX           # record types: A, AAAA, MX, TXT, NS, CNAME, SOA
dig @8.8.8.8 example.com     # query a specific resolver
dig +trace example.com       # walk the delegation chain from the root
dig -x 8.8.8.8               # reverse lookup
```

2. Trace (Tracert/Traceroute)
```bash
traceroute example.com
traceroute -I example.com          # use ICMP instead of UDP (often gets through firewalls)
traceroute -T -p 443 example.com   # TCP to port 443, useful when ICMP/UDP is blocked
tracepath example.com              # no root needed
mtr example.com                    # live, continuous traceroute with packet loss per hop
mtr -rwzc 100 example.com          # 100-cycle report, good for sharing
```

3. Curl
```bash
curl -v https://example.com                    # verbose: TLS handshake, headers, errors
curl -I https://example.com                    # headers only
curl -L -I https://example.com                 # follow redirects
curl -o /dev/null -s -w "dns:%{time_namelookup} connect:%{time_connect} tls:%{time_appconnect} total:%{time_total}\n" https://example.com
curl --resolve example.com:443:1.2.3.4 https://example.com   # bypass DNS, test a specific IP
curl -x http://proxy:8080 https://example.com  # test through a proxy
```

4. Port and Listener and MISC
```bash
nc -zv example.com 443               # port check (Test-NetConnection equivalent)
sudo ss -tulpn                       # listeners and PIDs

cat /etc/resolv.conf                 # DNS config; WSL often generates this from Windows
ip route show default                # the Windows host gateway IP
ipconfig.exe                         # run the Windows ipconfig from WSL
route.exe print                      # Windows routing table from WSL
env | grep -i proxy                  # proxy env vars, common on work machines

sudo apt update && sudo apt install whois
whois IP_ADDRESS
```
