# Broadsheet

A newspaper-style [Hugo](https://gohugo.io/) theme designed for news sites, magazines, and blogs that want the aesthetic of a traditional broadsheet newspaper with modern performance.

**Live Demo:** [ap7i.com](https://ap7i.com/)

> **Note:** This theme is in active development (v0.x). The API and features may change before v1.0 stable release.

## Features

- **Newspaper-style masthead** with date, navigation, and site title
- **Multi-column grid layouts** for homepage stories
- **Featured article support** for lead stories
- **Responsive design** optimized for mobile reading
- **Dark mode** follows system preference automatically, respecting individual user settings
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

## Dark Mode

Broadsheet automatically adapts to the user's system preference using CSS media queries (`prefers-color-scheme`). There is no manual toggle—the theme respects whatever the user has configured on their device:

- **iOS/Android** users with auto-switching see the theme change with sunrise/sunset
- **Users who prefer dark mode** always see the dark theme
- **Default system users** see the light theme

This approach:
- Respects individual user preferences without requiring interaction
- Eliminates JavaScript for theme switching
- Works immediately on first page load (no flash of wrong theme)

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

Fonts are self-hosted for performance and privacy (no external requests):
- **Headlines:** Libre Baskerville (serif)
- **Body:** Source Sans 3 (sans-serif)

To use different fonts, replace the files in `static/fonts/` and update the `@font-face` declarations in `assets/css/broadsheet.css`.

## Performance

Broadsheet is built for speed:

- **Zero JavaScript** for core functionality (dark mode via CSS media queries)
- **Self-hosted fonts** - no external requests to Google or other CDNs
- CSS-only layouts (no CSS frameworks)
- System font fallbacks for fast initial render
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

### Running the Example Site

The `exampleSite/` directory contains a complete demo site. To run it locally:

```bash
cd hugo-broadsheet/exampleSite
hugo server --themesDir /path/to/parent/of/hugo-broadsheet
```

For example, if your theme is at `/home/user/repos/hugo-broadsheet`:

```bash
cd /home/user/repos/hugo-broadsheet/exampleSite
hugo server --themesDir /home/user/repos
```

### Theme Development

When making changes to the theme, the example site will live-reload automatically.

## Contributing

Contributions are welcome! Please open an issue to discuss changes before submitting a PR.

## License

MIT License - see [LICENSE](LICENSE) for details.

## Third-Party Licenses

This theme includes the following third-party assets, which are distributed under their respective open-source licenses:

### Fonts (SIL Open Font License 1.1)

The fonts included in `static/fonts/` are licensed under the [SIL Open Font License 1.1](https://scripts.sil.org/OFL), which permits:
- Free use in personal and commercial projects
- Modification and redistribution
- Bundling with other software

| Font | Copyright | License File |
|------|-----------|--------------|
| [Libre Baskerville](https://github.com/impallari/Libre-Baskerville) | 2012 Pablo Impallari, Rodrigo Fuenzalida | `static/fonts/LICENSE-LibreBaskerville.txt` |
| [Source Sans 3](https://github.com/adobe-fonts/source-sans) | 2010-2020 Adobe | `static/fonts/LICENSE-SourceSans.md` |

### Icons (MIT License)

| Icon Set | Copyright | License File |
|----------|-----------|--------------|
| [Feather Icons](https://github.com/feathericons/feather) | 2013-2023 Cole Bemis | `static/fonts/LICENSE-FeatherIcons.txt` |

Icons are embedded as inline SVG in templates (no external requests).

## Credits

- Typography: [Libre Baskerville](https://github.com/impallari/Libre-Baskerville) by Pablo Impallari, [Source Sans](https://github.com/adobe-fonts/source-sans) by Adobe
- Icons: [Feather Icons](https://github.com/feathericons/feather) by Cole Bemis
