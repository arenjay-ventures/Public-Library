---
layout: default
title: Multi-Boot USB Setup Guide
parent: Linux Lab
nav_order: 1
---

# Multi-Boot USB Setup Guide (Windows)
## Puppy Linux, Tails, Kali Linux & Kali Purple on One 32GB USB Drive
##CURRENT STATE Puppy, Tails, and Kali are bootable Kali Purple is Not, fails install from USB##
---

## Prerequisites

**What You'll Need:**
- 32GB USB-C drive (USB 3.1+ recommended)
- Windows computer with Administrator access
- Internet connection for downloads
- Approximately 1-2 hours for complete setup

**Downloads Required:**
1. Ventoy installer (Windows): https://www.ventoy.net/en/download.html
2. Puppy Linux ISO: https://puppylinux-woof-ce.github.io/
3. Tails ISO: https://tails.boum.org/install/download/
4. Kali Linux ISO: https://www.kali.org/get-kali/
5. Kali Purple ISO: https://www.kali.org/get-kali/ (select Purple edition)

**Important:** Download 64-bit/amd64 versions for all ISOs.

---

## Part 1: Installing Ventoy on Your USB Drive

### Step 1: Download and Extract Ventoy

1. Visit https://www.ventoy.net/en/download.html
2. Download the Windows version (ventoy-x.x.xx-windows.zip)
3. Extract the ZIP file to a folder (right-click → Extract All)
4. Open the extracted folder

### Step 2: Launch Ventoy Installer

1. Find `Ventoy2Disk.exe` in the folder
2. **Right-click** on `Ventoy2Disk.exe`
3. Select **"Run as administrator"**
4. Click "Yes" on the User Account Control prompt
5. The Ventoy window will open

### Step 3: Configure Ventoy Options (Important!)

**Before installing, configure these options:**

1. Click the **"Option"** button at the top
2. **Partition Style:**
   - Select **GPT** (for UEFI systems - most modern computers)
   - Or select **MBR** (for older systems/Legacy BIOS)
   - **Recommendation:** Try GPT first
3. **Secure Boot Support:**
   - Check the box for **"Secure Boot Support"**
   - This includes the MOK key for Secure Boot systems
4. Click **"OK"** to save options

### Step 4: Install Ventoy to USB Drive

**WARNING: This will ERASE ALL data on your USB drive!**

1. In the Ventoy window, click the **Device** dropdown
2. Select your 32GB USB drive
3. **CAREFULLY verify this is the correct drive!**
   - Check the size matches your USB
   - Check the drive letter
   - **Wrong drive = data loss!**
4. Click the **"Install"** button
5. **Read the warning carefully**
6. Click **"Yes"** to confirm
7. Click **"Yes"** again on the second confirmation
8. Wait for installation (1-2 minutes)
9. You'll see **"Install Success"** when complete
10. Click **"OK"**

### Step 5: Verify Installation

1. Open **File Explorer** (Windows Explorer)
2. You should see your USB drive labeled **"Ventoy"**
3. The drive should be mostly empty with large free space
4. There's also a hidden VTOYEFI partition (32MB) - **don't touch this**

---

## Part 2: Adding Linux Distributions

### Step 6: Copy ISO Files to USB

1. Open **File Explorer**
2. Navigate to where you downloaded the ISO files
3. Open your **Ventoy USB drive** in another window
4. **Copy and paste** (or drag and drop) all four ISO files to the Ventoy drive:
   - PuppyLinux-X.XX.iso
   - tails-amd64-X.X.iso
   - kali-linux-XXXX.X-live-amd64.iso
   - kali-purple-XXXX.X-live-amd64.iso
5. Wait for all files to copy (10-20 minutes depending on USB speed)
6. **Do NOT extract or rename the files!** Keep them as .iso files

**Optional Organization:**
- You can create folders on the USB to organize ISOs
- Example: Create folders named "Security", "Privacy", "Lightweight"
- Move ISOs into appropriate folders
- Ventoy will find them in any folder structure

### Step 7: Safely Eject USB

1. Click the **"Safely Remove Hardware"** icon in system tray
2. Select your Ventoy USB drive
3. Wait for **"Safe to Remove Hardware"** message
4. Remove USB drive

---

## Part 3: Setting Up Persistence (Optional but Recommended)

Persistence allows you to save changes, installed tools, and files between reboots.

### Step 8: Create Persistence Files for Kali Linux

**Using VentoyPlugson (GUI Method):**

1. **Re-insert your Ventoy USB drive** if removed
2. Navigate to your Ventoy installation folder
3. Find and **double-click** `VentoyPlugson.exe`
4. Your default web browser will open automatically
5. You'll see the Ventoy Plugin Configuration page

**Configure Persistence:**

1. Click on **"Persistence Management"** in the left menu
2. Click **"Create New Persistence"** button
3. **For Kali Linux:**
   - **Select ISO:** Click dropdown and choose "kali-linux-XXXX.X-live-amd64.iso"
   - **Size:** Enter `8192` (8GB recommended)
   - **Label:** Type `persistence`
   - **File System:** Select `ext4`
4. Click **"OK"**
5. Wait for creation (5-10 minutes) - progress bar will show status
6. **Repeat for Kali Purple:**
   - Select "kali-purple-XXXX.X-live-amd64.iso"
   - Size: `4096` (4GB)
   - Label: `persistence`
   - File System: `ext4`
7. Close browser when done

**Notes on Other Distros:**
- **Tails:** Has built-in persistence wizard on first boot (**THIS DOES NOT WORK ON MY USB**)
- **Puppy Linux:** Automatically prompts to create save file on first shutdown

---

## Part 4: Preparing Your Computer for Boot

### Step 9: Check BitLocker Status (Important!)

**If you have Windows BitLocker enabled:**

1. Open **Start Menu**
2. Type **"BitLocker"**
3. Click **"Manage BitLocker"**
4. If your drive shows **"BitLocker On"**:
   - Click **"Turn off BitLocker"**
   - Wait for decryption to complete (may take a while)
   - **Why:** Disabling Secure Boot triggers BitLocker protection

**If BitLocker is already off, skip to next step.**

### Step 10: Access BIOS/UEFI Settings

**For HP Computers:**
1. **Restart** your computer
2. Immediately press **ESC** key repeatedly as computer starts
3. When you see the Startup Menu, press **F10** for BIOS Setup

**For Other Brands:**
- **Dell:** Press **F2** or **F12** during startup
- **Lenovo:** Press **F1** or **F2** during startup
- **ASUS:** Press **F2** or **DEL** during startup
- **Acer:** Press **F2** or **DEL** during startup
- **Generic:** Try **F2**, **F10**, **F12**, **DEL**, or **ESC**

Watch your screen during boot for a message like "Press F2 for Setup"

---

## Part 5: BIOS Configuration (Critical!)

### Step 11: Disable Secure Boot

**This is required for all distros to boot properly.**

**For HP Computers:**

1. Navigate to the **"Security"** tab (use arrow keys)
2. Select **"Secure Boot Configuration"**
3. Press **Enter**
4. Find **"Configure Legacy Support and Secure Boot"**
5. Change setting to:
   - **"Legacy Support Enable and Secure Boot Disable"**
   - Or simply: **"Secure Boot Disable"**
6. Press **Enter** to confirm
7. Press **F10** to save changes
8. Select **"Yes"** to confirm
9. Computer will restart

**For Other Brands:**

1. Look for **"Security"**, **"Boot"**, or **"Authentication"** tab
2. Find **"Secure Boot"** setting
3. Change to **"Disabled"**
4. Save and exit (usually **F10**)

### Step 12: Verify Boot Order (Optional)

While in BIOS, ensure USB boot is enabled:

1. Navigate to **"Boot"** tab
2. Look for **"Boot Order"** or **"Boot Priority"**
3. Ensure **"USB Device"** or **"Removable Devices"** is enabled
4. Optionally move it to top of boot order
5. Save and exit if you made changes

---

## Part 6: Booting Your Multi-Boot USB

### Step 13: Boot from USB Drive

**Method 1: Boot Menu (Easiest)**

1. **Insert your Ventoy USB drive**
2. **Restart** your computer
3. **Press the Boot Menu key** during startup:
   - **HP:** Press **F9** or **ESC** then **F9**
   - **Dell:** Press **F12**
   - **Lenovo:** Press **F12**
   - **ASUS:** Press **F8** or **ESC**
   - **Acer:** Press **F12**
4. **Select your USB drive** from the list
   - May appear as "USB Storage Device"
   - Or "Ventoy"
   - Or your drive brand name
5. Press **Enter**

**Method 2: Change Boot Order in BIOS**

1. Enter BIOS (see Step 10)
2. Go to **"Boot"** tab
3. Move **"USB Device"** to first position
4. Save and exit
5. Computer will boot from USB automatically

### Step 14: Navigate Ventoy Menu

1. **Ventoy boot menu appears** (purple/blue screen with list of ISOs)
2. **Use arrow keys** to highlight the distro you want
3. **Press Enter** to boot
4. Each distro will show its own boot menu with options

**First Time Boot Order:**
- Start with **Puppy Linux** (easiest to learn)
- Then **Tails** (privacy focused)
- Then **Kali Linux** (security tools)
- Finally **Kali Purple** (defensive security)

---

## Troubleshooting Guide

### Problem: "Security Policy Violation" or MOK Error

**Symptoms:**
- Error message about "Security Policy Violation"
- Mention of "MOK" or "Shim"
- System refuses to boot

**What This Is:**
- MOK = Machine Owner Key
- Part of Secure Boot system
- Ventoy needs to be "trusted" by your computer's Secure Boot

**Solution Option 1: Disable Secure Boot (Recommended)**

1. Restart and enter BIOS (ESC → F10 on HP)
2. Navigate to **Security → Secure Boot Configuration**
3. Verify **"Secure Boot"** is **"Disabled"**
4. Save and exit (F10)
5. Try booting again

**Solution Option 2: Enroll MOK Key (Keep Secure Boot Enabled)**

If you want to keep Secure Boot enabled, follow these steps:

**When MOK Management Screen Appears:**

1. **Select "Enroll key from disk"** (NOT "Enroll MOK")
2. Navigate to your USB drive (should show "Ventoy" or similar)
3. Look for the Ventoy certificate file:
   - File name: `ENROLL_THIS_KEY_IN_MOKMANAGER.cer`
   - Or: `ventoy.cer`
   - May be in root directory or `/EFI/BOOT/` folder
4. Press Enter to select the file
5. Select **"Continue"**
6. Confirm **"Yes"** to enroll
7. Select **"Reboot"**
8. USB should now boot successfully

**If MOK Key File is Missing:**

1. You need to reinstall Ventoy with Secure Boot support:
   - Run Ventoy2Disk.exe as Administrator
   - Click **"Option"** button
   - Check **"Secure Boot Support"** option
   - Reinstall to USB (will erase data)
   - Copy ISOs back to USB
2. Try booting again - MOK enrollment screen should appear

**Reference:**
- Official Ventoy Secure Boot Guide: https://www.ventoy.net/en/doc_secure_boot.html
- Contains detailed MOK enrollment instructions with screenshots

### Problem: "SBAT" Error and Automatic Shutdown

**Symptoms:**
- Error mentions "SBAT"
- Message says "Something went seriously wrong"
- Computer shuts down automatically
- Happens with Puppy Linux specifically

**Why This Happens:**
- SBAT (Secure Boot Advanced Targeting) is a newer security mechanism
- Puppy Linux doesn't support SBAT
- Only solution is disabling Secure Boot

**Solution:**
1. You **MUST** disable Secure Boot (see Step 11)
2. There is no workaround for SBAT without disabling Secure Boot
3. This is normal for older/smaller distros like Puppy

### Problem: BitLocker Recovery Key Required

**Symptoms:**
- After disabling Secure Boot, Windows asks for BitLocker recovery key
- Blue screen with key entry prompt

**Solution:**
1. If you have the recovery key:
   - Enter it to unlock Windows
   - Then disable BitLocker (see Step 9)
   - Reboot and disable Secure Boot again
   
2. If you don't have the recovery key:
   - Check your Microsoft account online for the key
   - Check printed documentation from when BitLocker was enabled
   - May need to recover/reinstall Windows if key is lost

**Prevention:**
Always disable BitLocker **BEFORE** changing Secure Boot settings.

### Problem: USB Drive Not Detected in Boot Menu

**Solutions to try:**

1. **Try different USB ports:**
   - Use USB 3.0 ports (usually blue inside)
   - Try ports directly on computer (not USB hub)
   - Try both front and back ports on desktop

2. **Enable USB Boot in BIOS:**
   - Enter BIOS
   - Look for "USB Boot" or "Boot from USB" setting
   - Ensure it's **Enabled**
   - Save and restart

3. **Change USB Boot Priority:**
   - Enter BIOS → Boot tab
   - Move "USB Device" higher in boot order
   - Save and restart

4. **Try Legacy Boot Mode:**
   - Enter BIOS
   - Find "Boot Mode" or "UEFI/Legacy Boot"
   - Try switching between UEFI and Legacy
   - Save and test

### Problem: Ventoy Menu Doesn't Appear

**Symptoms:**
- Computer boots normally to Windows/existing OS
- Or shows "No bootable device"

**Solutions:**

1. **Reinstall Ventoy:**
   - Run Ventoy2Disk.exe as administrator
   - Click "Option" → Try **MBR** partition style instead of GPT
   - Reinstall to USB
   - Copy ISOs again

2. **Verify ISOs are on USB:**
   - Open USB drive in File Explorer
   - Confirm .iso files are visible
   - Confirm they're in root directory or subfolders

3. **Check USB drive format:**
   - Right-click USB in File Explorer → Properties
   - Should show "exFAT" file system
   - If not, reinstall Ventoy

### Problem: Specific Distro Won't Boot

**Symptoms:**
- Ventoy menu works
- But selected distro fails to load or shows errors

**Solutions:**

1. **Re-download ISO file:**
   - Corrupt downloads happen
   - Delete old ISO from USB
   - Download fresh copy from official site
   - Copy to USB again

2. **Verify ISO checksum:**
   - Most distro sites provide SHA256 checksums
   - Use Windows PowerShell:
     ```powershell
     Get-FileHash -Path "C:\path\to\file.iso" -Algorithm SHA256
     ```
   - Compare result to official checksum

3. **Try different Ventoy boot mode:**
   - At Ventoy menu, look for boot mode options (F1, F2, F3 keys)
   - Try "Normal mode" vs "GRUB2 mode"

### Problem: Persistence Not Working

**Symptoms:**
- Changes don't save between reboots
- Installed software disappears
- Files don't persist

**Solutions:**

1. **Select correct boot option:**
   - When booting Kali, choose **"Live system (persistence)"**
   - NOT just "Live system"
   - Persistence option must be explicitly selected

2. **Verify persistence file exists:**
   - Open USB drive in File Explorer
   - Look for files like "persistence-kali" or similar
   - If missing, recreate using VentoyPlugson (Step 8)

3. **Check file naming:**
   - Persistence file name must match ISO name
   - Example: "kali-linux-2024.iso" needs "persistence-kali-linux-2024"

### Problem: Slow Performance

**Symptoms:**
- Distros run very slowly
- Applications take long to open
- General sluggishness

**Solutions:**

1. **Verify USB 3.0:**
   - Check USB drive packaging (should say USB 3.0, 3.1, or higher)
   - Use USB 3.0 port on computer (blue port or SS marking)
   - USB 2.0 is significantly slower

2. **Check available RAM:**
   - Linux live systems run in RAM
   - Minimum 4GB RAM recommended
   - 8GB+ ideal

3. **Reduce background programs:**
   - Close unnecessary applications
   - Free up RAM for the live system

4. **Consider dual-boot for daily use:**
   - Live USB is for learning/testing
   - Full installation on hard drive is much faster

### Problem: Can't Return to Windows

**Symptoms:**
- Computer always boots to USB now
- Can't access Windows

**Solution:**
1. Remove USB drive
2. Restart computer
3. Computer should boot to Windows normally

If still not working:
1. Enter BIOS
2. Change boot order back to "Windows Boot Manager" first
3. Save and exit

### Problem: "Not Enough Space" When Creating Persistence

**Symptoms:**
- VentoyPlugson gives error about space
- Can't create 8GB persistence file

**Solutions:**

1. **Check free space:**
   - Open USB drive properties
   - Verify actual free space
   - ISOs take up significant space

2. **Reduce persistence size:**
   - Try 4GB instead of 8GB for Kali
   - Try 2GB for Kali Purple
   - Can always increase later

3. **Use larger USB drive:**
   - 32GB fills up quickly with 4 distros + persistence
   - Consider 64GB+ USB drive for more comfortable space

---

## Tips for Success

**Best Practices:**

- ✓ Always **"Safely Remove Hardware"** before unplugging USB
- ✓ Keep original ISO files backed up on your computer
- ✓ Update ISOs every few months for latest security tools
- ✓ Test booting on your computer before relying on it
- ✓ Keep your BitLocker recovery key in a safe place
- ✓ Document your BIOS changes in case you need to revert

**Security Reminders:**

- ✗ Never use security tools on systems without permission
- ✗ Don't practice attacks on real networks or systems
- ✓ Use vulnerable VMs for practice (Metasploitable, DVWA)
- ✓ Keep learning ethical and legal


## Additional Resources

### Official Documentation

**Ventoy Resources:**
- **Secure Boot Support Guide:** https://www.ventoy.net/en/doc_secure_boot.html
  - Detailed MOK enrollment instructions
  - Screenshots of MOK management process
  - Troubleshooting for Secure Boot issues
- **Getting Started:** https://www.ventoy.net/en/doc_start.html
- **Persistence Plugin:** https://www.ventoy.net/en/plugin_persistence.html
- **FAQ:** https://www.ventoy.net/en/faq.html
- **Video Tutorials:** https://www.ventoy.net/en/screenshot.html

**Linux Distribution Documentation:**
- Puppy Linux Wiki: https://puppylinux.com/wiki
- Tails Documentation: https://tails.boum.org/doc/
- Kali Documentation: https://www.kali.org/docs/
- Kali Purple Guide: https://www.kali.org/blog/kali-linux-2023-1-release/#kali-purple

---

**Document Version:** 2.0  
**Last Updated:** October 2024  
**Tested On:** Windows 10, Windows 11, HP Hardware
