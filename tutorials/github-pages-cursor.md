```markdown
---
layout: default
title: Multi-Github-Pages-Cursor
parent: Tutorials
nav_order: 3
---

# High-Speed Portfolio Setup with an AI-Assisted Workflow

This tutorial documents the modern, efficient process for setting up a professional, two-site digital presence using GitHub Pages and an AI Coder (like Cursor or VS Code with an AI extension). The goal is to move from idea to a perfectly structured, live website in minutes, not hours.

**This is a tutorial for high-speed page and file setup, not content creation.** We leverage AI for the tedious and error-prone task of scaffolding, freeing us to focus on the human-centric work of writing valuable content.

**THE FOLLOWING IS AI GENERATED CONTENT BASED ON MY DESCRIPTION OF ACTIONS TAKEN AND ISSUES I FOUND WORKING BETWEEN MULTIPLE INCOMPLETE TUTORIALS**

---

### **The Strategy: A Professional Two-Site System**

To maintain a professional image, we separate our polished work from our learning notes.

1.  **The Portfolio (The "Museum"):** A curated, employer-facing site (`your-username.github.io`) showcasing only your best, completed projects. This is the link on your resume.
2.  **The Public Library (The "Workshop"):** A separate, scalable site (`...github.io/Public-Library`) for your notes, tutorials, references, and works-in-progress. This demonstrates your learning process without cluttering your main portfolio.

---

### **Phase 1: Local Environment Setup**

1.  **Install Tools:** Install [Git](https://git-scm.com/downloads) and your IDE of choice ([VS Code](https://code.visualstudio.com/) or [Cursor](https://cursor.sh/)).
2.  **Configure Git:** Open a terminal and tell Git who you are.
    ```bash
    git config --global user.name "Your Name"
    git config --global user.email "youremail@example.com"
    ```

### **Phase 2: Creating Repositories from the Official Template**

Using the official "Just the Docs" template is the fastest way to get a working base.

1.  **Navigate to the Template:** Go to the [Just the Docs Template Repository](https://github.com/just-the-docs/just-the-docs-template).
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

### **Phase 3: AI-Assisted Scaffolding**

This is the high-speed step. We provide a detailed file map to the AI and instruct it to build the entire structure for both sites.

1.  **Craft the Prompt:** A good prompt is specific. It should define the exact folder structure, file names, and the required YAML Front Matter for every single page.
2.  **Execute the Prompt:** In your AI Coder, open both project folders. Address the AI and provide the prompt below, filling in your specific details. The AI will generate all the necessary folders and placeholder `.md` files in seconds.

#### **The AI Coder Prompt Template:**
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
> *   Project Placeholders: Create placeholder pages for projects like `solidity-project-1.md` inside their respective sub-category folders (e.g., `projects/software-and-code/crypto/`).
>
> **Part 2: Refactor `Public-Library`**
> Create the following structure:
> *   Top-Level Pages: `templates.md`, `references.md`, `tutorials.md`, `project-log.md`.
> *   Populate `templates/` folder: Create `project-report-template.md` and populate it with the provided content. Create other template placeholders.
> *   Structure `references/` folder: Create category pages (`tools-and-tech.md`, `media.md`, `ai-prompts.md`) and then create placeholder pages for all the cheatsheets and resource links inside their respective sub-folders.
> *   Structure `tutorials/` folder: Create placeholder pages for tutorials like `setup-git.md`, `setup-cursor-ide.md`, etc.
>
> **`[Include the full Project Report Template content here at the end of your prompt]`**

### **Phase 4: Configuration & The Critical Subdirectory Fix**

The AI can't know your specific URLs. We must configure the `_config.yml` file for each site manually.

#### **For the Main Portfolio (`your-username.github.io`)**
The configuration is simple. Edit `_config.yml`:
```yaml
title: '<Your Name>: Professional Portfolio'
description: 'A curated collection of my professional projects.'
url: https://<your-username>.github.io
```

#### **A Common Pitfall: The 404 Error on the Second Site**
After deploying, I encountered a `404 Not Found` error for the `Public-Library` site. This is a classic issue when hosting a Jekyll site in a subdirectory.

**The Fix:** The `_config.yml` for any "Project Site" (one that lives in a subdirectory) requires **two** specific URL parameters: `url` and `baseurl`.

1.  **Open `_config.yml` in the `Public-Library` repository.**
2.  **Apply the Correct Configuration:**

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

### **Phase 5: The Final Push**

With the structure built and configured, we finalize the setup.

1.  **Commit and Push Both Repositories:** In the terminal for each project, run the standard Git cycle.
    ```bash
    # In each project's folder...
    git add .
    git commit -m "feat: Initial site structure and configuration"
    git push
    ```
2.  **Enable GitHub Pages:** On GitHub, go into the **Settings > Pages** tab for **both** repositories and enable deployment from the `main` branch.

Your two-site system is now live and correctly configured. You can now focus your time on the important work: filling in the placeholder pages with your high-quality project write-ups and learning notes.
```