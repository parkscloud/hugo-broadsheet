# Broadsheet

A newspaper-style Hugo theme designed for news sites, magazines, and blogs that want the aesthetic of a traditional broadsheet newspaper with modern performance.

> **Note:** This theme is in active development (v0.x). The API and features may change before v1.0 stable release.

## Features

- **Newspaper-style masthead** with date, navigation, and site title
- **Multi-column grid layouts** for homepage stories
- **Featured article support** for lead stories
- **Responsive design** optimized for mobile reading
- **Dark mode** with automatic system detection
- **Fast performance** - minimal JavaScript, optimized CSS
- **Clean typography** using Libre Baskerville (headlines) and Source Sans (body)
- **Section labels** for categorizing articles
- **Reading time** estimates
- **SEO optimized** with proper meta tags and semantic HTML

## Requirements

- Hugo Extended v0.112.0 or later (required for SCSS/CSS processing)
- Git (for submodule installation)

## Installation

### Option 1: Git Submodule (Recommended)

This method allows you to easily update the theme and track which version you're using.

```bash
# Navigate to your Hugo site
cd your-hugo-site

# Add the theme as a submodule
git submodule add https://github.com/parkscloud/hugo-broadsheet.git themes/broadsheet

# Initialize and update (if cloning a site that already has the submodule)
git submodule update --init --recursive
```

To update the theme later:

```bash
git submodule update --remote themes/broadsheet
```

### Option 2: Git Clone

If you want to modify the theme directly or don't want to use submodules:

```bash
cd your-hugo-site
git clone https://github.com/parkscloud/hugo-broadsheet.git themes/broadsheet

# Remove .git to avoid nested repo issues
rm -rf themes/broadsheet/.git
```

### Option 3: Download ZIP

1. Download the [latest release](https://github.com/parkscloud/hugo-broadsheet/releases) or [main branch ZIP](https://github.com/parkscloud/hugo-broadsheet/archive/refs/heads/main.zip)
2. Extract to `your-hugo-site/themes/broadsheet/`

### After Installation

Add to your `hugo.toml`:

```toml
theme = 'broadsheet'
```

## Configuration

Full configuration example for `hugo.toml`:

```toml
theme = 'broadsheet'

[params]
  # Site tagline (appears below masthead title)
  tagline = "All the news that's fit to print"

  # Show reading time on articles
  showReadingTime = true

  # Enable search functionality
  enableSearch = true

  # Footer links
  [[params.footerLinks]]
    name = "About"
    url = "/about/"
  [[params.footerLinks]]
    name = "Contact"
    url = "/contact/"

[menu]
  [[menu.main]]
    name = "News"
    url = "/posts/"
    weight = 1
  [[menu.main]]
    name = "Opinion"
    url = "/opinion/"
    weight = 2
  [[menu.main]]
    name = "Technology"
    url = "/tech/"
    weight = 3
```

## Content Front Matter

Posts support the following front matter:

```yaml
---
title: "Article Headline"
date: 2026-01-01
draft: false
author: "Jane Reporter"
section: "Technology"
summary: "A brief summary that appears in article lists and the lead story."
image: "/images/article-image.jpg"
imageCaption: "Photo credit or description"
featured: true  # Makes this the lead story on homepage
tags: ["breaking", "tech"]
---
```

### Front Matter Fields

| Field | Description |
|-------|-------------|
| `title` | Article headline |
| `date` | Publication date |
| `author` | Byline (e.g., "By Jane Reporter") |
| `section` | Section label (e.g., "Technology", "Opinion") |
| `summary` | Brief description for lists and featured display |
| `image` | Featured image path |
| `imageCaption` | Image caption/credit |
| `featured` | Set `true` to make this the lead story |
| `tags` | Array of tags for categorization |

## Homepage Layout

The homepage displays articles in a newspaper-style layout:

1. **Lead Story** - The most recent `featured: true` article (or most recent if none featured)
2. **Secondary Stories** - Next 4 articles in a grid
3. **Latest Stories** - Remaining articles in a list format

## Customization

### Colors

Override CSS custom properties in your own stylesheet:

```css
:root {
  --color-accent: #1a5f7a;  /* Change accent color */
  --font-headline: 'Playfair Display', serif;  /* Different headline font */
}
```

### Typography

The theme uses Google Fonts by default:
- **Headlines:** Libre Baskerville (serif)
- **Body:** Source Sans 3 (sans-serif)

To use different fonts, override the CSS custom properties and update the font imports in a custom `head.html` partial.

## Performance

Broadsheet is built for speed:

- No JavaScript frameworks
- Minimal inline JavaScript for dark mode toggle
- CSS-only layouts (no CSS frameworks)
- System font fallbacks
- Responsive images with lazy loading
- Minified output when built with `hugo --minify`

## Browser Support

- Chrome, Firefox, Safari, Edge (latest versions)
- Mobile browsers (iOS Safari, Chrome for Android)
- Graceful degradation for older browsers

## Versioning

This project uses [Semantic Versioning](https://semver.org/):

- **0.x.y** - Development releases (current)
  - `0.1.0` - Initial release
  - `0.x.0` - New features, may include breaking changes
  - `0.x.y` - Bug fixes and minor improvements
- **1.0.0** - First stable release (when feature-complete and battle-tested)
- **1.x.y** - Stable releases with backward compatibility

**Current status:** Pre-release development. Expect changes to templates, CSS classes, and configuration options before v1.0.

## Development

To develop the theme locally:

```bash
cd hugo-broadsheet/exampleSite
hugo server --themesDir ../..
```

## Contributing

Contributions are welcome! Please open an issue to discuss changes before submitting a PR.

## License

MIT License - see [LICENSE](LICENSE) for details.

## Credits

- Typography: [Google Fonts](https://fonts.google.com/)
- Icons: [Feather Icons](https://feathericons.com/) (inline SVG)
