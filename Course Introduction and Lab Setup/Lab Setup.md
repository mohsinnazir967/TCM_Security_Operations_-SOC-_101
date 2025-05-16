# Lab Setup

Set up a virtual lab environment for hands-on exercises using virtual machines (VMs). This allows you to safely install tools and generate artifacts without affecting your main operating system.

---

## 1. Why Use Virtual Machines?

- Run Windows and Linux systems simultaneously on your computer.
- Isolate lab activities from your main OS.
- Simulate real-world SOC scenarios.

---

## 2. Hypervisor Installation

**Recommended:** Oracle VirtualBox (free and cross-platform)

### Steps:
1. Download VirtualBox from [virtualbox.org](https://www.virtualbox.org/).
   - Choose the installer for your host OS (Windows, macOS, Linux).
2. Run the installer and follow the prompts.
   - If prompted for Microsoft Visual C++ 2019, download and install it from the Microsoft website.
   - Keep default settings during installation.
   - Allow network interface reset when prompted.
3. Launch VirtualBox. If you see the VirtualBox Manager window, installation is successful.

---

## 3. Download Windows 10 ISO

1. Go to the Windows Evaluation Center or use the provided direct link to download the [Windows 10 Enterprise ISO](https://www.microsoft.com/en-us/evalcenter/download-windows-10-enterprise) .
2. Select English, 64-bit edition, and start the download (file is ~5GB).

---

## 4. Organize Lab Files

1. Create a folder structure for your lab:
   - Example: `Documents/virtual machines/sock 101`
2. Move your downloaded Windows ISO file into the `sock 101` folder.

---

## 5. Create Windows Virtual Machine

1. Open VirtualBox and click **New**.
2. Name the VM (e.g., `sock 101 - Windows 10`).
3. Set the machine folder to your lab directory.
4. Attach the Windows ISO as the startup disk.
5. Select **Skip Unattended Installation**.
6. Set RAM (recommend at least 4–8GB, or as much as your system allows).
7. Create a dynamically allocated virtual hard disk (default 50GB is fine).
8. Review the summary, then click **Finish** to create the VM.

---

## 6. Install Windows

1. Start the VM.
2. Install Windows using the ISO:
   - Select language, time, and keyboard settings.
   - Choose **Install Now**.
   - Accept the license agreement.
   - Select **Custom installation**.
   - Create a new partition (accept default size), click **Apply**, then **Next**.
   - Wait for installation to finish and VM to reboot.
3. Go through the Windows setup:
   - Use **Domain Join Instead** to create a local account (username: TCM, password: password).
   - Skip adding a Microsoft account.
   - Disable privacy and tracking settings.
   - Skip Cortana and unnecessary options.

---

## 7. Improve VM Usability

1. In VirtualBox VM window, go to **Devices > Insert Guest Additions CD image**.
2. In Windows, open the CD drive, run the Guest Additions installer (`VBoxWindowsAdditions-amd64.exe`), and reboot.
3. After reboot, enable **View > Full Screen Mode** for better resolution.
4. Go to **Devices > Shared Clipboard > Bidirectional** to enable clipboard sharing between host and VM.

---

## 8. Take a Snapshot

- In VirtualBox, with the VM selected, go to **Machine > Take Snapshot**.
- Name it `base-install`. This lets you revert to a clean state if needed.

---

## 9. Windows VM Initial Configuration

### Disable Windows Defender (for malware testing labs only)

> **Note:** Only disable Defender for lab purposes. Do NOT do this on production or personal machines.

1. Open **Windows Security** from the Start menu.
2. Go to **Virus & Threat Protection** > **Manage Settings**.
3. Turn off **Tamper Protection**.
4. Open **PowerShell as Administrator** and run the following commands to fully disable Defender:

```powershell
Set-MpPreference -DisableRealtimeMonitoring $true
Set-MpPreference -DisableIOAVProtection $true
Set-MpPreference -DisableIntrusionPreventionSystem $true
Set-MpPreference -DisableScriptScanning $true
Set-MpPreference -DisableArchiveScanning $true
Set-MpPreference -DisableBlockAtFirstSeen $true
Set-ItemProperty -Path "HKLM:\SOFTWARE\Policies\Microsoft\Windows Defender" -Name "DisableAntiSpyware" -Value 1
```

- Confirm Defender is off by checking **Virus & Threat Protection**—it should report no active antivirus provider.

---

## 10. Get Course Files onto the VM

### Install Git

1. Download Git for Windows from [git-scm.com](https://git-scm.com/).
2. Launch the installer and accept defaults.

### Clone the Course Repository

1. Open **Command Prompt**.
2. Navigate to your Documents folder:

   ```cmd
   cd %USERPROFILE%\Documents
   ```

3. Clone the repository:

   ```cmd
   git clone <course-repo-link>
   ```

4. Open the cloned `sock 101` folder. Inside, extract any provided zip files (right-click > Extract All), and place extracted folders on your Desktop for easy access.

5. (Optional) Organize your files by creating a folder (e.g., `sock 101 course files`) and moving all extracted materials inside.

6. (Optional) For quick access, create desktop shortcuts for PowerShell and Command Prompt:
   - Search for PowerShell or CMD in the Start menu, right-click, open file location, then right-click and choose "Send to Desktop (create shortcut)".

---

## 11. Create Ubuntu Linux Virtual Machine

1. Download the Ubuntu Desktop ISO (LTS version recommended) from [ubuntu.com](https://ubuntu.com/download/desktop).
   - Example version: 24.04 LTS (or latest available). For older versions, see "alternative downloads".
2. Move the downloaded ISO to your `sock 101` lab folder.
3. In VirtualBox, click **New**.
4. Name the VM (e.g., `sock 101 - Ubuntu`).
5. Set the machine folder to your lab directory.
6. Attach the Ubuntu ISO as the startup disk.
7. Select **Skip Unattended Installation**.
8. Allocate RAM (e.g., 8GB or as much as reasonable for your system).
9. Set processors to 2.
10. Create a dynamically allocated virtual hard disk (match your Windows VM storage if possible).
11. Review settings and click **Finish**.

---

## 12. Install Ubuntu

1. Start the Ubuntu VM.
2. Boot from the ISO and select **Try or Install Ubuntu**.
3. Go through the installation steps:
   - Choose language, keyboard layout, and network options.
   - Choose **Install Ubuntu**, interactive installation, and default options.
   - For storage: **Erase disk and install Ubuntu** (this affects only the virtual disk, not your real one).
   - Set account info:
     - Name: TCM
     - Computer name: sock 101 - Ubuntu
     - Username: TCM
     - Password: password
   - Set your timezone and review settings.
4. Click **Install** and wait for completion.
5. Restart when prompted. Remove the virtual ISO if asked (VirtualBox usually does this automatically).

---

## 13. Ubuntu: Improve Usability & Prepare for Labs

1. Log in to Ubuntu (user: TCM, password: password).
2. Install Guest Additions for better display and shared clipboard:
   - Open Terminal (right-click desktop > Open in Terminal).
   - Update packages:  
     ```bash
     sudo apt update
     ```
   - If prompted about systemctl daemon, run:  
     ```bash
     sudo systemctl daemon-reload
     sudo apt update
     ```
   - Install required packages:
     ```bash
     sudo apt install bzip2 tar gcc make perl git
     sudo apt install linux-headers-generic
     sudo apt install linux-headers-$(uname -r)
     ```
   - In VirtualBox menu, go to **Devices > Insert Guest Additions CD image**.
   - Mount the CD if not auto-mounted. In terminal:
     ```bash
     cd /media/TCM/VBox_GAs*   # tab to autocomplete
     sudo ./VBoxLinuxAdditions.run
     ```
   - Reboot:  
     ```bash
     sudo reboot now
     ```
   - After reboot, go to **View > Full Screen Mode** in VirtualBox.
   - Enable clipboard: **Devices > Shared Clipboard > Bidirectional**.

3. (Optional) Clean up the desktop, pin Terminal, and adjust dock position as desired:
   - Right-click desktop > Desktop icon settings > Position dock at bottom.

---

## 14. Ubuntu: Get Course Files

1. Confirm git is installed:
   ```bash
   which git
   # If not installed:
   sudo apt install git
   ```
2. Clone the course repository to your Documents folder:
   ```bash
   cd ~/Documents
   git clone <course-repo-link>
   ```
3. Extract all course zip files from the cloned folder. Move extracted folders to the desktop for easy access.
4. (Optional) Organize files and adjust dock/taskbar as you like.
5. Eject Guest Additions CD if still mounted.

---

## 15. Ubuntu: Prepare for Labs

1. Run the install script to set up required packages and dependencies:
   ```bash
   cd ~/Documents/sock\ 101/resources/install
   chmod +x install.sh
   ./install.sh
   ```

2. (Optional) Change your desktop wallpaper for a custom look:
   - Right-click desktop > Change Background > Add Picture > select `wallpaper.png` from the course repo.

---

## 16. Virtual Machine Networking (Isolate VMs from Host, Connect Them Together)

1. In VirtualBox, go to **Tools > Network** (hamburger menu).
2. Under **NAT Networks**, click **Create**.
3. Name the network (e.g., `TCM`), set the IPv4 Prefix (e.g., `192.168.1.0/24`). Make sure it's different from your host's network.
4. Keep DHCP enabled. Click **Apply**.

### Attach Both VMs to the New NAT Network

5. For each VM (Windows and Ubuntu):
   - Right-click VM > **Settings > Network**
   - Enable only **Adapter 1**.
   - Set **Attached to:** `NAT Network`, and pick your created network (e.g., `TCM`).
   - Click **OK**.

### Test VM-to-VM Connectivity

6. Start both VMs.
7. In Ubuntu, open Terminal, run:
   ```bash
   ifconfig
   ```
   - Note the IP address (e.g., `192.168.1.13`).
8. In Windows, open Command Prompt, run:
   ```cmd
   ipconfig
   ```
   - Note the IP address (e.g., `192.168.1.12`).
9. From Windows, ping Ubuntu:
   ```cmd
   ping <Ubuntu-IP>
   ```
   - You should get replies.
   - (Reverse pings from Ubuntu to Windows may fail unless Windows firewall is adjusted, but this is not required.)

---

Your lab environment is now fully set up: both VMs are installed, configured, networked, and ready for practical SOC exercises.