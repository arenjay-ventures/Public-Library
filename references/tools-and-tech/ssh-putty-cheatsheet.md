---
layout: default
title: SSH & PuTTY Cheatsheet
parent: Tools & Technology
grand_parent: References
nav_order: 14
---

# SSH & PuTTY Cheatsheet

## Quick Summary
SSH (Secure Shell) is a cryptographic network protocol for secure remote access and file transfer. PuTTY is a popular SSH client for Windows. Essential for remote server management, secure file transfers, and tunneling.

## Importance
- **Remote Access**: Secure connection to servers and devices
- **File Transfer**: Secure copying of files between systems
- **Tunneling**: Create secure tunnels for network traffic
- **Automation**: Script remote commands and deployments
- **Security**: Encrypted communication over unsecured networks

## Basic Setup & Installation

### SSH Client Installation
```bash
# Ubuntu/Debian
sudo apt update
sudo apt install openssh-client

# CentOS/RHEL
sudo yum install openssh-clients

# macOS (usually pre-installed)
ssh --version
```

### PuTTY Installation (Windows)
1. Download from: https://www.putty.org/
2. Install or use portable version
3. Configure saved sessions for easy access

## Essential Commands

### SSH Connection
```bash
# Basic connection
ssh username@hostname

# Connect with specific port
ssh -p 2222 username@hostname

# Connect with key file
ssh -i /path/to/private_key username@hostname

# Connect with verbose output
ssh -v username@hostname

# Connect and execute command
ssh username@hostname "command"
```

### SSH Key Management
```bash
# Generate SSH key pair
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"

# Copy public key to server
ssh-copy-id username@hostname

# Add key to SSH agent
ssh-add /path/to/private_key

# List loaded keys
ssh-add -l
```

### SCP (Secure Copy)
```bash
# Copy file to remote server
scp file.txt username@hostname:/remote/path/

# Copy file from remote server
scp username@hostname:/remote/path/file.txt ./

# Copy directory recursively
scp -r local_directory/ username@hostname:/remote/path/

# Copy with specific port
scp -P 2222 file.txt username@hostname:/remote/path/
```

### SFTP (SSH File Transfer Protocol)
```bash
# Connect to SFTP
sftp username@hostname

# SFTP commands
get remote_file local_file    # Download file
put local_file remote_file   # Upload file
ls                           # List remote directory
lls                          # List local directory
cd remote_directory          # Change remote directory
lcd local_directory          # Change local directory
```

### SSH Tunneling
```bash
# Local port forwarding
ssh -L 8080:localhost:80 username@hostname

# Remote port forwarding
ssh -R 8080:localhost:80 username@hostname

# Dynamic port forwarding (SOCKS proxy)
ssh -D 1080 username@hostname
```

## PuTTY Configuration

### Basic Settings
- **Host Name**: IP address or hostname
- **Port**: 22 (default SSH port)
- **Connection Type**: SSH
- **Saved Sessions**: Name and save for reuse

### Advanced Settings
- **Connection > SSH > Auth**: Private key file path
- **Connection > Data**: Auto-login username
- **Terminal**: Terminal type and features
- **Window**: Window size and behavior

### PuTTY Key Generation
1. Run PuTTYgen
2. Generate new key pair (RSA 2048+)
3. Save private key (.ppk format)
4. Copy public key to server

## Security Best Practices

### Key Management
```bash
# Use strong passphrases for keys
ssh-keygen -t ed25519 -C "your_email@example.com"

# Disable password authentication (use keys only)
# Edit /etc/ssh/sshd_config
PasswordAuthentication no
PubkeyAuthentication yes
```

### SSH Configuration
```bash
# Client configuration (~/.ssh/config)
Host myserver
    HostName 192.168.1.100
    User myusername
    Port 22
    IdentityFile ~/.ssh/id_rsa
    ServerAliveInterval 60
```

### Server Hardening
```bash
# Edit /etc/ssh/sshd_config
PermitRootLogin no
MaxAuthTries 3
ClientAliveInterval 300
ClientAliveCountMax 2
```

## Troubleshooting

### Common Issues
```bash
# Permission denied (publickey)
ssh-add -l  # Check loaded keys
ssh-add ~/.ssh/id_rsa  # Add key to agent

# Connection refused
telnet hostname 22  # Test if port is open
ssh -v username@hostname  # Verbose connection

# Host key verification failed
ssh-keygen -R hostname  # Remove old host key
```

### Debugging
```bash
# Verbose SSH connection
ssh -vvv username@hostname

# Test SSH connection
ssh -T git@github.com  # Test GitHub SSH

# Check SSH agent
ssh-add -l
echo $SSH_AUTH_SOCK
```

## Useful Aliases
```bash
# Add to ~/.bashrc or ~/.zshrc
alias sshserver='ssh -i ~/.ssh/server_key user@server.com'
alias sshdev='ssh -L 3000:localhost:3000 dev@dev-server.com'
alias sshprod='ssh -L 8080:localhost:80 prod@prod-server.com'
```

## References
- [OpenSSH Manual](https://www.openssh.com/manual.html)
- [PuTTY Documentation](https://www.putty.org/)
- [SSH Key Management Guide](https://docs.github.com/en/authentication/connecting-to-github-with-ssh)
- [SSH Tunneling Guide](https://www.ssh.com/academy/ssh/tunneling)
