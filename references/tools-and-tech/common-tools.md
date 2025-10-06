---
layout: default
title: Common Tools
parent: Tools & Technology
grand_parent: References
nav_order: 2
---

# Common Tools

## **Essential Development Tools**

### **Code Editors & IDEs**

#### **Visual Studio Code**
- **What**: Free, cross-platform code editor by Microsoft
- **Why**: Extensions, debugging, Git integration, terminal
- **Setup**: Download from [code.visualstudio.com](https://code.visualstudio.com/)
- **Key Extensions**: Live Server, Prettier, GitLens, Python, JavaScript
- **Commands**: `code .` (open current directory)

#### **Cursor IDE**
- **What**: AI-powered code editor based on VS Code
- **Why**: Built-in AI assistance, code completion, chat interface
- **Setup**: Download from [cursor.sh](https://cursor.sh/)
- **Features**: AI code generation, explanation, debugging help
- **Cost**: Free tier available, paid plans for advanced features

#### **Sublime Text**
- **What**: Lightweight, fast text editor
- **Why**: Speed, multiple cursors, powerful search/replace
- **Setup**: Download from [sublimetext.com](https://www.sublimetext.com/)
- **Key Features**: Command palette (Ctrl+Shift+P), multi-select

### **Terminal & Command Line**

#### **Windows Terminal**
- **What**: Modern terminal application for Windows
- **Why**: Multiple tabs, themes, better performance
- **Setup**: Install from Microsoft Store or [github.com/microsoft/terminal](https://github.com/microsoft/terminal)
- **Features**: PowerShell, Command Prompt, WSL, Azure Cloud Shell

#### **PowerShell**
- **What**: Microsoft's command-line shell and scripting language
- **Why**: Object-oriented, powerful automation, cross-platform
- **Basic Commands**:
  ```powershell
  Get-ChildItem    # List files (ls)
  Set-Location     # Change directory (cd)
  Get-Content      # Read file (cat)
  New-Item         # Create file/folder
  ```

#### **Git Bash**
- **What**: Bash shell for Windows with Git integration
- **Why**: Unix-like commands, Git tools, familiar environment
- **Setup**: Included with Git for Windows
- **Features**: Bash commands, Git integration, Unix tools

### **Version Control**

#### **Git**
- **What**: Distributed version control system
- **Why**: Track changes, collaborate, backup code
- **Setup**: Download from [git-scm.com](https://git-scm.com/)
- **Basic Commands**:
  ```bash
  git init          # Initialize repository
  git add .         # Stage changes
  git commit -m ""  # Save changes
  git push          # Upload to remote
  git pull          # Download changes
  ```

#### **GitHub Desktop**
- **What**: GUI for Git operations
- **Why**: Visual interface, easier for beginners
- **Setup**: Download from [desktop.github.com](https://desktop.github.com/)
- **Features**: Visual diff, branch management, commit history

### **Package Managers**

#### **npm (Node Package Manager)**
- **What**: Package manager for JavaScript/Node.js
- **Why**: Install libraries, manage dependencies
- **Setup**: Comes with Node.js
- **Commands**:
  ```bash
  npm init          # Create package.json
  npm install       # Install dependencies
  npm run script    # Run scripts
  npm publish       # Publish package
  ```

#### **pip (Python Package Installer)**
- **What**: Package manager for Python
- **Why**: Install Python libraries, manage environments
- **Setup**: Comes with Python
- **Commands**:
  ```bash
  pip install package    # Install package
  pip list              # List installed packages
  pip freeze            # Show requirements
  pip install -r req.txt # Install from file
  ```

#### **Chocolatey (Windows)**
- **What**: Package manager for Windows
- **Why**: Install software from command line
- **Setup**: Run PowerShell as admin, then:
  ```powershell
  Set-ExecutionPolicy Bypass -Scope Process -Force
  [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072
  iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))
  ```
- **Commands**:
  ```bash
  choco install git     # Install software
  choco upgrade all     # Update all packages
  choco list            # List installed packages
  ```

### **Development Environments**

#### **Docker**
- **What**: Containerization platform
- **Why**: Consistent environments, easy deployment
- **Setup**: Download from [docker.com](https://docker.com/)
- **Basic Commands**:
  ```bash
  docker run image     # Run container
  docker build .       # Build image
  docker ps           # List containers
  docker-compose up   # Run multi-container apps
  ```

#### **VirtualBox**
- **What**: Virtualization software
- **Why**: Run multiple operating systems, testing
- **Setup**: Download from [virtualbox.org](https://www.virtualbox.org/)
- **Use Cases**: Linux testing, isolated environments, learning

### **Database Tools**

#### **MySQL Workbench**
- **What**: Visual database design tool
- **Why**: Database management, SQL development
- **Setup**: Download from [mysql.com](https://www.mysql.com/products/workbench/)
- **Features**: Visual query builder, database modeling

#### **DBeaver**
- **What**: Universal database tool
- **Why**: Support for multiple databases, free
- **Setup**: Download from [dbeaver.io](https://dbeaver.io/)
- **Features**: SQL editor, data visualization, ER diagrams

### **API Testing**

#### **Postman**
- **What**: API development and testing platform
- **Why**: Test APIs, document endpoints, collaborate
- **Setup**: Download from [postman.com](https://www.postman.com/)
- **Features**: Request builder, collections, environment variables

#### **Insomnia**
- **What**: API client and testing tool
- **Why**: Lightweight alternative to Postman
- **Setup**: Download from [insomnia.rest](https://insomnia.rest/)
- **Features**: GraphQL support, environment management

### **Design & Documentation**

#### **Figma**
- **What**: Collaborative design tool
- **Why**: UI/UX design, prototyping, team collaboration
- **Setup**: Sign up at [figma.com](https://figma.com/)
- **Features**: Real-time collaboration, component libraries

#### **Draw.io (diagrams.net)**
- **What**: Free diagramming tool
- **Why**: Flowcharts, system diagrams, documentation
- **Setup**: Use at [app.diagrams.net](https://app.diagrams.net/)
- **Features**: Flowcharts, ER diagrams, network diagrams

### **Productivity Tools**

#### **Notion**
- **What**: All-in-one workspace
- **Why**: Notes, databases, project management
- **Setup**: Sign up at [notion.so](https://notion.so/)
- **Features**: Templates, databases, collaboration

#### **Obsidian**
- **What**: Knowledge management tool
- **Why**: Note-taking, knowledge graphs, local storage
- **Setup**: Download from [obsidian.md](https://obsidian.md/)
- **Features**: Markdown support, plugins, graph view

### **System Monitoring**

#### **Process Monitor (ProcMon)**
- **What**: Windows system monitoring tool
- **Why**: Debug applications, monitor system activity
- **Setup**: Download from Microsoft Sysinternals
- **Features**: Real-time file, registry, network monitoring

#### **Wireshark**
- **What**: Network protocol analyzer
- **Why**: Network troubleshooting, security analysis
- **Setup**: Download from [wireshark.org](https://www.wireshark.org/)
- **Features**: Packet capture, protocol analysis

## **Tool Selection Guidelines**

### **For Beginners**
1. **VS Code** - Best all-around editor
2. **Git** - Essential version control
3. **Terminal** - Command line basics
4. **Postman** - API testing
5. **Docker** - Containerization

### **For Web Development**
1. **VS Code** with extensions
2. **Node.js** and npm
3. **Git** and GitHub
4. **Docker** for environments
5. **Postman** for API testing

### **For Cybersecurity**
1. **Wireshark** - Network analysis
2. **VirtualBox** - Lab environments
3. **Kali Linux** - Security tools
4. **Burp Suite** - Web application testing
5. **Metasploit** - Penetration testing

### **For Data Analysis**
1. **Jupyter Notebook** - Interactive analysis
2. **Python** with pandas, numpy
3. **R** and RStudio
4. **Tableau** - Data visualization
5. **SQL** tools (DBeaver, MySQL Workbench)

## **Installation Best Practices**

### **Windows**
1. **Use Chocolatey** for package management
2. **Install Git first** - many tools depend on it
3. **Use Windows Terminal** for better command line experience
4. **Enable WSL** for Linux compatibility

### **Cross-Platform Tools**
1. **Docker** - Consistent environments
2. **VS Code** - Universal editor
3. **Git** - Version control everywhere
4. **Node.js** - JavaScript runtime

### **Security Considerations**
1. **Download from official sources** only
2. **Keep tools updated** regularly
3. **Use antivirus** scanning for downloads
4. **Verify checksums** for critical tools

Remember: **Start with the basics and add tools as needed**. Don't overwhelm yourself with too many tools at once. Master the fundamentals first, then expand your toolkit based on your specific needs and projects.