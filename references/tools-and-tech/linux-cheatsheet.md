---
layout: default
title: Linux Cheatsheet
parent: Tools & Technology
grand_parent: References
nav_order: 6
---

# Linux Cheatsheet

## **What is Linux?**

Linux is an open-source operating system kernel that powers servers, embedded systems, and increasingly desktop computers. It's essential for:
- **Server Administration**: Most web servers run Linux
- **Cloud Computing**: AWS, Azure, Google Cloud use Linux
- **Cybersecurity**: Penetration testing, security analysis
- **Development**: Many development tools work best on Linux
- **Career Growth**: Linux skills are highly valued in tech

## **Getting Started**

### **Popular Distributions**
- **Ubuntu**: User-friendly, great for beginners
- **CentOS/RHEL**: Enterprise-focused, server environments
- **Debian**: Stable, widely used in servers
- **Kali Linux**: Security-focused, penetration testing
- **Arch Linux**: Advanced users, rolling release

### **Getting Linux**
1. **Virtual Machine**: VirtualBox, VMware (recommended for beginners)
2. **Dual Boot**: Install alongside Windows
3. **WSL**: Windows Subsystem for Linux
4. **Cloud**: AWS EC2, Google Cloud, Azure

## **Essential Commands**

### **File System Navigation**
```bash
# Navigation
pwd                    # Print working directory
ls                     # List files
ls -la                 # List all files with details
cd /path/to/directory  # Change directory
cd ~                   # Go to home directory
cd ..                  # Go up one directory
cd -                   # Go to previous directory

# File Operations
touch filename         # Create empty file
mkdir directory       # Create directory
mkdir -p path/to/dir  # Create nested directories
rm filename           # Delete file
rm -rf directory      # Delete directory recursively
cp source dest        # Copy file
mv source dest        # Move/rename file
```

### **File Permissions**
```bash
# View permissions
ls -la                 # Shows permissions (rwxrwxrwx)

# Change permissions
chmod 755 filename     # rwxr-xr-x (owner: rwx, group: r-x, other: r-x)
chmod +x filename      # Add execute permission
chmod -x filename      # Remove execute permission

# Change ownership
chown user:group file  # Change owner and group
chown user file        # Change owner only
```

### **Text Processing**
```bash
# View files
cat filename           # Display entire file
less filename          # View file page by page
head -n 10 filename    # Show first 10 lines
tail -n 10 filename    # Show last 10 lines
tail -f filename       # Follow file changes (logs)

# Search in files
grep "pattern" file    # Search for pattern in file
grep -r "pattern" dir  # Search recursively in directory
grep -i "pattern" file # Case-insensitive search
```

### **Process Management**
```bash
# View processes
ps                     # Show running processes
ps aux                 # Show all processes with details
top                    # Real-time process monitor
htop                   # Enhanced process monitor (install with: apt install htop)

# Process control
kill PID               # Kill process by ID
kill -9 PID            # Force kill process
killall process_name   # Kill all processes with name
nohup command &        # Run command in background
```

### **System Information**
```bash
# System info
uname -a               # System information
whoami                 # Current user
id                     # User and group IDs
df -h                  # Disk space usage
free -h                # Memory usage
uptime                 # System uptime
```

### **Package Management**

#### **Ubuntu/Debian (apt)**
```bash
# Update package lists
sudo apt update

# Install package
sudo apt install package_name

# Remove package
sudo apt remove package_name

# Search packages
apt search keyword

# List installed packages
dpkg -l

# Update system
sudo apt upgrade
```

#### **CentOS/RHEL (yum/dnf)**
```bash
# Install package
sudo yum install package_name
sudo dnf install package_name

# Remove package
sudo yum remove package_name

# Update system
sudo yum update
```

### **Network Commands**
```bash
# Network information
ip addr                # Show network interfaces
ip route              # Show routing table
netstat -tulpn        # Show network connections
ss -tulpn             # Modern alternative to netstat

# Connectivity
ping hostname          # Test connectivity
traceroute hostname    # Trace network path
nslookup domain       # DNS lookup
dig domain            # Advanced DNS lookup
```

### **File Compression**
```bash
# Create archives
tar -czf archive.tar.gz directory/    # Create gzipped tar
tar -xzf archive.tar.gz               # Extract gzipped tar
zip -r archive.zip directory/        # Create zip archive
unzip archive.zip                     # Extract zip archive

# Common tar options
tar -czf backup.tar.gz /path/to/backup
tar -xzf backup.tar.gz
tar -tf archive.tar.gz               # List contents without extracting
```

## **Text Editors**

### **Nano (Beginner-friendly)**
```bash
nano filename          # Open file in nano
# Ctrl+X to exit
# Ctrl+O to save
# Ctrl+W to search
```

### **Vim (Advanced)**
```bash
vim filename           # Open file in vim

# Vim modes
i                      # Insert mode
Esc                    # Command mode
:w                     # Save
:q                     # Quit
:wq                    # Save and quit
:q!                    # Quit without saving
```

### **Basic Vim Commands**
```bash
# Navigation
h, j, k, l            # Left, down, up, right
w                     # Next word
b                     # Previous word
0                     # Beginning of line
$                     # End of line
gg                    # Beginning of file
G                     # End of file

# Editing
i                     # Insert before cursor
a                     # Insert after cursor
o                     # New line below
O                     # New line above
x                     # Delete character
dd                    # Delete line
yy                    # Copy line
p                     # Paste
u                     # Undo
```

## **Shell Scripting Basics**

### **Creating Scripts**
```bash
#!/bin/bash           # Shebang line
# This is a comment

# Variables
NAME="John"
echo "Hello, $NAME"

# User input
read -p "Enter your name: " USERNAME
echo "Hello, $USERNAME"

# Conditional statements
if [ $AGE -gt 18 ]; then
    echo "Adult"
else
    echo "Minor"
fi

# Loops
for i in {1..5}; do
    echo "Number: $i"
done

# Functions
function greet() {
    echo "Hello, $1"
}
greet "World"
```

### **Making Scripts Executable**
```bash
chmod +x script.sh    # Make executable
./script.sh           # Run script
```

## **System Administration**

### **User Management**
```bash
# Add user
sudo useradd -m username
sudo passwd username

# Delete user
sudo userdel username

# Add to group
sudo usermod -aG groupname username

# Switch user
su username
sudo -u username command
```

### **Service Management**
```bash
# Systemd (modern Linux)
sudo systemctl start service_name
sudo systemctl stop service_name
sudo systemctl restart service_name
sudo systemctl enable service_name
sudo systemctl status service_name

# Service (older systems)
sudo service service_name start
sudo service service_name stop
sudo service service_name restart
```

### **Log Files**
```bash
# Common log locations
/var/log/syslog        # System log
/var/log/auth.log     # Authentication log
/var/log/apache2/     # Web server logs
/var/log/nginx/       # Nginx logs

# View logs
tail -f /var/log/syslog
journalctl -f         # Systemd journal
```

## **Security Basics**

### **Firewall (UFW)**
```bash
# Enable firewall
sudo ufw enable

# Allow/deny ports
sudo ufw allow 22     # SSH
sudo ufw allow 80     # HTTP
sudo ufw allow 443    # HTTPS
sudo ufw deny 23      # Telnet

# Check status
sudo ufw status
```

### **SSH**
```bash
# Connect to remote server
ssh username@hostname
ssh -p 2222 username@hostname

# Copy files
scp file.txt username@hostname:/path/
scp -r directory/ username@hostname:/path/

# Generate SSH key
ssh-keygen -t rsa -b 4096
ssh-copy-id username@hostname
```

## **Useful Aliases**
```bash
# Add to ~/.bashrc or ~/.zshrc
alias ll='ls -la'
alias la='ls -A'
alias l='ls -CF'
alias ..='cd ..'
alias ...='cd ../..'
alias grep='grep --color=auto'
alias fgrep='fgrep --color=auto'
alias egrep='egrep --color=auto'
```

## **Learning Resources**

### **Online Practice**
- **[Linux Journey](https://linuxjourney.com/)** - Interactive Linux tutorial
- **[OverTheWire Bandit](https://overthewire.org/wargames/bandit/)** - Linux security wargame
- **[Linux Academy](https://linuxacademy.com/)** - Comprehensive Linux training
- **[Red Hat Learning](https://www.redhat.com/en/services/training)** - Enterprise Linux training

### **Books**
- **"Linux Command Line and Shell Scripting Bible"** - Comprehensive reference
- **"The Linux Command Line"** by William Shotts - Free online book
- **"Linux Administration Handbook"** - System administration guide

### **Practice Environments**
- **VirtualBox** with Ubuntu
- **AWS EC2** free tier
- **Docker** containers
- **WSL** on Windows

## **Common Troubleshooting**

### **Permission Denied**
```bash
sudo chmod +x filename    # Make executable
sudo chown user:group file  # Change ownership
```

### **Command Not Found**
```bash
which command          # Find command location
whereis command        # Find command and man pages
sudo apt install package  # Install missing package
```

### **Disk Space Issues**
```bash
df -h                  # Check disk usage
du -sh directory/      # Check directory size
sudo apt autoremove    # Remove unused packages
sudo apt autoclean     # Clean package cache
```

Remember: **Linux is about practice**. Start with basic commands, build a home lab, and gradually work your way up to system administration and scripting. The command line is your friend - embrace it!