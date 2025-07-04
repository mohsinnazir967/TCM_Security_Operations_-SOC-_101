# Email Analysis Configuration 

Set up your Ubuntu VM for practical email analysis using Thunderbird and Sublime Text.

---

## 1. Install Mozilla Thunderbird (Email Client)

Thunderbird is a free, open-source email client used to open and analyze `.eml` files.

###  Install Thunderbird
```bash
sudo apt install thunderbird
```

###  Launch Thunderbird
1. Open **Thunderbird** via applications menu.
2. On first launch → Click **Cancel** on email setup.
3. You can now open `.eml` files locally without adding an account.

###  Opening `.eml` Files
- Double-click any `.eml` file.
- If not opening automatically:
  - Right-click the file → **Open With** → Select **Thunderbird Mail**.

###  Settings Adjustment
To allow remote images/content to load:
1. Open Thunderbird.
2. Click ☰ (hamburger menu) → **Settings**.
3. Go to **Privacy & Security** tab.
4. Enable:  
   ✅ *Allow remote content in messages*.

---

## ✍️ 2. Install Sublime Text (Text/Code Editor)

Used for manual analysis of raw email content and headers.

###  Download & Install
Visit: [https://www.sublimetext.com](https://www.sublimetext.com)

### 📦 Terminal Installation (Stable Version)
```bash
# Add GPG key
wget -qO - https://download.sublimetext.com/sublimehq-pub.gpg | sudo apt-key add -

# Add apt repo
echo "deb https://download.sublimetext.com/ apt/stable/" | sudo tee /etc/apt/sources.list.d/sublime-text.list

# Update packages
sudo apt-get update

# Optional fix for systemctl error
sudo systemctl daemon-reload

# Install Sublime Text
sudo apt-get install sublime-text
```

### 🧪 Verify Installation
- Open from **Applications** → Search **Sublime Text**.
- Alternatively, use `subl` command in terminal.

---

## 📂 3. Open `.eml` Files in Sublime

Navigate to your `.eml` file directory and open a sample email.

```bash
cd ~/Desktop/01-phishing-analysis/01-header-analysis
ls
subl sample1.eml
```

---

