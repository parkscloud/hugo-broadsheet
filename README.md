# Broadsheet

A newspaper-style Hugo theme designed for news sites, magazines, and blogs that want the aesthetic of a traditional broadsheet newspaper with modern performance.

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

## Installation

### As a Git Submodule (Recommended)

```bash
cd your-hugo-site
git submodule add https://github.com/raparks/hugo-broadsheet.git themes/broadsheet
```

### Manual Download

Download the theme and extract it to your `themes/broadsheet` directory.

## Configuration

Add to your `hugo.toml`:

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

## Development

To develop the theme locally:

```bash
cd hugo-broadsheet/exampleSite
hugo server --themesDir ../..
```

## License

MIT License - see [LICENSE](LICENSE) for details.

## Credits

- Typography: [Google Fonts](https://fonts.google.com/)
- Icons: [Feather Icons](https://feathericons.com/) (inline SVG)
