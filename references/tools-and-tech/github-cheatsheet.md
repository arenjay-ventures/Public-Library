---
layout: default
title: GitHub Cheatsheet
parent: Tools & Technology
grand_parent: References
nav_order: 5
---

# GitHub Cheatsheet

## **Authentication & Setup**

### **Personal Access Token Setup**
1. Go to GitHub.com → Settings → Developer settings → Personal access tokens → Tokens (classic)
2. Click "Generate new token (classic)"
3. Configure:
   - **Note**: "Local Development Token"
   - **Expiration**: 90 days (or your preference)
   - **Scopes**: Check `repo`, `workflow`, `write:packages`, `delete:packages`
4. Click "Generate token"
5. **Copy token immediately** (format: `ghp_xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx`)

### **Git Configuration**
```bash
# Set up user identity
git config --global user.name "arenjay-ventures"
git config --global user.email "your-email@example.com"

# Configure credential helper
git config --global credential.helper manager-core

# Test authentication
git fetch
```

### **Using Personal Access Token**
- **Username**: `arenjay-ventures`
- **Password**: Use your Personal Access Token (not GitHub password)
- Windows Credential Manager will store these credentials

## **Repository Management**

### **Clone Repository**
```bash
# HTTPS (recommended)
git clone https://github.com/arenjay-ventures/repository-name.git

# SSH (if configured)
git clone git@github.com:arenjay-ventures/repository-name.git
```

### **Create New Repository**
```bash
# Initialize local repository
git init
git add .
git commit -m "Initial commit"

# Add remote origin
git remote add origin https://github.com/arenjay-ventures/repository-name.git
git branch -M main
git push -u origin main
```

### **Repository Operations**
```bash
# Check repository status
git status
git remote -v

# Add remote repository
git remote add origin https://github.com/arenjay-ventures/repository-name.git

# Change remote URL
git remote set-url origin https://github.com/arenjay-ventures/repository-name.git
```

## **Branch Management**

### **Branch Operations**
```bash
# List branches
git branch -a

# Create and switch to new branch
git checkout -b feature-branch
git switch -c feature-branch  # Modern syntax

# Switch between branches
git checkout main
git switch main  # Modern syntax

# Delete branch
git branch -d feature-branch
git push origin --delete feature-branch
```

### **Branch Workflow**
```bash
# Pull latest changes
git pull origin main

# Create feature branch
git checkout -b feature/new-feature

# Make changes, commit
git add .
git commit -m "Add new feature"

# Push feature branch
git push origin feature/new-feature

# Create Pull Request on GitHub, then merge
```

## **Commit Management**

### **Making Commits**
```bash
# Stage specific files
git add filename.txt
git add folder/
git add *.md

# Stage all changes
git add .

# Commit with message
git commit -m "Descriptive commit message"

# Commit with detailed message
git commit -m "Add new feature" -m "Detailed description of changes"

# Amend last commit
git commit --amend -m "Updated commit message"
```

### **Commit Best Practices**
- Use present tense: "Add feature" not "Added feature"
- Keep first line under 50 characters
- Use detailed description for complex changes
- Reference issues: "Fix #123: Resolve authentication bug"

## **Push & Pull Operations**

### **Push Changes**
```bash
# Push to current branch
git push

# Push to specific branch
git push origin main
git push origin feature-branch

# Force push (use carefully)
git push --force-with-lease origin main

# Push all branches
git push --all origin
```

### **Pull Changes**
```bash
# Pull latest changes
git pull

# Pull from specific branch
git pull origin main

# Fetch without merging
git fetch origin
git merge origin/main
```

## **GitHub Pages Setup**

### **Enable GitHub Pages**
1. Go to repository → Settings → Pages
2. Source: "Deploy from a branch"
3. Branch: `main` (or `gh-pages`)
4. Folder: `/ (root)`
5. Save

### **Jekyll Configuration**
```yaml
# _config.yml
title: "Your Site Title"
description: "Site description"
theme: just-the-docs
url: "https://arenjay-ventures.github.io/repository-name"
```

## **Issue & Pull Request Management**

### **Creating Issues**
- Use clear, descriptive titles
- Include steps to reproduce for bugs
- Use labels for categorization
- Assign to team members

### **Pull Request Workflow**
```bash
# Create feature branch
git checkout -b feature/issue-123

# Make changes and commit
git add .
git commit -m "Fix #123: Resolve authentication issue"

# Push branch
git push origin feature/issue-123

# Create PR on GitHub
# After approval, merge and delete branch
```

## **Advanced Operations**

### **Undo Operations**
```bash
# Undo last commit (keep changes)
git reset --soft HEAD~1

# Undo last commit (discard changes)
git reset --hard HEAD~1

# Undo uncommitted changes
git checkout -- filename.txt
git restore filename.txt  # Modern syntax

# Revert a commit
git revert commit-hash
```

### **Stash Operations**
```bash
# Stash current changes
git stash
git stash push -m "Work in progress"

# List stashes
git stash list

# Apply stash
git stash apply
git stash pop

# Drop stash
git stash drop
```

### **History & Logs**
```bash
# View commit history
git log --oneline
git log --graph --oneline --all

# View file history
git log --follow filename.txt

# View changes
git diff
git diff --staged
git show commit-hash
```

## **Troubleshooting**

### **Common Issues**
```bash
# Authentication failed
git config --global credential.helper manager-core
git push  # Will prompt for credentials

# Merge conflicts
git status  # Shows conflicted files
# Edit files to resolve conflicts
git add resolved-file.txt
git commit -m "Resolve merge conflict"

# Detached HEAD
git checkout main
git checkout -b new-branch  # If you want to keep changes
```

### **Reset Operations**
```bash
# Reset to remote state
git fetch origin
git reset --hard origin/main

# Clean working directory
git clean -fd
```

## **GitHub CLI (Optional)**

### **Install GitHub CLI**
```bash
# Windows (using winget)
winget install GitHub.cli

# Or download from: https://cli.github.com/
```

### **GitHub CLI Commands**
```bash
# Authenticate
gh auth login

# Create repository
gh repo create repository-name --public

# Create issue
gh issue create --title "Bug report" --body "Description"

# Create pull request
gh pr create --title "Feature request" --body "Description"

# List repositories
gh repo list arenjay-ventures
```

## **Best Practices**

### **Repository Structure**
- Use descriptive commit messages
- Keep commits atomic (one logical change per commit)
- Use branches for features and fixes
- Regularly pull latest changes
- Use `.gitignore` for unnecessary files

### **Security**
- Never commit passwords or API keys
- Use environment variables for sensitive data
- Regularly rotate Personal Access Tokens
- Use SSH keys for frequent operations
- Enable 2FA on GitHub account

### **Collaboration**
- Use Pull Requests for code review
- Write clear PR descriptions
- Use labels and milestones
- Keep discussions constructive
- Follow the repository's contributing guidelines