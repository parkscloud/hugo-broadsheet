# Changelog

All notable changes to the Broadsheet theme are documented here. This project
follows [Semantic Versioning](https://semver.org/) (see the README): `0.x.0`
introduces new features, `0.x.y` is bug fixes and minor improvements. Release
history before `0.8.0` is recorded in the git tag list.

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
