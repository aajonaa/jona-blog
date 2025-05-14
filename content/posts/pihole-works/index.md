---
# Basic Post Information
title: "Yes, Pi-hole Works"
date: 2025-05-15T01:01:45+08:00
# lastmod: 2025-05-15T01:01:45+08:00
draft: true 

# Author Information
author: "Jona"
# For multiple authors, uncomment and use this format:
# authors: ["Author 1", "Author 2"]

# Content Metadata
description: "Pi-hole, the AD-Bloker, works when it server as the DNS server."
tags: ["Pi-hole", "DNS"]
categories: ["self-host"]
weight: 1

# SEO and Canonical URLs
canonicalURL: "https://yourdomain.com/posts/pihole-works"
# Uncomment if you want to prevent search engines from indexing this post
# noindex: true

# Social Media Preview
# These fields are used for Open Graph and Twitter Cards
og_image: images/posts/pihole-works/og-image.jpg
twitter_image: images/posts/pihole-works/twitter-image.jpg

# Cover Image
cover:
    image: pihole-traffic.jpg
    alt: "Pi-hole traffic page"
    caption: "Pi-hole, the DNS server"
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
    URL: "https://github.com/yourusername/your-repo/edit/main/content/posts/pihole-works.md"
    Text: "Suggest Changes"
    appendFilePath: true

# Series Information (if this post is part of a series)
series: ["posts"]
series_order: 1

# Related Posts (optional)
related:
  - "post-slug-1"
  - "post-slug-2"
---

## The effect of Pi-hole
We can seen the difference how the ads shows on in the page ([google scholar mirror website](https://sc.panda985.com/scholar?hl=zh-cn&q=Diease&btwaf=20577410)) with the pi-hole turns on or off.
### Here is how the web page looks like when pi-hole turned off.
{{< figure src="images/search-page-pihole-turned-off" "target=_blank" >}} 

### Here is how to web page looks like when the pi-hole turned off.
{{< figure src=images/search-page-pihole-turned-on "target=_blank">}} 