---
layout: default
title: GitHub Pages
parent: Tutorials
nav_order: 4
---

# GitHub Pages - Professional Portfolio Setup

## Tutorial Information

**Title:** GitHub Pages - Professional Portfolio Setup  
**Author:** Justin  
**Date Created:** 2024-10-08  
**Last Updated:** 2024-10-08  
**Difficulty Level:** Intermediate  
**Estimated Time:** 2-3 hours  
**Prerequisites:** GitHub account, basic command-line knowledge

---

## Overview

### What You'll Learn
- How to set up a professional GitHub Pages portfolio
- How to use Git and GitHub for version control
- How to configure Jekyll with "Just the Docs" theme
- How to use VS Code for development
- How to troubleshoot common GitHub Pages issues

### What You'll Build
A free, professional, and fully customizable portfolio website using the "Just the Docs" theme on GitHub Pages

### Technologies Used
- Git and GitHub
- GitHub Pages
- Jekyll
- Markdown
- YAML
- VS Code
- Command-Line Interface (CLI)

---

## Prerequisites

### Required Knowledge
- Basic understanding of version control concepts
- Familiarity with command-line interface
- Experience with text editing

### Required Tools
- Git - Version control system
- Visual Studio Code - Code editor/IDE
- GitHub account
- Internet connection

### System Requirements
- **Operating System:** Windows, macOS, or Linux
- **RAM:** 4GB minimum
- **Storage:** 1GB free space
- **Internet:** Stable connection for GitHub operations

---

## Step-by-Step Instructions

### Step 1: Install Essential Tools
**Objective:** Set up your development environment

1. **Git:** Git is the version control system that tracks changes to your code. If you don't have it, download and install it from [git-scm.com](https://git-scm.com/downloads). Accept the default settings during installation.
2. **Visual Studio Code (VS Code):** This will be our code editor, or IDE. It's the industry standard for its power and flexibility. Download it from [code.visualstudio.com](https://code.visualstudio.com/).

**Expected Result:** Both Git and VS Code installed and ready to use

**Troubleshooting:**
- **Issue:** Git command not recognized
  - **Solution:** Restart your terminal/command prompt after installation

---

### Step 2: Configure Git with Your Identity
**Objective:** Set up Git with your personal information

After installing Git, you must tell it who you are. This information will be attached to every change you make. Open your command prompt (Terminal on Mac/Linux, Git Bash on Windows) and run these two commands, replacing the placeholders with your information:

```bash
git config --global user.name "Your Name"
git config --global user.email "youremail@example.com"
```
*(Use the same email you used for your GitHub account.)*

**Expected Result:** Git configured with your identity

**Troubleshooting:**
- **Issue:** Commands not working
  - **Solution:** Make sure you're using Git Bash on Windows or Terminal on Mac/Linux

---

### Step 3: Create the Live Repository from Template
**Objective:** Set up your GitHub Pages repository

1. Navigate to the **[Just the Docs Template Repository](https://github.com/just-the-docs/just-the-docs-template)**.
2. Click the green **"Use this template"** button and select **"Create a new repository"**.
3. On the "Create a new repository" page, configure the following:
   - **Repository name:** This is the most critical step. Name it **exactly** `your-username.github.io`. (e.g., if your username is `jdoe`, the repo is `jdoe.github.io`).
   - **Description:** "My Cybersecurity Portfolio" or a similar professional summary.
   - **Public/Private:** Ensure it is set to **Public**.
4. Click **"Create repository"**.

**Expected Result:** New repository created with template content

**Troubleshooting:**
- **Issue:** Repository name not available
  - **Solution:** Choose a different username or add numbers/characters to make it unique

---

### Step 4: Clone the Repository to Your Local Machine
**Objective:** Get a local copy of your repository

"Cloning" means creating a local copy of the remote repository on your computer.

1. On your new repository's GitHub page, click the green **`< > Code`** button.
2. Ensure the **HTTPS** tab is selected and click the **copy icon** next to the URL.
3. Open your terminal and navigate to a directory where you want to store your projects (e.g., `cd Documents/Projects`).
4. Run the `git clone` command, pasting the URL you copied:
   ```bash
   git clone https://github.com/your-username/your-username.github.io.git
   ```
5. A new folder named `your-username.github.io` will be created. Navigate into it:
   ```bash
   cd your-username.github.io
   ```

**Expected Result:** Local copy of your repository on your computer

**Troubleshooting:**
- **Issue:** Clone fails with authentication error
  - **Solution:** Make sure you're using HTTPS and have access to the repository

---

### Step 5: Open the Project in VS Code
**Objective:** Set up your development environment

With your terminal still in the project directory, run this command to open the entire folder in VS Code:
```bash
code .
```
*(The `.` is shorthand for "the current directory".)*
You will now see the entire file structure of your new website in the left-hand sidebar of VS Code.

**Expected Result:** VS Code open with your project files visible

**Troubleshooting:**
- **Issue:** `code` command not found
  - **Solution:** Install VS Code and restart your terminal, or open VS Code manually and use File > Open Folder

---

### Step 6: Configure Your Site in `_config.yml`
**Objective:** Customize your site settings

The `_config.yml` file is the main control panel for your website.

1. In VS Code, find and open the `_config.yml` file.
2. Make the following edits. **Crucially, remember to wrap any values that contain special characters (like a colon `:`) in quotes.**
   ```yaml
   # Add quotes around the title because it contains a colon
   title: 'Your Name: Cybersecurity Portfolio'
   description: 'A collection of my hands-on projects and skills.'
   
   # This should already be set, but verify it
   theme: just-the-docs
   
   # This URL is automatically generated by GitHub, but setting it is good practice
   url: https://your-username.github.io
   ```
3. Save the file (`Ctrl+S` or `Cmd+S`).

**Expected Result:** Site configuration updated with your information

**Troubleshooting:**
- **Issue:** YAML syntax errors
  - **Solution:** Make sure to use proper indentation (spaces, not tabs) and quote strings with special characters

---

### Step 7: The First Commit & Push
**Objective:** Save and upload your changes

Now, let's send this change to GitHub using the command line.

1. Open the integrated terminal in VS Code (**View > Terminal** or **Ctrl+`**).
2. **Stage your changes:** This prepares your modified files for saving.
   ```bash
   git add .
   ```
3. **Commit your changes:** This saves the snapshot with a descriptive message explaining what you did.
   ```bash
   git commit -m "Configure initial site title and description"
   ```
4. **Push your changes:** This uploads your committed changes from your computer to the `main` branch on GitHub.
   ```bash
   git push
   ```

**Expected Result:** Changes uploaded to GitHub successfully

**Troubleshooting:**
- **Issue:** Push fails with authentication error
  - **Solution:** You may need to set up a Personal Access Token for GitHub authentication

---

### Step 8: Set Permissions and Go Live!
**Objective:** Enable GitHub Pages and make your site live

There's one final one-time setup step on GitHub to allow the site to build.

1. Go back to your repository on the GitHub website.
2. Go to **"Settings" > "Actions" > "General"**.
3. Scroll to "Workflow permissions", select **"Read and write permissions"**, and click **Save**.
4. Now navigate to **"Settings" > "Pages"**.
5. Under "Build and deployment", ensure the **Source** is set to **"Deploy from a branch"** and the branch is `main`.
6. You should see a message at the top saying, "Your site is live at `https://your-username.github.io`". It may take 2-5 minutes to build the first time.

**Expected Result:** Your website is live and accessible

**Troubleshooting:**
- **Issue:** Site not building
  - **Solution:** Check the Actions tab for build errors and fix any YAML syntax issues

---

## Troubleshooting & Debugging

### Step 1: Check the Build Action
- In your GitHub repository, go to the **"Actions"** tab.
- Look at the latest workflow run. Is it a **Green Checkmark (✅)** or a **Red X (❌)**?

### Step 2: If the Build FAILED (Red ❌)
- A failed build is almost always a syntax error in a `.yml` or `.md` file.
- Click on the failed run, then click the `build` job on the left.
- Scroll through the log and look for the error message in red text. It will often tell you the exact file and line number that caused the problem.
- **Common Cause:** A missing space after a colon in a YAML file (e.g., `title:My Site` instead of `title: My Site`) or improperly formatted Front Matter.
- Fix the error in VS Code, then `git add .`, `git commit -m "Fix build error"`, and `git push` again.

### Step 3: If the Build SUCCEEDED (Green ✅) but you don't see changes
- The issue is almost certainly browser caching. Your browser is showing you an old version of the site.
- **Solution:** Perform a "hard refresh" by pressing **`Ctrl+Shift+R`** (Windows/Linux) or **`Cmd+Shift+R`** (Mac).
- **Alternative Cause:** A logical error in your Front Matter. Double-check that `parent:` and `grand_parent:` values in your page files exactly match the `title:` of their intended parent pages (it's case-sensitive!).

---

## Summary

### What You Accomplished
Successfully set up a professional GitHub Pages portfolio website using the "Just the Docs" theme with proper version control workflow.

### Key Takeaways
- GitHub Pages provides free hosting for static websites
- Git workflow (add, commit, push) is essential for development
- YAML configuration files control site behavior
- VS Code is a powerful development environment
- Troubleshooting build errors is a normal part of development

### Skills Developed
- Git version control
- GitHub Pages deployment
- Jekyll site configuration
- Command-line interface usage
- Web development workflow
- Problem-solving and debugging

---

## Additional Resources

### Documentation
- [GitHub Pages Documentation](https://docs.github.com/en/pages)
- [Jekyll Documentation](https://jekyllrb.com/docs/)
- [Just the Docs Theme](https://just-the-docs.github.io/just-the-docs/)
- [Markdown Guide](https://www.markdownguide.org/)

### Tools & Extensions
- [VS Code Git Extension](https://marketplace.visualstudio.com/items?itemName=eamodio.gitlens) - Enhanced Git capabilities
- [Markdown All in One](https://marketplace.visualstudio.com/items?itemName=yzhang.markdown-all-in-one) - Markdown editing tools
- [YAML Extension](https://marketplace.visualstudio.com/items?itemName=redhat.vscode-yaml) - YAML syntax support

### Community Support
- [GitHub Community](https://github.community/)
- [Jekyll Talk](https://talk.jekyllrb.com/)
- [Stack Overflow GitHub Pages](https://stackoverflow.com/questions/tagged/github-pages)

---

**Tutorial Created By:** Justin  
**Contact:** Available through portfolio  
**Last Updated:** 2024-10-08  
**Version:** 1.0
