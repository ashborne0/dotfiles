*Will be updated regularly

# Download Latest and LTS Microsoft PowerShell in Microsoft Store 
# Download Latest and LTS Microsoft PowerToys in Microsoft Store

# ---------------------------------------------------------------------
# Profile
# ---------------------------------------------------------------------

1. CRUD
```shell
Get-Content $PROFILE
$PROFILE
Test-Path $PROFILE
open $PROFILE
code $PROFILE
```
2. Execution Policy
```shell
Set-ExecutionPolicy -Scope CurrentUser -ExecutionPolicy RemoteSigned
```

# -------------------------------------------------------------------------
# oh-my-posh installation [https://ohmyposh.dev/docs/installation/windows]
# -------------------------------------------------------------------------

```bash
```
### 1. Install the package with winget
```bash
winget install JanDeDobbeleer.OhMyPosh -s winget
```
Close and reopen PowerShell, then install the font:

### 2. Download Font
```bash
oh-my-posh font install meslo
```

### 3. Download Theme, in this case Neko
```bash
New-Item -ItemType Directory -Force "$HOME\.poshthemes" | Out-Null
Invoke-WebRequest https://raw.githubusercontent.com/JanDeDobbeleer/oh-my-posh/main/themes/neko.omp.json -OutFile "$HOME\.poshthemes\neko.omp.json"
```

### 4. Make Oh-my-post persistent in Powershell
```bash
if (!(Test-Path -Path $PROFILE)) { New-Item -ItemType File -Path $PROFILE -Force }
Add-Content $PROFILE 'oh-my-posh init pwsh --config "$HOME\.poshthemes\neko.omp.json" | Invoke-Expression'
```

### Exercpt
if above command cannot persist, just use this
```bash
oh-my-posh init pwsh --config "$HOME\.poshthemes\neko.omp.json" | Invoke-Expression
```

# ---------------------------
# WSL setup and installation 
# ---------------------------

### 1. Verify WSL service exists in your PC
```bash
wsl.exe
```

### 2. Search Distro Online
```bash
wsl.exe --list --online
```

### 3. Install selected Distro
```bash
wsl.exe --install Ubuntu-26.04 
```

# ---------------------------------------------------------------------------------------
# Tooling (Gcloud CLI, Kubectl, Terraform, K9s, git, kubectx, kubens, watch, screen/tmux)
# ---------------------------------------------------------------------------------------
winget install --id Git.Git -e
winget install --id Google.CloudSDK -e
winget install --id Kubernetes.kubectl -e
winget install --id Hashicorp.Terraform -e
winget install --id Derailed.k9s -e
winget install --id ahmetb.kubectx -e
winget install --id ahmetb.kubens -e
winget install psmux

watch (add this to ps $PROFILE)
```cpp
function watch {
    param([int]$n = 2, [Parameter(Mandatory, ValueFromRemainingArguments)]$cmd)
    while ($true) {
        $out = & { Invoke-Expression ($cmd -join ' ') 2>&1 | Out-String }
        Clear-Host
        "Every ${n}s: $($cmd -join ' ')   $(Get-Date -Format 'HH:mm:ss')`n"
        $out
        Start-Sleep $n
    }
}
```
Usage: ```bash watch 2 kubectl get pods```

# -----
# Misc
# -----

### 1. Why Apostrophes and double quotes don't show up until I type the next letter on Windows 11?
Answer: This is because keyboard layouts gets sets to "United States - International". Commonly faced issue for Windows 11 new devices.
Solution: change Keyboard layout to US only.

On Windows 11:
#### 1. Search "Language and Region" in the start menu
#### 2. Click the "Three Dots" menu next to  the current language settings
<img width="1807" height="1394" alt="image" src="https://github.com/user-attachments/assets/7d667881-465c-4cc2-a1ef-12c7dceb784a" />

#### 3. Scroll down below, Click "Add a Keyboard" and Select "US" instead of "US - International" (or your approriate keyboard layout preferences for your region or else)
<img width="803" height="620" alt="image" src="https://github.com/user-attachments/assets/bca37b2d-d119-4ec1-b09a-066ed5359d8b" />

