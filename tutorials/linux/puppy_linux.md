---
layout: default
title: Tails Linux Mastery Guide
parent: Linux
nav_order: 3
---

# Tails Linux Mastery Guide
## A Complete One-Day Journey to Anonymous and Secure Computing

**Download/Print Version:** [Day 1: Puppy Linux Mastery Guide PDF](Day%201_%20Puppy%20Linux%20Mastery%20Guide.pdf)

---

## Introduction: Why Tails?

Tails (The Amnesic Incognito Live System) represents a completely different philosophy than Puppy Linux. While Puppy optimizes for speed and efficiency, Tails optimizes for **privacy, anonymity, and security above all else**.

**What Makes Tails Unique:**
- Forces all internet traffic through Tor network
- Leaves no trace on the computer you use it on
- Uses state-of-the-art cryptographic tools
- Amnesia by default (forgets everything on shutdown)
- Designed for activists, journalists, and privacy-conscious users
- Endorsed by Edward Snowden and privacy advocates worldwide

**Today's Learning Goals:**
- Understand the Tor network and how it protects you
- Master anonymous browsing and communication
- Learn encryption fundamentals (files, messages, email)
- Configure persistent storage securely
- Recognize surveillance and tracking techniques
- Use Tails for real-world privacy scenarios
- Understand the threat models Tails protects against

**Time Required:** 6-8 hours (with breaks)

**Critical Context:**
Tails isn't just a tool—it's a complete security environment. Every feature serves a privacy purpose. Today, you'll learn not just *how* to use Tails, but *why* each feature matters and when you need them.

---

## Morning Session (8:00 AM - 12:00 PM)

### Hour 1: Understanding Threat Models and Privacy (8:00 - 9:00 AM)

Before using Tails, you must understand what it protects against—and what it doesn't.

#### What is a Threat Model?

**Definition:** A threat model identifies:
- **Who** might want to surveil you (adversaries)
- **What** they want to learn (information at risk)
- **How** they might attack you (attack vectors)
- **What** you're protecting (assets)

**Exercise 1: Personal Threat Assessment (20 minutes)**

Before booting Tails, think through these scenarios:

**Scenario A: Casual Privacy**
- **Adversary:** Advertisers, data brokers, tech companies
- **Goal:** Build profile for targeted ads, sell your data
- **Methods:** Cookies, trackers, browser fingerprinting
- **Protection needed:** Moderate (Tor Browser, tracker blocking)

**Scenario B: Investigative Journalism**
- **Adversary:** Government agencies, corporations being investigated
- **Goal:** Identify sources, prevent publication
- **Methods:** Network surveillance, device seizure, legal pressure
- **Protection needed:** High (Tails, encryption, OpSec discipline)

**Scenario C: Activist Organizing**
- **Adversary:** Authoritarian governments, opposition groups
- **Goal:** Identify organizers, disrupt movement
- **Methods:** Mass surveillance, metadata analysis, informants
- **Protection needed:** Very high (Tails, air-gapped systems, physical security)

**Scenario D: Whistleblowing**
- **Adversary:** Resourced organizations with legal power
- **Goal:** Identify whistleblower, prosecute, discredit
- **Methods:** All available surveillance, forensics, legal discovery
- **Protection needed:** Maximum (Tails, physical anonymity, opsec perfection)

**Write down:**
1. Which scenario closest matches why you're learning Tails?
2. What information do you want to protect?
3. Who might want that information?
4. What could they do with it?

**Understanding Tails' Protection Scope:**

**Tails DOES protect against:**
- ✓ Network surveillance of your internet traffic
- ✓ Website tracking and profiling
- ✓ Digital traces on the computer you're using
- ✓ Routine traffic analysis
- ✓ Commercial tracking and data collection
- ✓ Most government mass surveillance programs

**Tails DOES NOT protect against:**
- ✗ Targeted attacks against you specifically
- ✗ Physical surveillance (cameras, keyloggers)
- ✗ Compromised hardware (pre-installed malware)
- ✗ Your own mistakes (revealing identity in messages)
- ✗ Correlation attacks (advanced traffic analysis)
- ✗ Legal compulsion to reveal identity
- ✗ Physical device seizure after use

**The Critical Understanding:**
Tails is a **tool**, not magic. It provides technical protection, but you must provide **operational security** (OpSec). Your behavior matters as much as the technology.

#### How Tails Achieves Anonymity

**The Tor Network:**

```
You → Entry Guard → Middle Relay → Exit Relay → Website
     (encrypted) (encrypted) (decrypted) (sees exit IP)
```

**Key Principles:**

1. **Encryption Layers:** Your traffic is encrypted three times
   - Like an onion (hence "The Onion Router")
   - Each relay only sees previous and next relay
   - No single point knows both source and destination

2. **Random Path:** Each connection takes different route
   - Makes pattern analysis extremely difficult
   - Protects against single compromised relay

3. **Exit Node Anonymity:** Website sees exit node, not you
   - Your IP address is hidden
   - Your location is hidden
   - But: Exit node can see unencrypted traffic (use HTTPS!)

**Exercise 2: Tor Visualization (15 minutes)**

Draw or diagram:
1. Your normal internet connection path
   ```
   You → ISP → Website
   ```
   - ISP sees: Your IP, destination, timing
   - Website sees: Your IP, location, identity
   
2. Your Tor connection path
   ```
   You → Entry → Middle → Exit → Website
   ```
   - Entry sees: Your IP (but not destination)
   - Middle sees: Only relay IPs
   - Exit sees: Destination (but not your IP)
   - Website sees: Only exit node IP

**Why This Matters:**
Understanding Tor's architecture helps you understand its limitations. Tor protects the path, but you must protect the endpoints (your behavior).

#### Amnesia: The Live System Concept

**What "Amnesic" Means:**

Every time you shut down Tails:
- **RAM is wiped** (contains all your session data)
- **No trace remains** on the host computer
- **Next boot is fresh** (like it never happened)

**Why This Matters:**

Traditional operating systems leave evidence:
- Browser history (even "private mode")
- File system artifacts
- Registry entries (Windows)
- Temporary files
- Swap file data
- Thumbnail caches

**Tails leaves none of this** because:
- Runs entirely in RAM
- Never writes to host system drive
- Secure deletion of sensitive data
- RAM is volatile (loses data when powered off)

**The Trade-Off:**
Amnesia means **nothing persists** unless you explicitly configure it. This is intentional—default to forgetting everything is safest.

---

### Hour 2: First Boot and Initial Configuration (9:00 - 10:00 AM)

#### Booting Tails

1. **Select Tails from Ventoy menu**
2. **Tails Boot Menu appears:**
   - "Tails" - Normal boot
   - "Tails (Troubleshooting Mode)" - If normal boot fails
   - "Tails (External Hard Disk)" - For some hardware

3. **Choose "Tails"** and press Enter

**What's Happening:**
- Tails is loading into RAM
- Checking hardware compatibility
- Initializing security features
- **This takes longer than Puppy** (2-5 minutes normal)

#### Welcome Screen

**The Welcome to Tails Screen appears with critical options:**

**Language and Region:**
- Select your language
- Choose keyboard layout
- **Privacy consideration:** Use English if possible (less fingerprintable)

**Additional Settings (click + icon):**

1. **Administration Password:**
   - **What it is:** Sudo password for this session
   - **When needed:** Installing software, system changes
   - **Set it:** Check "Enable" and create strong password
   - **Security note:** Only exists for this session

2. **MAC Address Anonymization:**
   - **What it is:** Changes your network card's ID
   - **Why:** MAC addresses are unique and trackable
   - **Recommendation:** Leave enabled (default)
   - **When to disable:** Some networks block MAC spoofing

3. **Offline Mode:**
   - **What it is:** Start without network connection
   - **When to use:** Working with sensitive files locally
   - **Why:** Prevents accidental network exposure

4. **Unsafe Browser:**
   - **What it is:** Firefox without Tor (direct internet)
   - **When to use:** Captive portals (hotel/airport WiFi login)
   - **Why provided:** Some networks require login before Tor works
   - **Danger:** Reveals your real IP—use only when necessary

**Exercise 3: Secure Initial Configuration (15 minutes)**

**Your first boot checklist:**

1. **Language:** English (most anonymous)
2. **Keyboard:** Your actual layout (usability matters)
3. **Administration Password:** ✓ Enable with strong password
4. **MAC Anonymization:** ✓ Keep enabled
5. **Offline Mode:** ✗ Leave disabled (we need network today)
6. **Unsafe Browser:** ✗ Leave disabled (we don't need it now)

**Click "Start Tails"**

**Wait for desktop to load:**
- Background connects to Tor network
- System initializes security features
- This takes 1-3 minutes after desktop appears

**Tor Connection Notification:**
- Watch for "Connected to Tor successfully"
- Green onion icon in system tray = Connected
- Until this appears, no internet access

#### Understanding the Tails Desktop

**Desktop Environment: GNOME**
- More polished than Puppy's lightweight interface
- Organized "Activities" menu (top-left)
- System status indicators (top-right)
- Application dock (left side, appears on hover)

**Critical Desktop Elements:**

**Top Bar:**
- **Activities** (left): Access all applications
- **Date/Time** (center): Current UTC or local time
- **System Icons** (right):
  - Onion icon (Tor status)
  - Network icon
  - Sound icon
  - Power menu

**Important Applications:**

**Activities → show all applications:**
- **Tor Browser:** Your gateway to anonymous internet
- **Thunderbird:** Email client with OpenPGP support
- **KeePassXC:** Password manager
- **OnionShare:** Anonymous file sharing
- **MAT2:** Metadata removal tool
- **Electrum:** Bitcoin wallet
- **Files:** File manager

**Notice What's Missing:**
- No standard Firefox (only Tor Browser)
- No Chrome, Edge, or other browsers
- Limited application selection (intentional)
- Only privacy-preserving tools included

**Why This Matters:**
Every application in Tails is chosen for security. Random software installation could compromise anonymity. This curated approach is a feature, not a limitation.

**Exercise 4: Desktop Familiarization (15 minutes)**

1. **Explore Activities menu:**
   - Click "Activities"
   - Browse available applications
   - Notice security-focused selections

2. **Check Tor Connection:**
   - Click onion icon (top-right)
   - Read Tor circuit information
   - Understand: Entry, Middle, Exit relays

3. **Open Files (file manager):**
   - Notice: Limited directory structure
   - Home folder is empty (clean slate)
   - Amnesia sidebar (persistent storage not yet configured)

4. **System Settings:**
   - Activities → Settings
   - Browse available options
   - Notice: Some settings are locked/simplified (security)

---

### Hour 3: Anonymous Browsing with Tor Browser (10:00 - 11:00 AM)

#### Tor Browser Fundamentals

**What Makes Tor Browser Different:**
- Routes traffic through Tor network
- Resists fingerprinting (makes you look like everyone else)
- Blocks trackers and cookies by default
- Disables JavaScript on high security
- Isolates tabs and websites
- Clears everything on close

**Launch Tor Browser:**
- Activities → Tor Browser
- Or click "Tor Browser" icon in dock
- Wait for connection (usually immediate if Tor already connected)

**First Launch:**
- "Tor Browser is ready"
- Notice: DuckDuckGo is default search engine (privacy-respecting)
- URL bar shows .onion availability when applicable

#### Tor Browser Security Slider

**Critical Feature: Security Level**

1. **Access Security Settings:**
   - Click shield icon (address bar, right side)
   - Or menu (≡) → Settings → Privacy & Security → Security Level

2. **Three Security Levels:**

   **Standard (Default):**
   - All Tor Browser features enabled
   - JavaScript enabled on all sites
   - Best compatibility with websites
   - **Use for:** Normal browsing, trusted sites

   **Safer:**
   - JavaScript disabled on non-HTTPS sites
   - Some fonts and symbols disabled
   - Some website features may break
   - **Use for:** General anonymous browsing

   **Safest:**
   - JavaScript disabled on ALL sites
   - Images disabled by default
   - Many website features disabled
   - **Use for:** Maximum anonymity, high-risk scenarios

**Exercise 5: Security Level Testing (20 minutes)**

Test each security level to understand trade-offs:

**Part A: Standard Security**

1. Set security to "Standard"
2. Visit: https://www.nytimes.com
   - Page loads fully
   - JavaScript works
   - Videos play
   - Interactive features work

3. Visit: https://check.torproject.org
   - Confirms you're using Tor
   - Shows your exit node IP
   - **Important:** This is NOT your real IP!

4. Search for something (use DuckDuckGo)
   - Notice: No personalized results
   - No location-based results
   - Clean, untracked searching

**Part B: Safer Security**

1. Change to "Safer" mode
2. Reload nytimes.com
   - Some features broken?
   - Most content still accessible
   - Faster loading (less JavaScript)

3. Visit: http://example.com (note: HTTP, not HTTPS)
   - JavaScript disabled on this site
   - Basic HTML still works

**Part C: Safest Security**

1. Change to "Safest" mode
2. Reload any website
   - Very minimal functionality
   - No JavaScript at all
   - Text and links only
   - Feels like web from 1990s

3. Try searching
   - Still works! DuckDuckGo works without JavaScript
   - Results load (no fancy features)

**Understanding the Trade-Off:**
- **More security = Less convenience**
- **More functionality = More fingerprintable**
- Choose based on your threat model

**Recommendation for Today:**
Use "Safer" mode as default. Switch to "Safest" for sensitive research. Only use "Standard" if you trust the website.

#### Anonymous Browsing Best Practices

**DO:**
- ✓ Use HTTPS websites whenever possible
- ✓ Use DuckDuckGo or Startpage for searches
- ✓ Stay logged out of personal accounts
- ✓ Assume websites can see each other (don't link identities)
- ✓ Use Security Slider appropriately
- ✓ Check that Tor is connected (green onion)
- ✓ Close browser between sensitive activities

**DON'T:**
- ✗ Log into personal accounts (Gmail, Facebook, etc.)
- ✗ Download files unnecessarily
- ✗ Install browser extensions
- ✗ Maximize browser window (fingerprinting risk)
- ✗ Enable Flash, Java, or similar plugins
- ✗ Torrent files through Tor
- ✗ Use Tor and VPN simultaneously (usually counterproductive)

**Exercise 6: Fingerprinting Awareness (20 minutes)**

**Browser Fingerprinting** is how websites identify you without cookies.

**Test Your Fingerprint:**

1. Visit: https://coveryourtracks.eff.org
   - (Previously called Panopticlick)
   - Click "Test your browser"
   - Wait for analysis

2. **Results Explanation:**
   - **Unique fingerprint?** Hopefully "No" in Tails!
   - **Tracking cookies?** Should be blocked
   - **Fingerprinting protection?** Should be "Yes"

3.