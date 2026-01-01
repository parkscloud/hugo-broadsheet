# Getting Started with Hugo

This guide covers installing Hugo and creating a new site with the Broadsheet theme.

## Install Hugo

Hugo Extended is required for Broadsheet (needed for CSS processing).

### Ubuntu/Debian Linux

```bash
sudo snap install hugo --channel=extended
```

### macOS

```bash
brew install hugo
```

### Windows

```bash
choco install hugo-extended
# or
winget install Hugo.Hugo.Extended
```

### Verify Installation

```bash
hugo version
# Should show "extended" in the output
```

For other platforms, see the [official Hugo installation guide](https://gohugo.io/installation/).

## Create a New Site

```bash
# Create a new Hugo site
hugo new site my-news-site
cd my-news-site

# Initialize git
git init
git branch -m main

# Add the Broadsheet theme
git submodule add https://github.com/parkscloud/hugo-broadsheet.git themes/broadsheet
```

## Configure Your Site

Edit `hugo.toml`:

```toml
baseURL = 'https://example.com/'
languageCode = 'en-us'
title = 'My News Site'
theme = 'broadsheet'

[params]
  tagline = "Your tagline here"
  showReadingTime = true

[menu]
  [[menu.main]]
    name = "News"
    url = "/posts/"
    weight = 1
```

## Create Your First Post

```bash
hugo new posts/my-first-article.md
```

Edit `content/posts/my-first-article.md`:

```yaml
---
title: "My First Article"
date: 2026-01-01
draft: false
author: "Your Name"
section: "News"
summary: "A brief description of your article."
featured: true
---

Your article content goes here.
```

## Preview Locally

```bash
hugo server -D
```

Visit http://localhost:1313 to see your site.

## Build for Production

```bash
hugo --minify
```

The generated site is in the `public/` directory, ready to deploy.

## Next Steps

- Read the [Broadsheet README](README.md) for theme configuration options
- Learn more about Hugo at [gohugo.io](https://gohugo.io/documentation/)
- Explore [Hugo's content organization](https://gohugo.io/content-management/organization/)
