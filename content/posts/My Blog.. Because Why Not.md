

---
title: My Blog.. Because Why Not
date: 2024-12-01
draft: false
tags:
  - reece
  - blog
---

### Why I, Reece, Am Starting a Blog in 2024

Recently, I came across a video by NetworkChuck titled _I Started a Blog… in 2024 (Why You Should Too)_, and it sparked a realization about how impactful blogging could be—not just as a platform for sharing ideas but as a personal and professional growth tool. Coupled with insights from _Building a Second Brain_ by Tiago Forte, I now see blogging as more than just content creation; it’s an opportunity to organize, refine, and express my thoughts in a way that creates value for myself and others.

Here’s why I’m diving into this and how NetworkChuck’s approach inspired my plan.

---

#### The Power of a Second Brain

Tiago Forte’s concept of a "second brain" is transformative. It emphasizes capturing, organizing, and distilling information so it’s always at your fingertips when you need it. NetworkChuck highlights a key takeaway: **"Your mind is for having ideas, not holding them."**
!![Image Description](/images/Screenshot%202024-12-01%20204857%201.png)
I’ve been using digital tools like Notion and Obsidian to manage my projects, tasks, and ideas. These tools already serve as my second brain, helping me stay organized and focused. Blogging is the natural next step—taking the distilled knowledge from my second brain and sharing it with the world.

---

#### Expressing Ideas: The Missing Link

For the past year, I’ve been building systems, solving technical challenges, and exploring new concepts, but one thing has been missing: **expression.** While I’ve written notes, created workflows, and even built strategies, most of my work stays within my own ecosystem. Blogging will allow me to step out of that bubble, refine my ideas further, and share them with a broader audience.

As Chuck said in his video, "We only know what we make, and it’s only by sharing those ideas that we find out what’s valuable." That hit home for me. I want to take the lessons I’m learning—whether in IT, business, or life—and turn them into something actionable and meaningful for others.

---

#### Building a Legacy

I’m not just starting this blog for the public; I’m doing it for my family, friends, and future generations. Blogging will help me document my journey, share my perspective, and leave behind something tangible. Whether it’s insights about tech, reflections on life as an entrepreneur, or personal interests like blockchain, fitness, and trading, my blog will serve as a dynamic record of who I am and what I value.

!![Image Description](/images/Screenshot%202024-12-01%20222726.png)

---

#### Inspired by NetworkChuck’s Technical Workflow

NetworkChuck’s blogging workflow resonates with me because it’s built for efficiency and creativity. Here’s the pipeline he described—and what I plan to adapt:

1. **Drafting in Obsidian**: Using Obsidian for seamless note-taking and drafting blog posts feels like a perfect fit. It’s already part of my daily workflow.
    
2. **Automating with Hugo**: Transforming markdown files into beautiful websites with Hugo appeals to my love for automation and clean design.
    
3. **Version Control with GitHub**: Pushing blog content to GitHub introduces version control, collaboration opportunities, and a sense of structure to the process.
    
4. **Streamlined Hosting**: Leveraging a hosting provider for automated deployment ensures that my ideas are live with minimal manual effort.
    
5. **Solving Problems with Code**: Python scripts to manage image syncing and other customizations make the process even more tailored to my needs.
    

---
### Setting Up Your Own Blog

Inspired by NetworkChuck’s technical workflow, I want to share how you can set up your own blog from start to finish. Here’s the pipeline I’ve adapted and what you’ll need to get started.

#### Step 1: Setting Up Hugo

**Install Hugo**

1. Install [Git](https://github.com/git-guides/install-git).
    
2. Install [Go](https://go.dev/dl/).
    
3. Install [Hugo](https://gohugo.io/installation/).
    
4. Verify Hugo is installed correctly by running:
    
    ```
    hugo version
    ```

**Create a New Hugo Site**

1. Create your new site by running:
    
    ```
    hugo new site your-site-name
    ```
    
2. Change into the new directory:
    
    ```
    cd your-site-name
    ```
    

**Download a Hugo Theme**

1. Find a theme you like from [Hugo Themes](https://themes.gohugo.io/).
    
2. Install the theme, ideally as a Git submodule:
    
    ```
    git init
    git submodule add https://github.com/theme-author/theme-name.git themes/theme-name
    ```
    

**Adjust Hugo Settings**

1. Open your configuration file (`config.toml`) and edit it according to the theme's documentation.
    
2. Add basic settings like `baseurl`, `languageCode`, and `theme`.
    

#### Step 2: Syncing Obsidian to Hugo

I draft my blog posts in Obsidian. To move your posts from Obsidian to Hugo, you can use a simple script or a command-line tool.

**Windows Users**: Use `robocopy` to sync:

```
robocopy "sourcepath" "destinationpath" /mir
```

**Mac/Linux Users**: Use `rsync`:

```
rsync -av --delete "sourcepath" "destinationpath"
```

#### Step 3: Automating Image Handling with Python

To transfer images referenced in your Markdown files, use the following Python script to ensure all your images are moved to Hugo's `static/images` directory and properly linked.

**Python Script**:

```
import os
import re
import shutil

# Paths (using raw strings to handle Windows backslashes correctly)
posts_dir = r"C:\Users\YourUsername\Documents\YourBlog\content\posts"
attachments_dir = r"C:\Users\YourUsername\Documents\Obsidian\Attachments"
static_images_dir = r"C:\Users\YourUsername\Documents\YourBlog\static\images"

# Step 1: Process each markdown file in the posts directory
for filename in os.listdir(posts_dir):
    if filename.endswith(".md"):
        filepath = os.path.join(posts_dir, filename)

        with open(filepath, "r", encoding="utf-8") as file:
            content = file.read()

        # Step 2: Find all image links in the format ![Image Description](/images/image.png)
        images = re.findall(r'\[\[([^]]*\.png)\]\]', content)

        # Step 3: Replace image links and ensure URLs are correctly formatted
        for image in images:
            image_cleaned = image.strip()
            markdown_image = f"![Image Description](/images/{image_cleaned.replace(' ', '%20')})"
            content = content.replace(f"[[{image}]]", markdown_image)

            # Step 4: Copy the image to the Hugo static/images directory if it exists
            image_source = os.path.join(attachments_dir, image_cleaned)
            if os.path.exists(image_source):
                shutil.copy(image_source, static_images_dir)
            else:
                print(f"Image not found at: '{image_source}'")

        # Step 5: Write the updated content back to the markdown file
        with open(filepath, "w", encoding="utf-8") as file:
            file.write(content)

print("Markdown files processed and images copied successfully.")
```

#### Step 4: Version Control with GitHub

**Initialize a Git Repository**

1. Navigate to your Hugo site directory and initialize a Git repository:
    
    ```
    git init
    ```
    
2. Add your remote repository:
    
    ```
    git remote add origin https://github.com/yourusername/yourrepo.git
    ```
    

**Push Your Changes**

1. Stage and commit your changes:
    
    ```
    git add .
    git commit -m "Initial commit"
    ```
    
2. Push to GitHub:
    
    ```
    git push origin main
    ```
    

#### Step 5: Hosting Your Blog

To host your blog, choose a platform that supports static sites. Many Hugo users opt for platforms like Netlify, Vercel, or GitHub Pages for their simplicity and seamless integration with Git.

**Test Your Site**

1. Run the Hugo server locally to preview your changes:
    
    ```
    hugo server -t theme-name
    ```
    
2. Open your browser and navigate to `http://localhost:1313` to see your blog in action.



---

#### My Blogging Mission

Starting this blog isn’t about becoming an internet influencer or creating viral content. It’s about:

- **Clarity**: Turning scattered ideas into structured content.
- **Legacy**: Leaving behind a record of my thoughts and experiences for family and future generations.
- **Connection**: Sharing insights that might resonate with or help others in their own journeys.
- **Exploration**: Discovering what’s truly valuable by expressing and iterating on my ideas.

---

#### What’s Next

The plan is simple: start where I am, with the tools I have, and let the process evolve. I’ll use Obsidian as my blogging hub, integrate automation with Hugo and GitHub, and publish regularly. Each post will be a small step toward refining my voice and building a repository of knowledge.

This blog is a reflection of everything I’m learning, experimenting with, and striving to achieve. Whether it’s insights on managing IT systems, building a holding company, or creating a healthier lifestyle, I want my blog to capture the essence of my journey.

If you’re thinking about starting a blog, take this as your nudge. Let’s make 2024 the year of expression and connection.

Stay tuned for more as I set this into motion!

