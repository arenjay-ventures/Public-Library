---
layout: default
title: Building a Two-Site Portfolio with AI
parent: Tutorials
nav_order: 4
---

### **Tutorial Information**
**Title:** Building a Two-Site Professional Portfolio with GitHub Pages & an AI Assistant
**Author:** J. Hancock
**Date Created:** 2025-10-06
**Last Updated:** 2025-10-08
**Difficulty Level:** Intermediate
**Estimated Time:** 2 hours
**Prerequisites:** A GitHub account.

---

### **Overview**

This tutorial documents the modern, efficient process for setting up a professional, two-site digital presence using GitHub Pages and an AI Coder (like Cursor). The goal is to move from idea to a perfectly structured, live website in minutes, not hours.

> This tutorial's content is based on my direct actions and the real issues I encountered while working between multiple incomplete guides. The process described here is tested and verified.

**This is a tutorial for high-speed page and file setup, not content creation.** We leverage AI for the tedious and error-prone task of scaffolding, freeing us to focus on the human-centric work of writing valuable content.

#### **What You’ll Learn**
*   How to create a professional, two-site web presence for a portfolio and a public library.
*   How to use the standard Git command-line workflow to manage a project locally.
*   How to leverage an AI Coder to rapidly scaffold a complex website structure.
*   How to troubleshoot and fix the common "404 Not Found" error for multi-site GitHub Pages setups.

#### **What You’ll Build**
1.  A curated, employer-facing portfolio site (`your-username.github.io`).
2.  A separate, scalable Public Library (`your-username.github.io/Public-Library`) for notes and tutorials.

### **Prerequisites**
#### **Required Tools**
*   **Git:** [Download and install from git-scm.com](https://git-scm.com/downloads)
*   **IDE (AI Coder):** [Download and install Cursor](https://cursor.sh/) or Visual Studio Code with an AI extension.
*   **GitHub Account:** [Create one for free at GitHub.com](https://github.com/)

---

### **Step-by-Step Instructions**

#### **Step 1: Local Environment Setup**
**Objective:** Prepare your local machine with the necessary tools and configuration.

1.  Install Git and your chosen IDE.
2.  Open your terminal and configure Git with your identity.
    ```bash
    git config --global user.name "Your Name"
    git config --global user.email "youremail@example.com"
    ```
**Expected Result:** Git is installed and configured.

---

#### **Step 2: Create Repositories from the Official Template**
**Objective:** Use the official "Just the Docs" template to create two repositories with a working base.

1.  Navigate to the [Just the Docs Template Repository](https://github.com/just-the-docs/just-the-docs-template).
2.  **Create Your Portfolio Repo:**
    *   Click **"Use this template" > "Create a new repository"**.
    *   Name the repository **exactly** `your-username.github.io`.
    *   Ensure it is **Public**.
3.  **Create Your Library Repo:**
    *   Go back to the template and repeat the process.
    *   Name this repository `Public-Library` (or your chosen name).
    *   Ensure it is **Public**.
4.  **Clone Both Repositories:** In your terminal, navigate to your projects directory and clone both new repositories to your local machine.
    ```bash
    git clone https://github.com/your-username/your-username.github.io.git
    git clone https://github.com/your-username/Public-Library.git
    ```
5.  **Open Workspace:** Open your IDE and add both project folders to your workspace for easy file management.

**Expected Result:** You have local copies of both repositories, ready for modification.

---

#### **Step 3: AI-Assisted File Scaffolding**
**Objective:** Use your AI Coder to rapidly and accurately build the entire folder and file structure for both sites.

1.  **Craft the Prompt:** A good prompt is specific. It should define the exact folder structure, file names, and the required YAML Front Matter for every single page. You can add a diagram or visual or your file map or layout as well.

2.  **Execute the Prompt:** In your AI Coder, open both project folders. Address the AI and provide the prompt below, filling in your specific details. The AI will generate all the necessary folders and placeholder `.md` files in seconds.

##### **The AI Coder Prompt Template:**
**`[Copy the prompt below and fill in the <placeholders>]`**
> You are an expert in setting up Jekyll sites with the "Just the Docs" theme. I have two repositories that I need to completely restructure: my main portfolio site (`<your-username>.github.io`) and my knowledge base (`Public-Library`).
>
> Your task is to execute the following file creation and moving plan. If you find any existing content files, MOVE them into the new structure and UPDATE their YAML Front Matter. DO NOT DELETE my existing content. For all new placeholder pages, use `(Content coming soon...)` under the main heading. For every file, generate the correct YAML Front Matter (`title`, `parent`, `grand_parent`, `nav_order`, `has_children`).
>
> **Part 1: Refactor `<your-username>.github.io`**
> Create the following structure:
> *   Top-Level Pages: `about.md`, `projects.md`, `certifications.md`, `contact.md`.
> *   Project Categories (in `projects/`): `physical-and-homelab.md`, `software-and-code.md`.
> *   Software Sub-Categories (in `projects/software-and-code/`): `crypto.md`, `web.md`, `scripts.md`.
> *   Project Placeholders: Create placeholder pages for projects like `solidity-project-1.md` inside their respective sub-category folders.
>
> **Part 2: Refactor `Public-Library`**
> Create the following structure:
> *   Top-Level Pages: `templates.md`, `references.md`, `tutorials.md`, `project-log.md`.
> *   Populate `templates/` folder: Create `project-report-template.md` and populate it with the provided content.
> *   Structure `references/` and `tutorials/` folders with their respective category pages and placeholders.
>
> **`[Include the full Project Report Template content here at the end of your prompt]`**

**Expected Result:** Both local repositories now have a complete, nested file structure.

---

#### **Step 4: Manual Configuration & Troubleshooting**
**Objective:** Manually configure the `_config.yml` file for each site, applying the critical fix for the subdirectory-based Public Library.

1.  **Configure the Main Portfolio (`your-username.github.io`):**
    *   Open its `_config.yml` file and edit the `title`, `description`, and `url`.
    ```yaml
    title: '<Your Name>: Professional Portfolio'
    description: 'A curated collection of my professional projects.'
    url: https://<your-username>.github.io
    ```

2.  **Troubleshooting a Common Pitfall: The 404 Error on the Second Site:**
    *   **Issue:** After deploying, I encountered a `404 Not Found` error for my `Public-Library` site. This is a classic issue when hosting a Jekyll site in a subdirectory.
    *   **Cause:** The site's internal links were pointing to the root domain instead of the correct subdirectory path.
    *   **Solution:** The `_config.yml` for any "Project Site" (one that lives in a subdirectory) requires **two** specific URL parameters: `url` and `baseurl`. Open `_config.yml` in the `Public-Library` repository and apply the following configuration:

        **Incorrect:**
        ```yaml
        # This causes 404 errors
        url: https://<your-username>.github.io/Public-Library
        ```

        **Correct:**
        ```yaml
        # This works
        url: https://<your-username>.github.io
        baseurl: /Public-Library
        ```
    This simple change allows Jekyll to correctly build all asset and page links relative to the subdirectory, fixing the 404 errors.

**Expected Result:** Both sites are now correctly configured.

---

#### **Step 5: The Final Push**
**Objective:** Deploy your local changes to GitHub to make the websites live.

1.  **Commit and Push Both Repositories:** In the terminal for each project, run the standard Git cycle.
    ```bash
    # In each project's folder...
    git add .
    git commit -m "feat: Initial site structure and configuration"
    git push
    ```
2.  **Enable GitHub Pages:** On GitHub, go into the **Settings > Pages** tab for **both** repositories and enable deployment from the `main` branch.

**Expected Result:** After 2-5 minutes, your two-site system is live and correctly configured. You can now focus on the important work of filling in the placeholder pages with your high-quality project write-ups and learning notes.

---

### **Summary**

#### **What You Accomplished**
You successfully built and deployed a professional, two-site digital presence. You have a polished portfolio for employers and a separate, scalable library for your public notes, all while practicing a modern, AI-assisted development workflow.

#### **Key Takeaways**
*   Separating a curated portfolio from a public "workshop" creates a more professional presentation.
*   Using an AI Coder can dramatically accelerate the initial, error-prone setup of a complex site structure.
*   Jekyll sites hosted in a subdirectory **must** use the `baseurl` parameter in their configuration to function correctly.