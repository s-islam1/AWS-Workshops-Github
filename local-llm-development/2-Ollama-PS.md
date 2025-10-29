# 🧠 Install and Run Ollama on Windows (via PowerShell)

This guide walks you through installing **Ollama** — a lightweight local large language model (LLM) runtime — directly from **PowerShell** on Windows.  
You’ll download, install, verify, and run a model locally — plus create a quick restart alias for PowerShell.

---

## 🪟 Prerequisites

- Windows 10 or 11 (64-bit)
- PowerShell (Run as **Administrator**)
- Internet connection

---

## ⚙️ Step 1: Download Ollama Installer Using `curl`

Run the following command in **PowerShell (Admin)**:

```powershell
curl.exe -L -o "$env:USERPROFILE\Downloads\OllamaSetup.exe" https://ollama.com/download/OllamaSetup.exe
````

✅ **Explanation:**

* `curl.exe` → ensures PowerShell uses the native `curl` binary (not the alias).
* `-L` → follows redirects (some URLs redirect internally).
* `-o` → saves the file to your Downloads folder.

---

## 📁 Step 2: Confirm the File Downloaded

Verify the installer exists and check its size:

```powershell
Get-Item "$env:USERPROFILE\Downloads\OllamaSetup.exe"
```

If you see details like file size and modification time, it downloaded successfully.

---

## ⚡ Step 3: Launch the Installer

Run the Ollama setup wizard:

```powershell
Start-Process "$env:USERPROFILE\Downloads\OllamaSetup.exe"
```

Follow the on-screen instructions.
Ollama installs by default to:

```
C:\Users\<YourName>\AppData\Local\Programs\Ollama
```

---

## 🔁 Step 4: Restart PowerShell (to refresh PATH)

Once the installer finishes, **close and reopen** PowerShell.
Alternatively, you can use this command to automatically restart it as Admin:

```powershell
Start-Process "powershell" -Verb RunAs
exit
```

---

## ✅ Step 5: Verify the Installation

Run:

```powershell
ollama --version
```

You should see something like:

```
ollama version 0.1.32
```

---

## 🧩 Step 6: Pull and Run a Model

Pull a small, efficient model:

```powershell
ollama pull gemma3:1b
```

Then run it:

```powershell
ollama run gemma3:1b
```

Type any question — for example:

```
What is a neural network?
```

To exit, press **Ctrl + C** or type /bye

```
/bye
```



---

## 🧰 Step 7: Create a PowerShell Restart Function and Alias

You can create a helper function to quickly reopen PowerShell in Administrator mode (useful after new installs).

Run:

```powershell
function Restart-PSAdmin { Start-Process "powershell" -Verb RunAs; exit }
Set-Alias restartps Restart-PSAdmin
```

Now, anytime you need to restart PowerShell as Admin, just type:

```powershell
restartps
```

💡 **Tip:** To make this permanent, add those two lines to your PowerShell profile:

```powershell
notepad $PROFILE
```

Paste the lines at the end and save.

---

## 🧠 Step 8: Summary

You’ve now successfully:

✅ Downloaded Ollama via PowerShell
✅ Installed and verified it
✅ Pulled and ran a local model (`gemma3:1b`)
✅ Created a restart alias for PowerShell

You can now experiment with larger models, integrate Ollama with Python, or connect it to a local web UI like **Open WebUI**.

---

### 🧾 References

* [Ollama Official Site](https://ollama.com)
* [Model Library](https://ollama.com/library)
* [Ollama GitHub](https://github.com/ollama/ollama)

---

### 💡 Author

Created by **Shahpar Islam**
Assistant Professor, NOVA IET Department
[https://github.com/s-islam1](https://github.com/s-islam1)
