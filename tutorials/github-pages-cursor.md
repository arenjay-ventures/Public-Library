---
layout: default
title: GitHub Pages Cursor
parent: Tutorials
nav_order: 1
---
# Github-pages-cursor (Using AI for proper Folder and Pages Formatting)

This tutorial shows using cursor as a method of fast formatting folders and page structures for mulitple github-pages, while minimizing the common frontmatter errors.
The example file format below should be updated for your specific goals and intents. Then you can provide the content to the AI assistant in you IDE to complete the update.
After proper pages are made you can fill in your actual project documentation on each page, and have the IDE-AI check you for formatting errors.


**THE FOLLOWING IS AI GENERATED CONTENT BASED ON MY DESCRIPTION OF ACTIONS TAKEN AND ISSUES I FOUND WORKING BETWEEN MULTIPLE INCOMPLETE TUTORIALS**

---

```markdown

# High-Speed Portfolio Setup with an AI-Assisted Workflow

This tutorial documents the modern, efficient process for setting up a professional, two-site digital presence using GitHub Pages and an AI Coder (like Cursor or VS Code with an AI extension). The goal is to move from idea to a perfectly structured, live website in minutes, not hours.

**This is a tutorial for high-speed page and file setup, not content creation.** We leverage AI for the tedious and error-prone task of scaffolding, freeing us to focus on the human-centric work of writing valuable content.

---

### **The Strategy: A Professional Two-Site System**

To maintain a professional image, we separate our polished work from our learning notes.

1.  **The Portfolio (The "Museum"):** A curated, employer-facing site (`your-username.github.io`) showcasing only your best, completed projects. This is the link on your resume.
2.  **The Public Library (The "Workshop"):** A separate, scalable site (`...github.io/Public-Library`) for your notes, tutorials, references, and works-in-progress. This demonstrates your learning process without cluttering your main portfolio.

---

### **Phase 1: Architecture & Planning**

Before writing a single line of code, we map out the entire file structure for **both** sites. This "Information Architecture" plan will become the blueprint for our AI prompt. Thinking this through first prevents messy refactoring later.

*Example: We decided on a structure with top-level pages like "About" and "Projects," with nested sub-categories for different project types like "Homelab" and "Software."*

### **Phase 2: Local Environment Setup**

1.  **Install Tools:** Install [Git](https://git-scm.com/downloads) and your IDE of choice ([VS Code](https://code.visualstudio.com/) or [Cursor](https://cursor.sh/)).
2.  **Configure Git:** Open a terminal and tell Git who you are.
    ```bash
    git config --global user.name "Your Name"
    git config --global user.email "youremail@example.com"
    ```

### **Phase 3: Repository Creation & Cloning**

1.  **Create Repositories on GitHub:**
    *   **Portfolio Repo:** Create a public repository named **exactly** `your-username.github.io`.
    *   **Library Repo:** Create a second public repository named `Public-Library`.

2.  **Clone Both Repositories:** In your terminal, navigate to your projects directory and clone both empty repositories.
    ```bash
    git clone https://github.com/your-username/your-username.github.io.git
    git clone https://github.com/your-username/Public-Library.git
    ```

3.  **Open Workspace:** Open your IDE and add both project folders to your workspace for easy file management.

### **Phase 4: AI-Assisted Scaffolding**

This is the high-speed step. We provide our detailed file map to the AI and instruct it to build the entire structure.

1.  **Craft the Prompt:** A good prompt is specific. It should define the exact folder structure, file names, and the required YAML Front Matter (`title`, `parent`, `nav_order`, etc.) for every single page.
2.  **Execute the Prompt:** In your AI Coder, instruct it to apply the plan to both project folders. The AI will generate all the necessary folders and placeholder `.md` files with perfectly formatted Front Matter in seconds, a task that would take a human 30+ minutes and likely include typos.
3.  **Add the Theme:** Instruct the AI to add the "Just the Docs" theme files (`_config.yml`, `Gemfile`, etc.) to both repositories if they weren't created from a template.

### **Phase 5: Configuration & A Critical Subdirectory Fix**

The AI can't know your specific URLs. We must configure the `_config.yml` file for each site manually.

#### **For the Main Portfolio (`your-username.github.io`)**
The configuration is simple. Edit `_config.yml`:
```yaml
title: 'Your Name: Professional Portfolio'
description: 'A curated collection of my professional projects.'
url: https://your-username.github.io
```

#### **A Common Pitfall: The 404 Error on the Second Site**
After deploying, I encountered a `404 Not Found` error for the `Public-Library` site. This is a classic issue when hosting a Jekyll site in a subdirectory.

**The Problem:** The site's internal links (for CSS, pages, etc.) were pointing to the root domain (`your-username.github.io/style.css`) instead of the correct subdirectory path (`your-username.github.io/Public-Library/style.css`).

**The Fix:** The `_config.yml` for any "Project Site" (one that lives in a subdirectory) requires **two** specific URL parameters: `url` and `baseurl`.

1.  **Open `_config.yml` in the `Public-Library` repository.**
2.  **Apply the Correct Configuration:**

    **Before (Incorrect):**
    ```yaml
    # This causes 404 errors
    url: https://your-username.github.io/Public-Library
    ```

    **After (Correct):**
    ```yaml
    # This works
    url: https://your-username.github.io
    baseurl: /Public-Library
    ```
*   **`url`:** Points to your main GitHub Pages domain.
*   **`baseurl`:** Tells Jekyll that this specific site's root is inside the `/Public-Library` folder.

This simple change allows Jekyll to correctly build all asset and page links relative to the subdirectory, fixing the 404 errors.

### **Phase 6: The Final Push**

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