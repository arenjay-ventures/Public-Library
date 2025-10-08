---
layout: default
title: Disk Cleanup
parent: Tutorials
nav_order: 1
---

# Disk Cleanup – Preparing for a media server

## Tutorial Information

**Title:** Disk Cleanup – Preparing for a media server  
**Author:** Justin  
**Date Created:** 2024-10-08  
**Last Updated:** 2024-10-08  
**Difficulty Level:** Beginner  
**Estimated Time:** 2-4 hours  
**Prerequisites:** Windows computer, administrator access

---

## Overview

### What You'll Learn
- How to identify and remove large system files
- How to manage Windows hibernation and virtual memory
- How to find and remove duplicate files
- How to set up BitLocker encryption
- How to use disk management tools effectively

### What You'll Build
A clean, optimized Windows system with proper disk management and security settings

### Technologies Used
- Windows PowerShell
- BitLocker encryption
- Disk management tools (WinDirStat, Tree Size, Everything)
- Windows built-in disk cleanup utilities

---

## Prerequisites

### Required Knowledge
- Basic understanding of Windows file system
- Familiarity with Windows settings and control panel
- Experience with file management

### Required Tools
- Windows computer with administrator access
- Disk analysis tools (WinDirStat, Tree Size Free, Everything 1.5a)
- Internet connection for downloading tools

### System Requirements
- **Operating System:** Windows 10/11
- **RAM:** 4GB minimum
- **Storage:** Sufficient free space for analysis
- **Internet:** Connection for downloading tools

---

## Step-by-Step Instructions

### Step 1: Initial Disk Analysis
**Objective:** Identify large files and unused programs taking up space

I used the tools listed in the Disk Management and System Tools to inspect, review, consolidate file and clean up multiple Hard Drives in preparation for moving media to a Media Server, and to clean up operations on my main computers as well.

I started by sorting by file size in WinDirStat.

Found the largest files were LLM files used with LMStudio. Which I do use, but can move to a faster drive for better performance.

The next largest files were related to ComfyUI, another AI program that I am not using anymore. So I uninstalled it then checked to confirm files deleted. Found ~6.6GB of residual files to remove manually.

**Expected Result:** You should have a clear picture of what's taking up space on your drives

**Troubleshooting:**
- **Issue:** Tools show system drive only
  - **Solution:** Use tools that can scan multiple drives or run from different locations

---

### Step 2: Remove Hibernation File (hiberfil.sys)
**Objective:** Free up space by removing unnecessary hibernation file

When consolidating hard drive data I came across the VERY large file of hiberfil.sys. This file holds a snapshot of the RAM image for hibernating the computer and allowing a faster start up from where the user left off. This file is NOT encrypted unless using system drive level encryption such as BitLocker is enabled.

If we are not using the hibernate feature (I don't) it is a unneeded waste of space for the very large file.
If we are not using BitLocker on the system drive of the computer, then it is susceptible to extraction from a physical attack.
We can turn it off and it will automatically delete the file as well. I may turn it back on after hard drives are cleaned up and BitLocker installed.

1. Open Windows PowerShell as an Administrator
2. Type the command `powercfg /h off` and press Enter
3. Hibernation will be turned off and the hiberfil.sys file will be automatically deleted.

To turn it back on follow same directions with command: `powercfg /h on`

**Expected Result:** The hiberfil.sys file will be removed, freeing up significant disk space

**Troubleshooting:**
- **Issue:** Command not recognized
  - **Solution:** Make sure you're running PowerShell as Administrator

---

### Step 3: Manage Virtual Memory (pagefile.sys and swapfile.sys)
**Objective:** Optimize virtual memory settings for your system

This file can get very large and is indicative of the computer using a lot of virtual memory. My file was not ridiculously large, but we will check its settings anyways. I recently doubled the available RAM and may be able to adjust the max settings down.

1. Open File Explorer, right-click This PC, select Properties, then Advanced System Settings.
2. Go to the Advanced Tab, click Settings under Performance, and then select the Advanced tab again
3. Under Virtual Memory, click Change, then uncheck Automatically manage page file size for all drives.
4. Select your drive, choose Custom Size, and enter manual size.

Won't Take Effect until after Reboot.

There is an option to not use a paging file. This is not recommended in general user settings.

*Note: I made no adjustments for my situation*

**Expected Result:** Optimized virtual memory settings for your system

**Troubleshooting:**
- **Issue:** Changes don't take effect
  - **Solution:** Restart your computer for changes to apply

---

### Step 4: Remove Chrome Gemini Nano Weights
**Objective:** Remove large AI model files from Chrome browser

Also located a large 1.3GB file called weights.bin
After some online research I determined this is the model weights file for a Gemini Nano LLM built in to Chrome Browser.

Source: chrome://flags/#prompt-api-for-gemini-nano

1. Go to the link above in chrome browser
2. Change drop down selection to "Disabled"

Can also set to Disabled the following:

- Prompt API for Gemini Nano
- Prompt API for Gemini Nano with Multimodal Input
- Summarization API for Gemini Nano
- Writer API for Gemini Nano
- Proofreader API for Gemini Nano

3. Click Relaunch, or close and Relaunch Chrome
4. Restart, manually delete the file if not removed.

*Result: This worked for me and I removed the 1.3GB file along with another one in the same folder that was related (didn't catch the name) total removed was 2.7GB.*

**Expected Result:** Chrome AI features disabled and large model files removed

**Troubleshooting:**
- **Issue:** Files still present after disabling
  - **Solution:** Manually delete the files after restarting Chrome

---

### Step 5: Set Up BitLocker Encryption
**Objective:** Enable full disk encryption for security

BitLocker is full hard disk encryption native to Windows. It requires a Recovery Key, and therefore is often OFF when shipped with a new computer. It must be turned on and a recovery key created by the new user.

I checked on a computer that came with Windows pre-installed and determined BitLocker had never been set up…so these are the steps to set it up.

1. In windows search, type Manage BitLocker (select it)
2. In the BitLocker Drive Encryption page, you can see which drive volumes have BitLocker on or not.
3. Select the Drive you want to Encrypt
4. Create you recovery key, either save the file, print the key, etc (**KEEP SAFE NEVER LOSE**)
5. Select whether you want to Encrypt used disk space only (for a new computer or drive) OR Encrypt entire drive
6. Select Encryption mode (explanation is provided)
7. Select "Run BitLocker system check" (we don't want a small issue to make us lose access to EVERYTHING)
8. Computer will Restart
9. log back in: computer may appear normal, opening BitLocker again it will not say "BitLocker Encrypting" This may take a while if a large drive.

**Expected Result:** Full disk encryption enabled with recovery key saved

**Troubleshooting:**
- **Issue:** BitLocker not available
  - **Solution:** Check if your computer supports TPM (Trusted Platform Module)

---

### Step 6: Final Cleanup and Optimization
**Objective:** Perform final disk cleanup and error checking

From file explorer we can a few utilities to cleanup and double check no errors on the disk. Typically not needed, but given the large amount of files moved and number of changes it is a good practice.

1. Open Windows File Explorer
2. Right click on the drive you want to clean up
3. under General tab, select Disk Cleanup
4. wait until completed…then select Clean system files, then when complete select file types you feel comfortable removing, select Okay, Select Delete Permanently
5. Under Tools tab, "Error Checking" select Check, select Scan Drive
6. Last run Optimize, this may not be recommended for SSD drive, so check what you are using.

Optimize drive screen will come up to select the drive, Analyze if there are issues, the Optimize if you choose too, you can also set a schedule for regular checks.

*Note: My files were fine even after all the files being moved so optimize was not run in my case*

**Expected Result:** Clean, optimized drives with no errors

**Troubleshooting:**
- **Issue:** Optimization not recommended for SSD
  - **Solution:** Check your drive type - SSDs don't need defragmentation

---

## Duplicate File Management

### Step 7: Find and Remove Duplicate Files
**Objective:** Identify and remove duplicate files to free up space

It appears the name may have changed so I put both here.
Download and run setup, I ran with "Start scan after installation"

It may ask to install additional components to see previews of RAW files. We may have some photos in RAW format so I selected "Yes".

**Disappointment:**
It only allowed search the main PC drive, and wanted monetary upgrade for additional features and a separate program for reviewing photos. Not the experience I remembered from previous use…removed a couple small files, and uninstalled.

I moved the setup.exe file for the program to a different drive and used Task Manager to kill all processes from the previous version. Then reinstalled in the new location.
Attempting to see if it checks the drive it is on, or just the system drive…it checked the system drive only.

*Removing - won't use again*

### Tree Size Free

Installed new program to try, fast install and setup, very fast file search.
VERY FAST SCAN OF A DRIVE.
Can select a different drive under "Select Directory"

This is faster and very similar to WinDirStat, I will probably use this one in the future.

*Note: Not seeing where I can search for duplicates…*

### UltraSearch Free

From same company as Tree Size, Installed new program to try, fast install and setup, very fast file search.
I can see the use, especially the Pro version that can search inside of Zip files.
Free does not appear to have duplicate search enabled.

*Uninstalled*

### Everything 1.5a

Installed new program to try, fast install and setup, very fast file search.
Has a right click on header to search for duplicates by type (name, length, size etc)

*This is great!*
Found a total of 3.4GB additional duplicates, mainly .pdf and .mp3 files
Removed then, ran clean up again.
Will dump recycle bin and restart.

---

## Summary

### What You Accomplished
Successfully cleaned up multiple hard drives, removed large system files, enabled encryption, and optimized disk usage in preparation for media server setup.

### Key Takeaways
- System files like hiberfil.sys can take up significant space
- Chrome AI features download large model files
- BitLocker encryption is essential for security
- Multiple tools may be needed to find all duplicate files
- Everything 1.5a is the most effective duplicate finder

### Skills Developed
- Disk space analysis and management
- Windows system optimization
- Security configuration with BitLocker
- Duplicate file detection and removal
- System maintenance best practices

---

## Additional Resources

### Documentation
- [Windows Disk Cleanup](https://support.microsoft.com/en-us/windows/disk-cleanup-in-windows-10-8a96ff42-5751-39ad-23d6-859b934a1b4b)
- [BitLocker Documentation](https://docs.microsoft.com/en-us/windows/security/information-protection/bitlocker/)
- [Windows Virtual Memory](https://docs.microsoft.com/en-us/windows/client-management/introduction-to-configuring-virtual-memory)

### Tools & Extensions
- [WinDirStat](https://windirstat.net/) - Disk usage statistics
- [Tree Size Free](https://www.jam-software.com/treesize_free) - Disk space analysis
- [Everything 1.5a](https://www.voidtools.com/forum/viewtopic.php?t=9787#new) - (Specifically 1.5a) File search and duplicate detection

### Community Support
- [Windows Support Forums](https://answers.microsoft.com/en-us/windows)
- [Reddit r/Windows10](https://www.reddit.com/r/Windows10/)
- [Stack Overflow Windows](https://stackoverflow.com/questions/tagged/windows)

---

**Tutorial Created By:** Justin  
**Contact:** Available through portfolio  
**Last Updated:** 2024-10-08  
**Version:** 1.0

