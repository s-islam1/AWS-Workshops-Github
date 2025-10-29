**PowerShell scripts**:

* `download-tools.ps1` → downloads all installers to your **Downloads** folder
* `install-tools.ps1` → installs them **in order**, waiting for each to finish

---

## 1) `download-tools.ps1` — download all installers

```powershell
<#  download-tools.ps1
    Downloads installers for:
      1) VS Code (User installer, x64, Stable)
      2) Ollama
      3) Python 3.12.10 (x64)
      4) Docker Desktop (x64)
#>

Set-StrictMode -Version Latest
$ErrorActionPreference = 'Stop'

# Where to save the files
$DownloadDir = Join-Path $env:USERPROFILE 'Downloads'
New-Item -ItemType Directory -Force -Path $DownloadDir | Out-Null

# Destination file paths
$VSCodeExe   = Join-Path $DownloadDir 'VSCodeSetup.exe'
$OllamaExe   = Join-Path $DownloadDir 'OllamaSetup.exe'
$PythonExe   = Join-Path $DownloadDir 'python-3.12.10-amd64.exe'
$DockerExe   = Join-Path $DownloadDir 'DockerDesktopInstaller.exe'

# Source URLs
$VSCodeUrl   = 'https://update.code.visualstudio.com/latest/win32-x64-user/stable'
$OllamaUrl   = 'https://ollama.com/download/OllamaSetup.exe'
$PythonUrl   = 'https://www.python.org/ftp/python/3.12.10/python-3.12.10-amd64.exe'
$DockerUrl   = 'https://desktop.docker.com/win/main/amd64/Docker%20Desktop%20Installer.exe'

function Download-File {
    param(
        [Parameter(Mandatory)] [string]$Url,
        [Parameter(Mandatory)] [string]$Destination
    )
    if (Test-Path $Destination) {
        Write-Host "✔ File already exists, skipping: $Destination"
        return
    }
    Write-Host "↓ Downloading:`n  $Url`n→ $Destination"
    # Use curl.exe for speed & reliability; follow redirects; retry a few times
    $args = @('-L', '--retry', '5', '--retry-delay', '2', '-o', $Destination, $Url)
    $proc = Start-Process -FilePath 'curl.exe' -ArgumentList $args -NoNewWindow -PassThru -Wait
    if ($proc.ExitCode -ne 0) {
        throw "Download failed (exit=$($proc.ExitCode)) for $Url"
    }
    Write-Host "✔ Downloaded: $Destination`n"
}

Download-File -Url $VSCodeUrl -Destination $VSCodeExe
Download-File -Url $OllamaUrl -Destination $OllamaExe
Download-File -Url $PythonUrl -Destination $PythonExe
Download-File -Url $DockerUrl -Destination $DockerExe

Write-Host "`nAll downloads complete. Files saved in: $DownloadDir"
```

---

## 2) `install-tools.ps1` — install sequentially (wait between each)

```powershell
<#  install-tools.ps1
    Installs, in order (waiting for each to finish):
      1) VS Code
      2) Ollama
      3) Python 3.12.10
      4) Docker Desktop
#>

Set-StrictMode -Version Latest
$ErrorActionPreference = 'Stop'

# --- Ensure the script is running elevated (Admin) ---
function Ensure-Admin {
    $id   = [Security.Principal.WindowsIdentity]::GetCurrent()
    $pr   = New-Object Security.Principal.WindowsPrincipal($id)
    $isAdmin = $pr.IsInRole([Security.Principal.WindowsBuiltInRole]::Administrator)
    if (-not $isAdmin) {
        Write-Host "Requesting elevation..."
        Start-Process -FilePath "powershell.exe" -Verb RunAs -ArgumentList "-NoProfile","-ExecutionPolicy","Bypass","-File","`"$PSCommandPath`""
        exit
    }
}
Ensure-Admin

# Paths (must match what the download script used)
$DownloadDir = Join-Path $env:USERPROFILE 'Downloads'
$VSCodeExe   = Join-Path $DownloadDir 'VSCodeSetup.exe'
$OllamaExe   = Join-Path $DownloadDir 'OllamaSetup.exe'
$PythonExe   = Join-Path $DownloadDir 'python-3.12.10-amd64.exe'
$DockerExe   = Join-Path $DownloadDir 'DockerDesktopInstaller.exe'

function Require-File {
    param([string]$Path)
    if (-not (Test-Path $Path)) { throw "Missing installer: $Path" }
}

function Install-Interactive {
    param([string]$Path, [string]$Name)
    Write-Host "▶ Launching $Name installer (interactive): $Path"
    Start-Process -FilePath $Path -Wait
    Write-Host "✔ $Name installation step finished.`n"
}

# If you want SILENT installs instead, use the function below per app
function Install-Silent {
    param([string]$Path, [string]$Name, [string[]]$Args)
    Write-Host "▶ Launching $Name installer (silent): $Path $($Args -join ' ')"
    Start-Process -FilePath $Path -ArgumentList $Args -Wait
    Write-Host "✔ $Name installation step finished.`n"
}

# 1) VS Code
Require-File $VSCodeExe
# Interactive:
Install-Interactive -Path $VSCodeExe -Name 'Visual Studio Code'
# Silent alternative (comment interactive and uncomment below if you prefer):
# Install-Silent -Path $VSCodeExe -Name 'Visual Studio Code' -Args @('/VERYSILENT','/MERGETASKS=!runcode,addcontextmenufiles,addcontextmenufolders,addtopath')

# 2) Ollama
Require-File $OllamaExe
Install-Interactive -Path $OllamaExe -Name 'Ollama'
# (Ollama’s silent switches are not officially documented; interactive is safest.)

# 3) Python 3.12.10
Require-File $PythonExe
# Interactive:
Install-Interactive -Path $PythonExe -Name 'Python 3.12.10'
# Silent alternative (recommended for labs; adds Python to PATH):
# Install-Silent -Path $PythonExe -Name 'Python 3.12.10' -Args @('/quiet','InstallAllUsers=1','PrependPath=1','Include_test=0')

# 4) Docker Desktop
Require-File $DockerExe
# Interactive (prompts for WSL 2 if needed):
Install-Interactive -Path $DockerExe -Name 'Docker Desktop'
# Silent alternative:
# Install-Silent -Path $DockerExe -Name 'Docker Desktop' -Args @('install','--quiet')  # optionally add: '--accept-license'

Write-Host "🎉 All installers completed. Open a NEW PowerShell window to refresh PATH."

# Quick post-checks (optional; comment out if you used interactive installs and haven't restarted yet)
Write-Host "`n🔎 Quick version checks (may require reopening terminal):"
Write-Host "code --version:"
try { & code --version | Select-Object -First 1 } catch { Write-Host "  (VS Code CLI not in PATH yet)"; }

Write-Host "`nollama --version:"
try { & ollama --version } catch { Write-Host "  (Ollama not in PATH yet)"; }

Write-Host "`npython --version:"
try { & python --version } catch { Write-Host "  (Python not in PATH yet)"; }

Write-Host "`ndocker --version:"
try { & docker --version } catch { Write-Host "  (Docker not in PATH yet)"; }
```

---

### How to run

1. **Open PowerShell as Administrator**
2. Allow local scripts (first time only):

```powershell
Set-ExecutionPolicy -ExecutionPolicy Bypass -Scope Process -Force
```

3. Run the download script:

```powershell
.\download-tools.ps1
```

4. Run the installer script:

```powershell
.\install-tools.ps1
```
