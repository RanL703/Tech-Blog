---
title: My Personal Growth Blog Pipeline
date: 2025-02-06
draft: false
tags:
  - blogging
  - tech
---
---
## Tools You’ll Need
- **Obsidian**: My go-to note-taking app for drafting blog posts ([Obsidian.md](https://obsidian.md))].
- **Hugo**: A static site generator for turning Markdown into a website ([gohugo.io](https://gohugo.io)).
- **Git/GitHub**: For version control and free hosting via GitHub Pages.

---

## Step 1: Organize Your Obsidian Vault
1. **Create a `posts` folder**:  
   This will store all your blog drafts in Obsidian.  
   ```bash
   mkdir ~/obsidian-vault/posts
	```
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
   - Install Hugo globally :  
	```bash
		brew install hugo  # Mac
		choco install hugo # Windows
	```

2. **Create a new site**:  
   ```bash
	   hugo new site my-blog && cd my-blog
	   git init
   ```

### Add a Theme (Terminal Theme Example)
You can get the theme of your choice from https://themes.gohugo.io/!
3. **Install as a submodule**:  
   ```bash
	   ## Initialize a git repository (Make sure you are in your Hugo website directory)
	
	git init
	
	## Set global username and email parameters for git
	
	git config --global user.name "Your Name"
	git config --global user.email "your.email@example.com"
	
	
	## Install a theme (we are installing the Terminal theme here). Once downloaded it should be in your Hugo themes folder
	## Find a theme ---> https://themes.gohugo.io/
	
	git submodule add -f https://github.com/panr/hugo-theme-terminal.git themes/terminal
   ```
4. **Configure `hugo.toml`**:  
	We will edit the _hugo.toml_ file to make these changes. In the command line, type
	 `nano hugo.toml` (Linux/Mac) or `notepad hugo.toml` (Windows) or `code hugo.toml` (All platforms)
   ```toml
	baseurl = "/"
	languageCode = "en-us"
	# Add it only if you keep the theme in the `themes` directory.
	# Remove it if you use the theme as a remote Hugo Module.
	theme = "terminal"
	paginate = 5
	
	[params]
	  # dir name of your main content (default is `content/posts`).
	  # the list of set content will show up on your index page (baseurl).
	  contentTypeName = "posts"
	
	  # if you set this to 0, only submenu trigger will be visible
	  showMenuItems = 2
	
	  # show selector to switch language
	  showLanguageSelector = false
	
	  # set theme to full screen width
	  fullWidthTheme = false
	
	  # center theme with default width
	  centerTheme = false
	
	  # if your resource directory contains an image called `cover.(jpg|png|webp)`,
	  # then the file will be used as a cover automatically.
	  # With this option you don't have to put the `cover` param in a front-matter.
	  autoCover = true
	
	  # set post to show the last updated
	  # If you use git, you can set `enableGitInfo` to `true` and then post will automatically get the last updated
	  showLastUpdated = false
	
	  # Provide a string as a prefix for the last update date. By default, it looks like this: 2020-xx-xx [Updated: 2020-xx-xx] :: Author
	  # updatedDatePrefix = "Updated"
	
	  # whether to show a page's estimated reading time
	  # readingTime = false # default
	
	  # whether to show a table of contents
	  # can be overridden in a page's front-matter
	  # Toc = false # default
	
	  # set title for the table of contents
	  # can be overridden in a page's front-matter
	  # TocTitle = "Table of Contents" # default
	
	
	[params.twitter]
	  # set Twitter handles for Twitter cards
	  # see https://developer.twitter.com/en/docs/tweets/optimize-with-cards/guides/getting-started#card-and-content-attribution
	  # do not include @
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
Run this script to copy images from Obsidian’s attachment folder to Hugo’s `static/images` and fix Markdown links :  
```python
import os
import re
import shutil

# Paths
posts_dir = r"C:\Users\RANADEEP LASKAR\Documents\RanaBlog\content\posts"
attachments_dir = r"C:\Users\RANADEEP LASKAR\Documents\Attachments"
static_images_dir = r"C:\Users\RANADEEP LASKAR\Documents\RanaBlog\static\images"

# Step 1: Process each markdown file in the posts directory
for filename in os.listdir(posts_dir):
    if filename.endswith(".md"):
        filepath = os.path.join(posts_dir, filename)
        
        with open(filepath, "r") as file:
            content = file.read()
        
        # Step 2: Find all image links in the format ![Image Description](/images/Pasted%20image%20...%20.png)
        images = re.findall(r'\[\[([^]]*\.png)\]\]', content)
        
        # Step 3: Replace image links and ensure URLs are correctly formatted
        for image in images:
            # Prepare the Markdown-compatible link with %20 replacing spaces
            markdown_image = f"![Image Description](/images/{image.replace(' ', '%20')})"
            content = content.replace(f"[[{image}]]", markdown_image)
            
            # Step 4: Copy the image to the Hugo static/images directory if it exists
            image_source = os.path.join(attachments_dir, image)
            if os.path.exists(image_source):
                shutil.copy(image_source, static_images_dir)

        # Step 5: Write the updated content back to the markdown file
        with open(filepath, "w") as file:
            file.write(content)

print("Markdown files processed and images copied successfully.")

```

---

## Step 5: Deploy to GitHub Pages
5. **Initialize Git** (if not done earlier):  
   ```bash
   git init
   git remote add origin https://github.com/yourusername/your-repo.git
   ```

6. **Build and Push**:  
   ```bash
   hugo -D  # Builds site to /public
   cd public
   git add .
   git commit -m "Deploy blog"
   git push origin main
   ```
7. **Enable GitHub Pages**:  
   - Go to your repo’s **Settings > Pages**.
   - Set the branch to `main` and folder to `/public`.

---

## Final Notes
- **Preview locally**: Run `hugo server -D` to test your site.
- **GitHub Actions (Optional)**: Automate builds using [this workflow example](https://gist.github.com/abstractalgo/7d02299bcf9d3a1b1c94f08860d1dd75) .

---

*Inspired by [NetworkChuck’s blog pipeline](https://blog.networkchuck.com/posts/my-insane-blog-pipeline/). Simplified for GitHub hosting.* 🎉
### Key Adjustments Made:
8. **Removed Hostinger-specific steps** (e.g., `git subtree split` for Hostinger branch).
9. **Simplified deployment** to use GitHub Pages instead of third-party hosting.
10. **Rephrased technical jargon** for readability (e.g., "MEGA SCRIPT" → "Python Script").
11. **Added direct GitHub Pages instructions** for clarity.