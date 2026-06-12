# KDCN-KALI 🐉

**Custom Kali NetHunter for Termux – with KDCN branding (kdcn-kali prompt)**  
*Built by Kingman Digital Cyber Network*  
*Engineered on Android · Kali Linux · Termux*

---

## About

This repository contains a **customised Kali NetHunter (rootless) installer** for Termux.  
It is based on the official NetHunter Termux installer but adds a **branded bash prompt**:

```

kdcn-(kali㉿kdcn-kali)-[~]$

```

Root prompt becomes:
```

kdcn-(root㉿kdcn-kali)-[~]#

```

No manual configuration needed – the prompt is automatically injected into `.bashrc` during installation.

> *"Move fast, not careless." – CTO KINGMAN KE*

---

## Prerequisites

- **Android device** (no root required)
- **~15GB free storage** (more for full image)
- **Stable internet** (WiFi recommended)
- **Termux** installed from [F-Droid](https://f-droid.org/repo/com.termux_118.apk) or the [NetHunter Store](https://store.nethunter.com)

---

## One‑Command Installation

Run this in Termux:

```bash
curl -LO https://github.com/Kingman37-net/KDCN-KALI/raw/main/install-kdcn-kali.sh
chmod +x install-kdcn-kali.sh
./install-kdcn-kali.sh
```

The script will:

· Detect your device architecture (arm64/armhf)
· Ask which image you want (full / minimal / nano)
· Download the rootfs (using axel or wget)
· Verify SHA512 checksum
· Extract and configure the chroot
· Set up launchers (nethunter, nh, kex)
· Apply the KDCN custom prompt
· Clean up temporary files

---

After Installation

Start Kali NetHunter CLI

```bash
nethunter
# or the shortcut:
nh
```

Your prompt will look like:

```
kdcn-(kali㉿kdcn-kali)-[~]$
```

Run as root

```bash
nethunter -r
# or:
nh -r
```

Root prompt:

```
kdcn-(root㉿kdcn-kali)-[~]#
```

Set up GUI (KeX)

```bash
nethunter kex passwd    # set your VNC password once
nethunter kex start     # start the GUI session
```

Then open the NetHunter-KeX app (install from NetHunter Store) and connect to 127.0.0.1:5901 (or use the app's autoconnect).

To stop the GUI:

```bash
nethunter kex stop
```

Update Kali

Inside NetHunter:

```bash
sudo apt update
sudo apt full-upgrade -y
```

---

What's Inside (Image Options)

Image Size Description
full ~12-15GB Complete Kali Linux with most tools (metasploit, nmap, burp, sqlmap, etc.)
minimal ~4-6GB Lightweight – core Kali utilities and networking tools
nano ~2-3GB Extremely minimal – only essential packages

Choose the one that fits your storage and needs. You can always install more tools later with sudo apt install <package>.

---

Custom Prompt – How It Works

The installer adds these lines to /home/kali/.bashrc, /root/.bashrc, and /etc/skel/.bashrc:

```bash
PS1="kdcn-(kali㉿kdcn-kali)-[\\w]\\$ "          # for kali user
PS1="kdcn-(root㉿kdcn-kali)-[\\w]\\# "          # for root
```

If you already have NetHunter installed and want only the prompt, run:

```bash
nethunter
echo 'PS1="kdcn-(kali㉿kdcn-kali)-[\\w]\\$ "' >> ~/.bashrc
source ~/.bashrc
```

---

Troubleshooting

"proot error" or "cannot create directory"

· Ensure you have enough free storage (df -h /data)
· Reinstall proot: pkg reinstall proot

"tcpdump: permission denied" (packet capture)

· Normal on non‑rooted Android – use -sT for TCP connect scans instead of raw sockets

KeX won't start / black screen

```bash
nethunter kex stop
nethunter kex passwd
nethunter kex start
```

Phantom process killer (Android kills NetHunter in background)

Use Shizuku + aShell to increase max_phantom_processes.
See this guide.

---

Uninstall

To completely remove KDCN‑KALI:

```bash
rm -rf ~/kali-arm64          # or kali-armhf
rm -f $PREFIX/bin/nethunter
rm -f $PREFIX/bin/nh
```

Optionally delete the downloaded rootfs archive (kali-nethunter-rootfs-*.tar.xz).

---

Integration with KDCN‑TOOLS

My KDCN-TOOLS repository contains native Node.js Blue Team tools (system scanner, port scanner, network monitor, etc.).
KDCN-KALI provides the full Kali Linux arsenal – together they form a complete mobile security workstation.

Use KDCN‑TOOLS for quick, lightweight assessments. Use KDCN‑KALI when you need Metasploit, Burp Suite, or other heavyweight tools.

---

Security & Legal

· Only test networks you own or have explicit written permission to audit.
· Unauthorised scanning or exploitation is illegal.
· This toolset is for educational and ethical security research.

---

Author

CTO KINGMAN KE – Founder, Kingman Digital Cyber Network
Embu, Kenya 🇰🇪

📧 kingmandigitalcybernetwork@gmail.com
🌐 kingman37-net.github.io/kingman-digital-website

---

License

Private – for authorised security testing and educational use only.

```
