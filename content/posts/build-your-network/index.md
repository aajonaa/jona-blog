---
# Basic Post Information
title: "How To Build Your Local Network / Connect All Device Together"
date: 2025-05-19T20:10:01+08:00
# lastmod: 2025-05-19T20:10:01+08:00
draft: true 

# Author Information
author: "Jona"
# For multiple authors, uncomment and use this format:
# authors: ["Author 1", "Author 2"]

# Content Metadata
description: "Using the tailscale (zerotier) to build yourself local network, your tailnet. Access all your service using the easy remembered domain name (controlled by a tail node running pihole -- global nameserver). Even if you use the exit node, you are still capable of accessing the service using the easy memory domain name (modify /etc/hosts needed in the exit node)."
tags: ["LAN", "Domain"]
categories: ["Self-host"]
weight: 1

# SEO and Canonical URLs
canonicalURL: "https://yourdomain.com/posts/build-your-network"
# Uncomment if you want to prevent search engines from indexing this post
# noindex: true

# Social Media Preview
# These fields are used for Open Graph and Twitter Cards
og_image: images/og-image.jpg
twitter_image: images/twitter-image.jpg

# Cover Image
cover:
    image: images/self_host_network.jpg
    alt: "A self-host network in home."
    caption: "Self-host network"
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
    URL: "https://github.com/yourusername/your-repo/edit/main/content/posts/build-your-network.md"
    Text: "Suggest Changes"
    appendFilePath: true

# Series Information (if this post is part of a series)
series: ["post"]
series_order: 1

# Related Posts (optional)
related:
  - "post-slug-1"
  - "post-slug-2"
---

## How did I make all my device under the same network everywhere
- [Tailscale](https://github.com/tailscale/tailscale) / [Zerotier](https://github.com/zerotier/ZeroTierOne) (I prefer zerotier which have a global nameserver settings -- choose one of the tail node as the DNS server)
- [Pi-hole](https://github.com/pi-hole/pi-hole) (One of the tail node should server as Pi-hole DNS server -- records local hosts domain)

## Additional feature that I had
- Azure server (Tail node serve as exit node for the tail node that want browser website blocked by GFW)
- Alibaba server (Tail node serve as self-hosted cloud storage -- [zfile](https://github.com/zfile-dev/zfile))
- Local server (computer) (Self-hosted photo server [immich](https://github.com/immich-app/immich), self-hosted notes server [trilium](https://github.com/zadam/trilium), self-hosted blog server [hugo](https://github.com/gohugoio/hugo), and self-hosted Zerotier controller (Break the limit of maximum 10 devices in a network) [ztncui](https://github.com/key-networks/ztncui))

## The specific settings that I need to made to make sure I can find host by domain name
- Scenario 1: Connected to tailnet but not using exit node
  - Using tailscale DNS settings (pi-hole DNS server)
  - Configure pi-hole DNS server All Settings -> dns.host value add following content
```bash
100.103.142.83 jona.azure
100.114.162.2 mlm.azure
100.127.20.16 sag.win
100.100.49.115 sag.server
100.100.194.74 dorm.win
100.78.226.36 laptop.ubu
100.111.220.41 sag.ubu
100.68.60.127 laptop.mac
100.69.109.25 mlm.redmi
100.90.2.11 sys.win
100.73.4.19 mlm.win
100.79.185.126 hy.win
100.101.182.107 jona.ali
``` 

- Scenario 2: Connected to tailnet but using exit node
  Configuration that exit node needed to implement:
  - Configure the exit node **`accept-dns=false`**, which means do not use the Tailscale DNS settings, or the DNS query will add the unnecessary two hops. (Since the DNS query will also send to the exit node.)
  - Modify the /etc/hosts file, add above DNS records to make sure the tail node which use this exit node can find the host by domain name


## How I configured those open source server
- *[pi-hole](http://sag.server)*
  - `Curl -sSL https://install.pi-hole.net`
- *[zfile](http://jona.ali)*
  - docker-compose.yml
```bash
services:
  zfile:
    image: zhaojun1998/zfile
    container_name: zfile
    ports:
      - "8443:8080"  # Map port 8443 on the host to 8080 in the container
    volumes:
      - /root/zfile/Files:/data/file
    restart: unless-stopped
```
- *[immich](http://sag.server:2283)*
  - docker-compose.yml and .env
```bash
#
# WARNING: Make sure to use the docker-compose.yml of the current release:
#
# https://github.com/immich-app/immich/releases/latest/download/docker-compose.yml
#
# The compose file on main may not be compatible with the latest release.
#

name: immich

services:
  immich-server:
    container_name: immich_server
    image: ghcr.io/immich-app/immich-server:${IMMICH_VERSION:-release}
    # extends:
    #   file: hwaccel.transcoding.yml
    #   service: cpu # set to one of [nvenc, quicksync, rkmpp, vaapi, vaapi-wsl] for accelerated transcoding
    volumes:
      # Do not edit the next line. If you want to change the media storage location on your system, edit the value of UPLOAD_LOCATION in the .env file
      - ${UPLOAD_LOCATION}:/usr/src/app/upload
      - /etc/localtime:/etc/localtime:ro
    env_file:
      - .env
    ports:
      - '2283:2283'
    depends_on:
      - redis
      - database
    restart: always
    healthcheck:
      disable: false

  immich-machine-learning:
    container_name: immich_machine_learning
    # For hardware acceleration, add one of -[armnn, cuda, openvino] to the image tag.
    # Example tag: ${IMMICH_VERSION:-release}-cuda
    image: ghcr.io/immich-app/immich-machine-learning:${IMMICH_VERSION:-release}
    # extends: # uncomment this section for hardware acceleration - see https://immich.app/docs/features/ml-hardware-acceleration
    #   file: hwaccel.ml.yml
    #   service: cpu # set to one of [armnn, cuda, openvino, openvino-wsl] for accelerated inference - use the `-wsl` version for WSL2 where applicable
    volumes:
      - model-cache:/cache
    env_file:
      - .env
    restart: always
    healthcheck:
      disable: false

  redis:
    container_name: immich_redis
    image: docker.io/redis:6.2-alpine@sha256:2ba50e1ac3a0ea17b736ce9db2b0a9f6f8b85d4c27d5f5accc6a416d8f42c6d5
    healthcheck:
      test: redis-cli ping || exit 1
    restart: always

  database:
    container_name: immich_postgres
    image: docker.io/tensorchord/pgvecto-rs:pg14-v0.2.0@sha256:90724186f0a3517cf6914295b5ab410db9ce23190a2d9d0b9dd6463e3fa298f0
    environment:
      POSTGRES_PASSWORD: ${DB_PASSWORD}
      POSTGRES_USER: ${DB_USERNAME}
      POSTGRES_DB: ${DB_DATABASE_NAME}
      POSTGRES_INITDB_ARGS: '--data-checksums'
    volumes:
      # Do not edit the next line. If you want to change the database storage location on your system, edit the value of DB_DATA_LOCATION in the .env file
      - ${DB_DATA_LOCATION}:/var/lib/postgresql/data
    healthcheck:
      test: pg_isready --dbname='${DB_DATABASE_NAME}' --username='${DB_USERNAME}' || exit 1; Chksum="$$(psql --dbname='${DB_DATABASE_NAME}' --username='${DB_USERNAME}' --tuples-only --no-align --command='SELECT COALESCE(SUM(checksum_failures), 0) FROM pg_stat_database')"; echo "checksum failure count is $$Chksum"; [ "$$Chksum" = '0' ] || exit 1
      interval: 5m
      start_interval: 30s
      start_period: 5m
    command:
      [
        'postgres',
        '-c',
        'shared_preload_libraries=vectors.so',
        '-c',
        'search_path="$$user", public, vectors',
        '-c',
        'logging_collector=on',
        '-c',
        'max_wal_size=2GB',
        '-c',
        'shared_buffers=512MB',
        '-c',
        'wal_compression=on',
      ]
    restart: always

volumes:
  model-cache:
```

```bash
# You can find documentation for all the supported env variables at https://immich.app/docs/install/environment-variables

# The location where your uploaded files are stored
# UPLOAD_LOCATION=./library
UPLOAD_LOCATION=/data/immich-app/library
# The location where your database files are stored
DB_DATA_LOCATION=./postgres

# To set a timezone, uncomment the next line and change Etc/UTC to a TZ identifier from this list: https://en.wikipedia.org/wiki/List_of_tz_database_time_zones#List
# TZ=Etc/UTC

# The Immich version to use. You can pin this to a specific version like "v1.71.0"
IMMICH_VERSION=release

# Connection secret for postgres. You should change it to a random password
# Please use only the characters `A-Za-z0-9`, without special characters or spaces
DB_PASSWORD=YjM1NThjYj

# The values below this line do not need to be changed
###################################################################################
DB_USERNAME=postgres
DB_DATABASE_NAME=immich
```
- *[trilium](http://sag.ubu:8080)*
  - docker-compose.yml
```bash
# Running `docker-compose up` will create/use the "trilium-data" directory in the user home
# Run `TRILIUM_DATA_DIR=/path/of/your/choice docker-compose up` to set a different directory
version: '2.1'
services:
  trilium:
    image: zadam/trilium
    restart: always
    environment:
      - TRILIUM_DATA_DIR=/home/node/trilium-data
    ports:
      - "8080:8080"
    volumes:
      - ${TRILIUM_DATA_DIR:-~/trilium-data}:/home/node/trilium-data

volumes:
  trilium:
```
- *[hugo](http://sag.ubu)*
  - Downloaded the **hugo_extended_withdeploy_0.147.2_linux-amd64.deb** file
  - dpkg -i above_file.deb
  - The commands used for create page bundle post
```bash
 # Function to create a new Hugo page bundle post
 hugoPost() {
   if [ -z "$1" ]; then
     echo -n "Please provide a post title."
     return 1
   fi

   TITLE="$1"  # The original title as input by the user
   SLUG="$TITLE"

   BUNDLE_PATH="content/posts/$SLUG"
   mkdir -p "$BUNDLE_PATH"
   mkdir -p "$BUNDLE_PATH/images"

   # Create the index.md file using Hugo.
   hugo new --kind post "posts/$SLUG/index.md"

   echo "Created post bundle at $BUNDLE_PATH"
   echo "Edit your content in $BUNDLE_PATH/index.md"
 }
```

- *[ztncui](http://us.yourjona.tech)*
  - Build from source
```bash
sudo npm install -g node-gyp

git clone https://github.com/key-networks/ztncui

cd ztncui/src
npm install # You can use mirror if this very slow, install the node-modules

# .env file content under src folder
# TOKEN lies in /var/lib/zerotier-one/authtoken.secret
ZT_TOKEN=bkswwjz8e9hobpt9y4phbss8
HTTP_ALL_INTERFACES=yes
HTTP_PORT=80

cp -v etc/default.passwd etc/passwd # default password is : password

chmod 400 .env
chown root:root .env

npm start # for testing

npm install -g pm2
pm2 start bin/www --name ztncui
pm2 save 
pm2 startup
```