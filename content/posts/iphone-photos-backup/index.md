---
# Basic Post Information
title: "How Did I Backup My Iphone Photos"
date: 2025-05-17T17:08:05+08:00
# lastmod: 2025-05-17T17:08:05+08:00
draft: true 

# Author Information
author: "Jona"
# For multiple authors, uncomment and use this format:
# authors: ["Author 1", "Author 2"]

# Content Metadata
description: "With only 64GB storage in my iphone, I have no idea but to make up my way to backup my photos now and then. But how?"
tags: ["Iphone", "Backup", "Photo"]
categories: ["Backup"]
weight: 1

# SEO and Canonical URLs
canonicalURL: "https://yourdomain.com/posts/iphone-photos-backup"
# Uncomment if you want to prevent search engines from indexing this post
# noindex: true

# Social Media Preview
# These fields are used for Open Graph and Twitter Cards
og_image: images/og-image.jpg
twitter_image: images/twitter-image.jpg

# Cover Image
cover:
    image: images/out-of-storage.jpg
    alt: "Text warning of iphone out of storage."
    caption: "Iphone storage warning"
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
    URL: "https://github.com/yourusername/your-repo/edit/main/content/posts/iphone-photos-backup.md"
    Text: "Suggest Changes"
    appendFilePath: true

# Series Information (if this post is part of a series)
series: ["Posts"]
series_order: 1

# Related Posts (optional)
related:
  - "post-slug-1"
  - "post-slug-2"
---

## How I survived under my 6 years old 64GB iphone

### What needed to backup original photos of iphone
- A samba server in the local area (which will be more stable of uploadding)
- A MacOS computer which (I did not tried a black MacOS yet) also connected to this samba server
- External storage (SSD or HDD)

### Backup flow 
Actually before I execute this flow I will backup all my photos to [immich](https://immich.app/), because I will delete all my photos in my iphone after I execute this flow, so I will make sure immich have one copy of current photos.
1. Iphone connect to the samba server
2. Selected all you photos in your iphone 
3. Touch option (make sure the current format and all the information needed) 
4. Export unmodified original to the samba server's shared folder (do not let iphone sleep during this time) 
5. Mac connected to the samba server -> Create a new photo lib (if your prefer a new photo lib) 
6. Open photos app and click import (choose the uploaded folder) 
7. Waiting for the review import finished click the import all new items 
8. Check if all the items are imported 
9. Move this new photo lib to external SSD storage.  
10. Feel free to free your iphone and Mac's storage of photos

### How to setup a samba server
- Mention that samba server support all plateform file format which is good for our backup.
Here are few steps to setup a samba server in linux system
- Install samba software in system
```bash {linenos=false}
apt install samba
```
- Configure the conf file of samba (Add user conf)
```bash {linenos=false}
vim /etc/samba/smb.conf
```
- Add following lines at the end of the smb.conf (the actually storage is on /srv/samba/shared/ folder, and the name of the connected samba folder is CrossPlatformFolder -> the nickname of the /srv/samba/shared/ folder)
```bash
[global]
vfs objects = streams_xattr

[CrossPlatformFolder]
path = /srv/samba/shared
browseable = yes
writable = yes
read only = no
guest ok = no
valid users = jona
```
- After you have configured the conf file, you need to create the actual storage point and the user (create a user called jona and set its password)
```bash {linenos=false}
smbpasswd -a jona
```
- Create the actual storage point (Make sure the user jona have the enough permission over the samba folder)
```bash {linenos=false}
makedir -p /srv/samba/shared/
```
```bash {linenos=false}
chown jona:jona /srv/samba/shared/
```
- Feel free to connect to your samba server now and upload your photos!
