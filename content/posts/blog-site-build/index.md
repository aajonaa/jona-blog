---
# Basic Post Information
title: "FAQs / How I build My Hugo Blog Site"
date: 2025-05-13T08:32:52+08:00
# lastmod: 2025-05-13T08:32:52+08:00
draft: true 

# Author Information
author: "Jona"
# For multiple authors, uncomment and use this format:
# authors: ["Author 1", "Author 2"]

# Content Metadata
description: "How I build my hugo blog site, nearly spend 2 or 3 days to finish my site buiding. What hapened during this time, what problem did I encountered, and how I solved the problem." 
tags: ["development", "blog"]
categories: ["DEV"]
weight: 1

# SEO and Canonical URLs
canonicalURL: "https://yourdomain.com/posts/blog-site-build"
# Uncomment if you want to prevent search engines from indexing this post
# noindex: true

# Social Media Preview
# These fields are used for Open Graph and Twitter Cards
og_image: "/images/posts/blog-site-build/og-image.jpg"
twitter_image: "/images/posts/blog-site-build/twitter-image.jpg"

# Cover Image
cover:
    image: DavidGoggins.png
    alt: "Descriptive alt text for the cover image"
    caption: "David Goggins"
    relative: true
    hidden: false

# Table of Contents Settings
showToc: true
TocOpen: false
UseHugoToc: true

# Display Settings
ShowReadingTime: true
ShowBreadCrumbs: true
ShowPostNavLinks: true
ShowWordCount: true
ShowRssButtonInSectionTermList: true

# Content Features
comments: true
disableHLJS: false
disableShare: false
hideSummary: false
searchHidden: false

# Edit Post Link
editPost:
    URL: "https://github.com/yourusername/your-repo/edit/main/content/posts/blog-site-build.md"
    Text: "Suggest Changes"
    appendFilePath: true

# Series Information (if this post is part of a series)
series: ["DEV"]
series_order: 1

# Related Posts (optional)
related:
  - "post-slug-1"
  - "post-slug-2"
---

## My experience of blog site building
I got depression when I know that the mdm web site is handled by Boli Zheng. Before I got this infomation, I have tried to learn the html, css, though very basic, but it did helped me to extend my knowledge. And at least I have some experience of writing the front page of web site. At that time, teacher Yi Chen ask me to build a researcher cv for him, and commit that he will pay me when I finish the web site building with the deadline set to the end of the semester. Before I start to
building the site for him, I have learned and build my own site, called Jona-NDO, not so good a time, but embody my spirit -- No Days Off. Even at this day, I still strive to grow, I am't afraid of dying, but I dare to not success, I dare to fail. It would be very sad to be a failure. Moreover, I want to have a collection of the knowledge or experience what I have learned, so I have also created a website to remember what I have tried and failed or some of the commands of Linux. Actually, I
got to say it is useless. Realize that I have spend so many time doding the work with no paying, sad and frustrated.

## What problem did I encounter when I build this blog site
- The hugo obtained over 80K stars with so fuzzy docs, it is really hard and sad to see. Moreover, the installation by using the package management did not work. The version that downloaded from the package management is really old which no longer suitable to the theme that I want to install. So I found the binary version of deb to install it -- build version.
- There have two branch of the hugo-PaperMod theme, it is the first time that I know when I git clone a repo, all of its branch is cloned, and I can change the branch by issue command 'git checkout branch-name'.
- Config file under the root website folder. Gemimi told me to create a config file to store my hugo.yaml file (initial toml file, hugo new site --format yaml to specify the format). Besides this, there have a root config, a basic config, a development config, and a production config, which can be lies in the \_default folder, development folder, and production folder. No where can I find this but AI. So this can be the drawback of the non-commerical software.
- Understand the hugo folders and the themes folders. I learned those folders function by communicate with Gemini. And I learned that the other config file will override the \_default config file, the root layouts folder will override the themes/layouts folder. Maybe there have some little expression mistake, the config file have no meaning of override, they are merging!
- Change the layout of the pages. I find it is relatively easy compare with the above problems, you can achieve this by chaging the config file.
- The most frusting problem: config file revised while did not take effect, only the command option takes effect. I want to specify a production version blog listen to the default port 1313, bind to 127.0.0.1, and the nginx server it on the port 80, and the baseURL set for 'http://sag.ubu/' with the appendPort=false, so that I can access all the post or all the element in the website throught my local computers (mostly my windows). And the development version blog listen to port 1234, with the baseURL set for 'http://sag.ubu:443', that's because the nginx serve it on port 443, if the baseURL is not 443, then it goes to the other site which I locally can not access it. I mentioned a lot things that is not related to this problem (they are just my setting detail). Actually, my problem is that the server block in the config file will not take effect whatever how hard I have tried. It nearly spend me over 5 hours to find that the problem may lies in the hugo deb binary version.
- Another problem occured after I want to take a rest and finish other of my task -- the search functionality did not include my own posts. Finally find the reason by using the **Cursor** with the AI model **claude-3.7-sonnet**. The reason behind my problem is that the hugo.yaml file had been mistakely changed which remove the outputs block, this block helps to generate the json file of the pages, which are used for further indexing. 

## How long have I spend to build this blog site
- I spend two days to build it blog site. Compare with how I take my time but can not found the solution to make the page suite my need. Now the time is relatively short. But I think it may benefit from the AI's development.

## How many did I have learned to build this blog site
I have learned many git command, the rebase, the remote, the status, the checkout, also the reset, I think all of those can help me in my future career. Besides this, acturally there is little I can know, since there are all the HTML with variables, functions which is hard to understand.

## How many knowledge can I transfer by building this blog site
As I said before, the git -- version control system may helps.

## What you hope to gain throught this blog
I wish I can record as many as I can, including my feelings, my growth, and many of other things. Also I hope I can more familiar with how to organize the paragraphes through markdown.
