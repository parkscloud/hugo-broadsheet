# Changelog

All notable changes to the Broadsheet theme are documented here. This project
follows [Semantic Versioning](https://semver.org/) (see the README): `0.x.0`
introduces new features, `0.x.y` is bug fixes and minor improvements. Release
history before `0.8.0` is recorded in the git tag list.

## [0.9.2] - 2026-10-11

### Changed

- Footer links from `params.footerLinks` that point to another site
  (`http://` or `https://`) now open in a new tab with
  `rel="noopener noreferrer"`, matching the footer's other outside links.
  Relative links such as `/about/` still open in place. ap7i.com needed this
  for a footer link to Google's preferred-sources tool.

## [0.9.1] - 2026-10-11

### Changed

- Page titles put the page first and the site name last: `Article Title | Site`
  instead of `Site | Article Title`. The homepage keeps `Site | tagline`.
  Search and AI answer engines weigh the opening words of a title, and
  Microsoft's guidance for Copilot asks for titles that summarize the content
  and match the on-page headline. When a long title is truncated in results,
  the cut now falls on the site name rather than the headline.

## [0.9.0] - 2026-10-11

### Added

- A robots.txt template, `layouts/robots.txt`. The example site sets
  `enableRobotsTXT = true`, but with no template in the theme Hugo fell back to
  its embedded one-line default, `User-agent: *`, which lists no sitemap.
  Google Search Console on ap7i.com showed Google fetching exactly that
  14-byte file. The new template allows every crawler and lists the sitemap
  by absolute URL, and it points to `llms.txt` when a site has one.
- `params.robotsAllowAI`, off by default. When true, the robots.txt group also
  names the major search and AI crawlers and adds yes signals for search, AI
  answers, and AI training: `Content-Usage` from the IETF AI preferences
  drafts and `Content-Signal` from Cloudflare's Content Signals. Sites decide
  for themselves; the theme grants nothing beyond plain crawling unless a site
  opts in. ap7i.com is the first to turn it on.

## [0.8.9] - 2026-09-07

### Fixed

- Article titles and headlines in lead stories, cards, and lists now wrap long
  unbroken names within their columns. `overflow-wrap: anywhere` prevents
  horizontal page overflow on narrow screens and allows grid items to shrink
  below a word's intrinsic width. The UnitedHealthcare article on ap7i.com
  exposed the issue at a 390-pixel viewport.

## [0.8.1] - 2026-06-11

### Fixed
- Long unbroken strings (URLs especially) in article body copy overflowed the
  right edge of the page on narrow screens instead of wrapping — most visibly
  inside `.callout` boxes, where a bare autolinked URL extended past both the
  callout background and the viewport. `.article-content` now sets
  `overflow-wrap: break-word`, which inherits to everything in the article body
  (paragraphs, links, callouts, blockquotes, lists), so an overflowing word
  breaks mid-string only when it cannot fit on a line of its own. `break-word`
  was chosen over `anywhere` deliberately: it does not affect min-content
  intrinsic sizing, so table column widths inside the 0.8.0 `.table-scroll`
  containers are unchanged. Desktop rendering is unaffected (the strings fit on
  one line). The existing `.callout pre` rule (`overflow-wrap: anywhere`, for
  preformatted blocks) is unchanged.

## [0.8.0] - 2026-05-23

### Added
- **Mobile SMS / text share button** on single posts. It appears only in the
  mobile view (`max-width: 767px`) and opens the device's default messaging app
  pre-filled with the post headline and URL via an `sms:?&body=` link (the `?&`
  form is accepted by both iOS and Android). It is hidden on desktop, where an
  `sms:` link is not useful. The button reuses the existing `.share-button`
  styling, so it inherits dark-mode colors automatically.
- **Table render hook** (`layouts/_default/_markup/render-table.html`) that wraps
  every Markdown table in a `.table-scroll` container. Wide tables now scroll
  horizontally inside their own box instead of forcing the whole page to scroll
  on narrow screens. Column alignment from the Markdown source is preserved.
- **`urlencode` partial** (`layouts/partials/urlencode.html`) — percent-encodes a
  single string for safe use as a URL query value (`&`, `#`, `%`, spaces, etc.),
  emitting `%20` for spaces so the result is also valid in `mailto:`/`sms:`
  targets (some clients render a `+` literally).

### Changed
- Every share button that embeds the post title in a query string (X, Reddit,
  Email, and the new SMS button) now routes the title — and the email summary —
  through the `urlencode` partial. Previously only spaces were encoded, so a
  headline containing `&` or `#` would truncate the shared text or break the
  link. LinkedIn and Facebook are unchanged (they pass only the URL).
- The visible "Share" text label was removed from the share row on all viewports;
  the row is now icon-only. The container keeps an accessible name via
  `role="group"` and `aria-label="Share"`, and each button retains its own
  `aria-label`.
- `.article-share-buttons` now uses `flex-wrap: wrap` so the icon row wraps
  gracefully instead of overflowing on very narrow screens.

### Fixed
- Narrow-screen (≈320px) horizontal page overflow from two sources: wide post
  tables, and — once the sixth (SMS) share icon was added — the share row itself.
  Both are now contained, so small phones no longer get a horizontal scrollbar.
