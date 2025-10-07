---
layout: default
title: DISK CLEANUP
parent: references/tutorials
nav_order: 1
##**DISK CLEANUP – Preparing for a media server**

### ** Project Disk Cleanup**
*   This page detials the tools used for disk management. Most have their own tutorials or directions that update with versions. So instead of re-writing tutorials, I will consolidate what was used along with personal notes on the use regarding issues and utility of the tool.

A complete list of the tools can be found at the references/tools-and-tech page under Disk Management and System Tools

### **3. The Implementation & Process**
*   **(Bulleted list or short paragraphs)** Detail the key steps you took to build the solution. This is where you showcase your technical process. Focus on the "how" and "why" of your decisions.
*   *Example Step 1: **Infrastructure Setup.** Deployed three Ubuntu Server VMs in VirtualBox, configured with a host-only network to simulate an isolated corporate environment.*
*   *Example Step 2: **SIEM Installation.** Installed and configured a Wazuh server on the primary monitoring VM, ensuring agent communication ports were correctly firewalled.*
*   *Example Step 3: **Log Ingestion & Testing.** Deployed Wazuh agents to the target VMs. Generated test traffic using Nmap from a Kali Linux VM to verify that logs were being collected and that basic intrusion detection rules were firing correctly.*

---

### **ACTIONABLE STEPS FOR CLEAN-UP**
*   **Using the tools:**  I used the tools listed listed in the Disk Management and System Tools to inspect, review, consolidate file and clean up multiple Hard Drives in preparation for moving media to a Media Server, and to clean up operations on my main computers as well.
---
### **hiberfil.sys**
*   When consolidating hard drive data I came across the VERY large file of hiberfil.sys. This file holds a snapshot of the RAM image for hibernating the computer and allowing a faster start up from where the user left off. This file is NOT encrypted  unless using system drive level encryption such as BitLocker is enabled.

If we are not using the hibernate feature (I don’t) it is a unneeded waste of space for the very large file.
If we are not using BitLocker on the system drive of the computer, then it is susceptible to extraction from a physical attack.
We can turn it off and it will automatically delete the file as well. I may turn it back on after hard drives are cleaned up and BitLocker installed.

STEPS TO COMPLETE: 
1: Open Windows PowerShell as an Administrator
2: Type the command 
	powercfg /h off

and press Enter

3: Hibernation will be turned off and the hiberfil.sys file will be automatically deleted.
To turn it back on follow same directions with command: powercfg /h on
---
### **pagefile.sys and swapfile.sys**
*   This file can get very large and is indicative of the computer using a lot of virtual memory. My file was not ridiculously large, but we will check its settings anyways. I recently doubled the available RAM and may be able to adjust the max settings down.

STEPS TO COMPLETE: Disable automatic management:
1: Open File Explorer, right-click This PC, select Properties, then Advanced System Settings.
2: Go to the Advanced Tab, click Settings under Performance, and then select the Advanced tab again
3: Under Virtual Memory, click Change, then uncheck Automatically manage page file size for all drives.
4: Select your drive, choose Custom Size, and enter manual size.
Won’t Take Effect until after Reboot.

There is an option to not use a paging file. This is not recommended in general user settings.

**I made no adjustments for my situation**
---

### **LARGE unused programs**
*   **Locating large Programs** I started by sorting by file size in WinDirStat. 

Found the largest files were LLM files used with LMStudio. Which I do use, but can move to a faster drive for better performance.

The next largest files were related to ComfyUI, another AI program that I am not using anymore. So I uninstalled it then checked to confirm files deleted. Found ~6.6GB of residual files to remove manually.
---

### **weights.bin **
*   Also located a large 1.3GB file called weights.bin
After some online research I determined this is the model weights file for a Gemini Nano LLM built in to Chrome Browser. 

Source: chrome://flags/#prompt-api-for-gemini-nano

STEPS TO COMPLETE TO DISABLE AND REMOVE: 
1: go to the link above in chrome browser
2: change drop down selection to “Disabled”

Can also set to Disabled the following:

Prompt API for Gemini Nano
Prompt API for Gemini Nano with Multimodal Input
Summarization API for Gemini Nano
Writer API for Gemini Nano
Proofreader API for Gemini Nano

3: Click Relaunch, or close and Relaunch Chrome

4: Restart, manually delete the file if not removed.

**This worked for me and I removed the 1.3GB file along with another one in the same folder that was related (didn’t catch the name) total removed was 2.7GB .**
---
### **BitLocker Check**
*   **BitLocker** BitLocker is full hard disk encryption native to Windows. It requires a Recovery Key, and therefore is often OFF when shipped with a new computer. It must be turned on and a recovery key created by the new user.

I checked on a computer that came with Windows pre-installed and determined BitLocker had never been set up…so these are the steps to set it up.

STEPS TO CHECK AND SET UP:
1: In windows search, type Manage BitLocker (select it)
2: In the BitLocker Drive Encryption page, you can see which drive volumes have BitLocker on or not.
3: Select the Drive you want to Encrypt
4: Create you recovery key, either save the file, print the key, etc (**KEEP SAFE NEVER LOSE**
5: Select whether you want to Encrypt used disk space only (for a new computer or drive) OR Encrypt entire drive
6: Select Encryption mode (explanation is provided)
7: Select “Run BitLocker system check” (we don’t want a small issue to make us lose access to EVERYTHING)
8: Computer will Restart
9: log back in: computer may appear normal, opening BitLocker again it will not say “BitLocker Encrypting” This may take a while if a large drive.

### **LAST CLEAN UP STEPS**
*   **Disk Cleanup** From file explorer we can a few utilities to cleanup and double check no errors on the disk. Typically not needed, but given the large amount of files moved and number of changes it is a good practice.

STEPS TO TAKE:
1: Open Windows File Explorer
2: Right click on the drive you want to clean up
3: under General tab, select Disk Cleanup
4: wait until completed…then select Clean system files, then when complete select file types you feel comfortable removing, select Okay, Select Delete Permanently
5: Under Tools tab, “Error Checking” select Check, select Scan Drive
6: Last run Optimize, this may not be recommended for SSD drive, so check what you are using. 
Optimize drive screen will come up to select the drive, Analyze if there are issues, the Optimize if you choose too, you can also set a schedule for regular checks.
**MY FILES WERE FINE EVEN AFTER ALL THE FILES BEING MOVED SO OPTIMIZE WAS NOT RUN IN MY CASE**
---

### **Duplicate Files Search**
*   **dupeGuru: Duplicate Files Fixer** It appears the name may have changed so I put both here.
Download and run setup, I ran with “Start scan after installation”

It may ask to install additional components to see previews of RAW files. We may have some photos in RAW format so I selected “Yes”.

**DISAPPOINTMENT**
It only allowed search the main PC drive, and wanted monetary upgrade for additional features and a separate program for reviewing photos. Not the experience I remembered from previous use…removed a couple small files, and uninstalled.

I moved the setup.exe file for the program to a different drive and used Task Manager to kill all processes from the previous version. Then reinstalled in the new location.
Attempting to see if it checks the drive it is on, or just the system drive…it checked the system drive only.

**REMOVING - WONT USE AGAIN**

---
### **Tree Size Free**
*   ** Tree Size ** Installed new program to try, fast install and setup, very fast file search.
VERY FAST SCAN OF A DRIVE.
Can select a different drive under “Select Directory”

This is faster and very similar to WinDirStat, I will probably use this one in the future.

**Not seeing where I can search for duplicates…**
---
### **UltraSearch Free**
*   ** UltraSearch** From same company as Tree Size, Installed new program to try, fast install and setup, very fast file search.
I can see the use, especially the Pro version that can search inside of Zip files.
Free does not appear to have duplicate search enabled.

**UNINSTALLED** 
---
### **Everything 1.5a**
*   ** Everything ** Installed new program to try, fast install and setup, very fast file search.
Has a right click on header to search for duplicates by type (name, length, size etc)

**THIS IS GREAT**
Found a total of 3.4GB additional duplicates, mainly .pdf and .mp3 files
Removed then, ran clean up again.
Will dump recycle bin and restart. 
---





