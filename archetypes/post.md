---
# Basic Post Information
title: "{{ replace .Name "-" " " | title }}"
date: {{ .Date }}
# lastmod: {{ .Date }}
draft: true 

# Author Information
author: "Jona"
# For multiple authors, uncomment and use this format:
# authors: ["Author 1", "Author 2"]

# Content Metadata
description: "A brief description of your post that will appear in search results and social media shares"
tags: ["tag1", "tag2"]
categories: ["category1"]
weight: 1

# SEO and Canonical URLs
canonicalURL: "https://yourdomain.com/posts/{{ .Name }}"
# Uncomment if you want to prevent search engines from indexing this post
# noindex: true

# Social Media Preview
# These fields are used for Open Graph and Twitter Cards
og_image: images/og-image.jpg
twitter_image: images/twitter-image.jpg

# Cover Image
cover:
    image: images/cover.jpg
    alt: "Descriptive alt text for the cover image"
    caption: "Image caption or credit"
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
    URL: "https://github.com/yourusername/your-repo/edit/main/content/posts/{{ .Name }}.md"
    Text: "Suggest Changes"
    appendFilePath: true

# Series Information (if this post is part of a series)
series: ["Series Name"]
series_order: 1

# Related Posts (optional)
related:
  - "post-slug-1"
  - "post-slug-2"
---
