# 🧰 Install Python, VS Code, and Docker Desktop on Windows (PowerShell Tutorial)

This guide walks you through installing **Python 3.12.10**, **Visual Studio Code**, and **Docker Desktop** directly from **PowerShell (Admin)** — no manual downloads required.

---

## 🪟 Prerequisites
- Windows 10 or 11 (64-bit)
- PowerShell run as Administrator
- Stable Internet connection

---

## 🐍 Step 1 – Install Python 3.12.10

**1️⃣ Download the installer**

```powershell
curl.exe -L -o "$env:USERPROFILE\Downloads\python-3.12.10-amd64.exe" https://www.python.org/ftp/python/3.12.10/python-3.12.10-amd64.exe
````

**2️⃣ Verify the file**

```powershell
Get-Item "$env:USERPROFILE\Downloads\python-3.12.10-amd64.exe"
```

**3️⃣ Run the installer (interactive)**

```powershell
Start-Process "$env:USERPROFILE\Downloads\python-3.12.10-amd64.exe"
```

☑️ Make sure you check **“Add python.exe to PATH”** before clicking *Install Now.*

**4️⃣ Silent install (option for scripts)**

```powershell
Start-Process "$env:USERPROFILE\Downloads\python-3.12.10-amd64.exe" -ArgumentList "/quiet InstallAllUsers=1 PrependPath=1 Include_test=0" -Wait
```

**5️⃣ Restart PowerShell and verify**

```powershell
python --version
pip --version
```

---

## 🧑‍💻 Step 2 – Install Visual Studio Code

**1️⃣ Download VS Code**

```powershell
curl.exe -L -o "$env:USERPROFILE\Downloads\VSCodeSetup.exe" https://update.code.visualstudio.com/latest/win32-x64-user/stable
```

**2️⃣ Confirm download**

```powershell
Get-Item "$env:USERPROFILE\Downloads\VSCodeSetup.exe"
```

**3️⃣ Run installer**

```powershell
Start-Process "$env:USERPROFILE\Downloads\VSCodeSetup.exe"
```

Choose default options and let it add “Open with Code” and PATH entries.

**4️⃣ Restart PowerShell and verify**

```powershell
code --version
```

---

## 🐳 Step 3 – Install Docker Desktop for Windows

**1️⃣ Download Docker Desktop**

```powershell
curl.exe -L -o "$env:USERPROFILE\Downloads\DockerDesktopInstaller.exe" https://desktop.docker.com/win/main/amd64/Docker%20Desktop%20Installer.exe
```

**2️⃣ Check file**

```powershell
Get-Item "$env:USERPROFILE\Downloads\DockerDesktopInstaller.exe"
```

**3️⃣ Run the installer (interactive)**

```powershell
Start-Process "$env:USERPROFILE\Downloads\DockerDesktopInstaller.exe"
```

Follow the prompts → leave **“Use WSL 2 based engine”** checked.

**4️⃣ Silent install (optional)**

```powershell
Start-Process "$env:USERPROFILE\Downloads\DockerDesktopInstaller.exe" -ArgumentList "install --quiet" -Wait
```

**5️⃣ Restart PowerShell and verify**

```powershell
docker --version
```

You should see something like:

```
Docker version 27.0.x, build ...
```

---

## 🧰 Step 4 – Create a Quick Admin Restart Alias

If you don’t already have it:

```powershell
function Restart-PSAdmin { Start-Process "powershell" -Verb RunAs; exit }
Set-Alias restartps Restart-PSAdmin
```

Now simply type:

```powershell
restartps
```

to relaunch PowerShell in **Administrator mode** with refreshed PATH.

---

## 🧠 Step 5 – Summary

✅ Installed Python 3.12.10
✅ Installed VS Code
✅ Installed Docker Desktop
✅ Verified each installation
✅ Created a PowerShell restart alias

You’re now ready to develop locally — whether it’s Python projects, Docker containers, or LLMs using Ollama + VS Code.

---

## 🔗 References

* [Python Downloads](https://www.python.org/downloads/)
* [Visual Studio Code](https://code.visualstudio.com/)
* [Docker Desktop Docs](https://docs.docker.com/desktop/install/windows-install/)
