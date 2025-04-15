---
title: My Personal Growth Blog Pipeline
date: 2025-02-06
draft: false
tags:
  - blogging
  - tech
---
I decided that I will be starting this blog just so I can post more nerdy stuff than non-premium X.com account can handle. :P

---
## Tools You’ll Need

- **Obsidian**: My go-to note-taking app for drafting blog posts ([Obsidian.md](https://obsidian.md)).
- **Hugo**: A static site generator for turning Markdown into a website ([gohugo.io](https://gohugo.io)).
- **Git/GitHub**: For version control (optional, but useful for Vercel integration).
- **Vercel**: For hosting your Hugo site ([vercel.com](https://vercel.com)).

---
## Step 1: Organize Your Obsidian Vault

1. **Create a `posts` folder**:
    This will store all your blog drafts in Obsidian.
	Also note where all your Obsidian directories are using the following steps:
	![Image description](/images/WhatsApp%20Image%202025-02-06%20at%2015.53.50_5254f6f6.jpg)
2. **Note structure**:
    Write posts in Markdown with Hugo-compatible frontmatter:
    ```markdown
    ---
    title: "My First Blog Post"
    date: 2025-02-06
    draft: false
    tags:
      - blogging
      - tech
    ---
    ```
---
## Step 2: Set Up Hugo

### Install Hugo

1. **Prerequisites**:
    - Install [Git](https://git-scm.com) and [Go](https://go.dev/dl).
    - Install Hugo globally:
        ```bash
        brew install hugo # Mac
        choco install hugo # Windows
        ```
2. **Create a new site**:
    ```bash
    hugo new site my-blog && cd my-blog
    git init
    ```
### Add a Theme (Terminal Theme Example)

You can get the theme of your choice from [Hugo Themes](https://themes.gohugo.io/).

3. **Install as a submodule**:
    ```bash
    ## Initialize a git repository (Make sure you are in your Hugo website directory)
    git init
    
    ## Set global username and email parameters for git
    git config --global user.name "Your Name"
    git config --global user.email "your.email@example.com"
    
    ## Install a theme (we are installing the Terminal theme here). Once downloaded it should be in your Hugo themes folder
    git submodule add -f https://github.com/panr/hugo-theme-terminal.git themes/terminal
    ```
4. **Configure `hugo.toml`**:
    Edit your `hugo.toml` file (using `nano hugo.toml`, `notepad hugo.toml`, or `code hugo.toml`) and add or update the configuration:
    ```toml
    baseurl = "/"
    languageCode = "en-us"
    theme = "terminal"
    [pagination]
	    pagerSize = 5
    
    [params]
    contentTypeName = "posts"
    showMenuItems = 2
    showLanguageSelector = false
    fullWidthTheme = false
    centerTheme = false
    autoCover = true
    showLastUpdated = false
    
    [params.twitter]
    creator = ""
    site = ""
    
    [languages]
    
    [languages.en]
    languageName = "English"
    title = "Terminal"
    
    [languages.en.params]
    subtitle = "A simple, retro theme for Hugo"
    owner = ""
    keywords = ""
    copyright = ""
    menuMore = "Show more"
    readMore = "Read more"
    readOtherPosts = "Read other posts"
    newerPosts = "Newer posts"
    olderPosts = "Older posts"
    missingContentMessage = "Page not found..."
    missingBackButtonLabel = "Back to home page"
    minuteReadingTime = "min read"
    words = "words"
    
    [languages.en.params.logo]
    logoText = "Terminal"
    logoHomeLink = "/"
    
    [languages.en.menu]
    [[languages.en.menu.main]]
    identifier = "about"
    name = "About"
    url = "/about"
    
    [[languages.en.menu.main]]
    identifier = "showcase"
    name = "Showcase"
    url = "/showcase"
    ```

---
## Step 3: Sync Obsidian to Hugo

### Automate Content Transfer

- **Windows**:
    Use `robocopy` to mirror your Obsidian `posts` folder to Hugo’s `content/posts`:
    ```powershell
    robocopy "C:\obsidian-vault\posts" "C:\hugo-blog\content\posts" /mir
    ```
- **Mac/Linux**:
    Use `rsync` for the same effect:
    ```bash
    rsync -av --delete ~/obsidian-vault/posts/ ~/hugo-blog/content/posts/
    ```

---
## Step 4: Handle Images

### Python Script for Image Relinking

Run this script to copy images from Obsidian’s attachment folder to Hugo’s `static/images` and fix Markdown links:

```python
import os
import re
import shutil

# Paths
posts_dir = r"C:\Users\RANADEEP LASKAR\Documents\RanaBlog\content\posts"
attachments_dir = r"C:\Users\RANADEEP LASKAR\Documents\Attachments"
static_images_dir = r"C:\Users\RANADEEP LASKAR\Documents\RanaBlog\static\images"

# Process each markdown file in the posts directory
for filename in os.listdir(posts_dir):
    if filename.endswith(".md"):
        filepath = os.path.join(posts_dir, filename)
        with open(filepath, "r") as file:
            content = file.read()

        # Find all image links in the format [[image.png]]
        images = re.findall(r'\[\[([^]]*\.png)\]\]', content)

        # Replace image links and ensure URLs are correctly formatted
        for image in images:
            markdown_image = f"![Image Description](/images/{image.replace(' ', '%20')})"
            content = content.replace(f"[[{image}]]", markdown_image)

            # Copy the image to the Hugo static/images directory if it exists
            image_source = os.path.join(attachments_dir, image)
            if os.path.exists(image_source):
                shutil.copy(image_source, static_images_dir)

        # Write the updated content back to the markdown file
        with open(filepath, "w") as file:
            file.write(content)

print("Markdown files processed and images copied successfully.")
```

---
## Step 5: Deploy to Vercel

1. **Prepare Your Repository** (if not done earlier):
    Initialize Git in your Hugo site directory:
    ```bash
    git init
    git add .
    git commit -m "Initial commit"
    ```
2. **Push Your Repository to GitHub (Optional)**:
    If you prefer integrating Vercel with GitHub for automatic deployments:
    ```bash
    git remote add origin https://github.com/yourusername/your-repo.git
    git push -u origin main
    ```
3. **Deploy Using Vercel**
    You have two options to deploy your Hugo site with Vercel:
    ### Option A: Deploy via the Vercel Dashboard
    - **Sign Up / Log In**: Go to [vercel.com](https://vercel.com) and sign in with your GitHub.
      
    - **Import Your Project**: Click on **"New Project"** and import your GitHub repository.
     ![Image description](/images/WhatsApp%20Image%202025-02-06%20at%2015.53.50_ca57f782.jpg)
    - **Configure Build Settings**:
        - **Framework Preset**: Select **"Hugo"**.
        ![Image description](/images/WhatsApp%20Image%202025-02-06%20at%2015.53.50_ca57f782.jpg)
        - **Output Directory**: Set to `public`.
    - **Deploy**: Click **"Deploy"**. Vercel will build your Hugo site and provide you with a live URL.
     ![Image description](/images/WhatsApp%20Image%202025-02-06%20at%2015.53.50_ca57f782.jpg)
    
    ### Option B: Deploy via the Vercel CLI
    1. **Install Vercel CLI** (if not already installed):
        ```bash
        npm install -g vercel
        ```
    2. **Run Vercel in Your Project Directory**:
        ```bash
        vercel
        ```
        Follow the interactive prompts to link or create a new Vercel project. Vercel will detect your Hugo site and build it accordingly.
    3. **For Production Deployments**, run:
        
        ```bash
        vercel --prod
        ```
        
        This command will deploy your site to production and return the live URL.
        
---
## Final Notes

- **Preview locally**: Run `hugo server -D` to test your site locally.
- **Automate Deployments**: If you push your repository to GitHub and link it with Vercel, every push to your main branch will trigger a new deployment.
- **Environment Variables & Custom Configs**: You can further customize your deployment via the Vercel dashboard or by adding a `vercel.json` configuration file.

_Inspired by [NetworkChuck’s blog pipeline](https://blog.networkchuck.com/posts/my-insane-blog-pipeline/). Simplified for Vercel hosting._ 