---
layout: default
title: GitHub Pages Cursor
parent: Tutorials
nav_order: 1
---
# Github-pages-cursor (Using AI for proper Folder and Pages Formatting)

This tutorial shows using cursor as a method of fast formatting folders and page structures for desired github-pages, while minimizing the common frontmatter errors.
The example file format below should be updated for yoru specific goals and intents. Then you can provide the content to the AI assistant in you IDE to complete the update.
After proper pages are made you can fill in your actual project documentation on each page, and have the IDE-AI check you for formatting errors.


**THE FOLLOWING IS AI GENERATED CONTENT BASED ON MY DESCRIPTION OF ACTIONS TAKEN AND ISSUES I FOUND WORKING BETWEEN MULTIPLE INCOMPLETE TUTORIALS**


---

### **Project Tutorial: Building Your Professional Portfolio with an AI-Assisted Workflow**

**Objective:** To efficiently build a free, professional, and fully customizable portfolio website using the "Just the Docs" theme on GitHub Pages. This guide leverages a standard developer workflow (Git, VS Code/Cursor) and introduces an AI assistant to accelerate the tedious initial setup of folders and files, allowing you to focus on creating high-quality project content.

**A Note on AI Usage:** The goal here is to use AI as a smart tool for **structure and formatting**, not for content creation. Your project descriptions and analyses must be your own work. AI makes the process faster; you provide the substance.

**Skills Demonstrated:** `Git`, `GitHub Pages`, `Markdown`, `YAML`, `AI-Assisted Development`, `VS Code/Cursor`, `CLI`, `Technical Documentation`

---

### **Phase 1: AI-Assisted Structuring**

This is where we accelerate the process. Instead of manually creating every folder and file and risking typos in the Front Matter, we will instruct an AI assistant like Cursor to do it for us. This ensures a perfectly formatted structure from the start.

#### **Step 1: Prompting the AI for Structure**

In your IDE (Cursor or VS Code with an AI extension), open a chat window and provide a clear, detailed prompt. The key to a good prompt is to be specific about the file names, folder hierarchy, and the exact Front Matter content.

**The Prompt:**

> **Prompt for AI Assistant:**
>
> "You are an expert in setting up Jekyll sites with the 'Just the Docs' theme. Based on the project list I provide, please generate the necessary folder and file structure inside my current project directory.
>
> For each Markdown (`.md`) file, you must create the file with the correct YAML Front Matter to ensure the navigation sidebar is perfectly nested. Do not generate the main content for the pages; use `(Coming Soon)` as a placeholder under the main heading.
>
> Here is the desired structure:
>
> 1.  **Top-Level Pages:**
>     *   `about.md` (nav_order: 2)
>     *   `projects.md` (nav_order: 3, has_children: true)
>     *   `contact.md` (nav_order: 5)
>
> 2.  **'Projects' Main Categories (inside the `projects` folder):**
>     *   `foundations.md` (Parent: Projects, nav_order: 1, has_children: true)
>     *   `cyber-defense.md` (Parent: Projects, nav_order: 2, has_children: true)
>     *   `engineering-and-pentesting.md` (Parent: Projects, nav_order: 3, has_children: true)
>
> 3.  **Project Pages (nested inside their category folders):**
>     *   Under `projects/foundations/`:
>         *   `linux-lab-and-wireshark.md`
>         *   `python-log-parser.md`
>     *   Under `projects/cyber-defense/`:
>         *   `home-lab-siem-monitoring.md`
>         *   `aws-ec2-hardening.md`
>         *   `python-threat-intel-tool.md`
>     *   Under `projects/engineering-and-pentesting/`:
>         *   `secure-aws-vpc-with-terraform.md`
>         *   `penetration-testing-report.md`
>
> Remember to correctly set the `title`, `parent`, `grand_parent`, `nav_order`, and `has_children` properties in the YAML Front Matter for every file."

#### **Step 2: Review and Verify**
After the AI generates the files, quickly review them. Check that the folders are named correctly and that the `parent` and `grand_parent` values in the Front Matter match the `title` of their parent pages exactly. The AI is excellent at this, but a quick human check is always good practice.

---

### **Phase 2: The Human Workflow - Edit, Commit, Push**

With the tedious structuring done, you can now focus on the most important part: creating the content that represents your skills.

#### **Step 3: Configure and Commit Your Initial Site**

1.  Open the `_config.yml` file. Edit the `title` and `description` to your liking, remembering to wrap any values containing special characters in quotes.
2.  Save all your files.
3.  Now, commit this entire initial structure to your repository. Open the integrated terminal:
    ```bash
    # Stage all the new files and changes
    git add .

    # Commit the changes with a clear message
    git commit -m "feat: Initial site structure and configuration via AI assistant"

    # Push the changes to GitHub
    git push
    ```

By following this AI-assisted workflow, you've dramatically reduced the setup time and eliminated a common source of frustrating errors, allowing you to jump straight into the meaningful work of documenting your projects.
