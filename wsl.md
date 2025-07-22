Installing **Windows Subsystem for Linux (WSL)** and running **Ubuntu** on Windows 10 is straightforward. Follow these steps:

---

### **Step 1: Enable WSL in Windows 10**
1. **Open PowerShell as Administrator** (Right-click Start → **Windows PowerShell (Admin)**).  
2. Run the following command to enable WSL:
   ```powershell
   wsl --install
   ```
   *(This automatically enables WSL and installs Ubuntu by default.)*  

   **If the above doesn't work**, manually enable WSL:
   ```powershell
   dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
   ```

3. **Enable Virtual Machine Platform** (Required for WSL 2):
   ```powershell
   dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
   ```
4. **Restart your PC**.

---

### **Step 2: Install Ubuntu from Microsoft Store**
1. Open the **Microsoft Store**:  
   - Search for **"Ubuntu"** (choose the latest LTS version, e.g., *Ubuntu 22.04 LTS*).  
   - Click **Install**.  

   *(Alternatively, list available distros via PowerShell: `wsl --list --online` and install with `wsl --install -d Ubuntu-22.04`.)*

2. **Launch Ubuntu** from the Start Menu.  
   - On first run, it will install and ask for a **username/password** (this is your Linux user, separate from Windows).

---

### **Step 3: Set WSL 2 as Default (Recommended)**
WSL 2 is faster and more compatible than WSL 1.  
1. Check WSL version:
   ```powershell
   wsl --list --verbose
   ```
2. If your Ubuntu is on **WSL 1**, upgrade it:
   ```powershell
   wsl --set-version Ubuntu-22.04 2
   ```
3. Set WSL 2 as default for new installations:
   ```powershell
   wsl --set-default-version 2
   ```

---

### **Step 4: Update Ubuntu**
After installation, run these commands in the Ubuntu terminal:
```bash
sudo apt update && sudo apt upgrade -y
```

---

### **Step 5: Access Linux Files from Windows**
- WSL files are stored at:  
  ```
  \\wsl$\Ubuntu-22.04\home\<your_username>\
  ```
  *(Replace `Ubuntu-22.04` with your distro name.)*

- Windows files are accessible in WSL at:  
  ```bash
  /mnt/c/  # C: drive
  /mnt/d/  # D: drive, etc.
  ```

---

### **Step 6: Optional: Install a Terminal (Windows Terminal)**
For a better experience, install **Windows Terminal** from the Microsoft Store.  
- Supports tabs, themes, and multiple WSL instances.

---

### **Step 7: Run Ubuntu Commands**
Now you can use Ubuntu commands directly in Windows:
```bash
# Example: Install a package
sudo apt install git

# Start a Python server
python3 -m http.server 8000
```

---

### **Troubleshooting**
1. **WSL Not Recognized?**  
   - Ensure **Windows 10 Version 2004 or later** (`Win + R` → `winver`).  
   - Re-enable WSL via **Turn Windows Features On/Off**:
     - Check **"Windows Subsystem for Linux"** and **"Virtual Machine Platform"**.

2. **Network Issues?**  
   - Reset WSL:
     ```powershell
     wsl --shutdown
     ```

3. **Need GUI Apps?**  
   - Install an X Server like **VcXsrv** or use **WSLg** (built into Windows 11).

---

### **Uninstall WSL**
To remove Ubuntu:
```powershell
wsl --unregister Ubuntu-22.04
```

---

That’s it! You now have a fully functional Ubuntu environment in Windows 10 via WSL. Let me know if you need help with specific configurations! 🚀