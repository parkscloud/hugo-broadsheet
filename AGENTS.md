# AGENTS.md — Broadsheet theme

Guidance for coding agents (Claude Code, Codex) working in this repository. Robert's cross-project preferences load from his global instructions; this file holds what is specific to the theme.

## What this is

Broadsheet is a Hugo theme with a newspaper look, maintained by Robert Parks. Its main consumer is ap7i.com (`/home/raparks/Documents/GitHub_Repos/ap7i.com`), which links it in as `themes/broadsheet`, a git-ignored symlink to this directory, so an edit here shows up in the site's next build. The site's `AGENTS.md` describes that side, including its local overrides of `head.html`, `footer.html` and `masthead.html`, which shadow the theme's copies.

Shared behavior belongs here, in partials both `head.html` files can call: `page-title.html`, `meta-description.html` (with `trim-to-length.html`) and `schema.html`. The designs behind them live in the site repo: `docs/structured-data-spec.md` and `docs/title-description-length-spec.md`.

## Testing

Build the example site into its own `public/`, which is git-ignored:

```bash
cd exampleSite
hugo --themesDir /home/raparks/Documents/GitHub_Repos --destination public
```

Hugo on Robert's Linux machine is the snap package, which cannot write under `/tmp`, Claude's scratchpad included, so keep test output inside the repository. To try a setting without editing `hugo.toml`, pass it as an environment variable, such as `HUGO_PARAMS_TITLEMAXLENGTH=40`, and build into a second folder you delete afterwards. The fuller test is the ap7i.com build: `hugo --minify`, then `python3 tools/check-head-lengths.py` and `python3 tools/check-structured-data.py` there.

## Template gotchas

- Count characters with `strings.RuneCount`. Go's `len` measures bytes, and Hugo's `countrunes` skips whitespace.
- `default` treats 0 as unset, so a numeric setting where 0 means something (turning a limit off, say) needs `isset site.Params "lowercasedname"`, since Hugo lowercases param keys.
- There is no `i18n/` folder, so wording a site might want to change belongs in a param, as `tagTitleFormat` does.
- AI-crawler welcomes and structured data are opt-in (`robotsAllowAI`, `schema.enable`), as Robert decided on 2026-10-11; fixes such as the length limits are on by default.

## Releasing

1. Update `CHANGELOG.md`: a `## [X.Y.Z] - date` entry under Added, Changed or Fixed. A `0.x.0` release adds features and `0.x.y` holds fixes.
2. Document new settings in `README.md` (configuration example, front matter table, feature list) and as comments in `exampleSite/hugo.toml`.
3. Commit with an imperative subject and a short body, then tag: `git tag -a vX.Y.Z -m "vX.Y.Z: summary"`.
4. Push with tags. This is a personal repository under `parkscloud`; when that `gh` account is active, `git -c credential.helper= -c 'credential.helper=!gh auth git-credential' push origin main --tags` works (the global instructions cover the two GitHub identities).
5. In ap7i.com, record "Bumped to Broadsheet vX.Y.Z" in its CHANGELOG, raise the site version, commit, push and deploy.
