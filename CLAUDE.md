# CLAUDE.md

Guidance for AI assistants (Claude Code and others) working in this repository.

## What this is

A single-page personal portfolio website for **Kamaldeep Singh**, a BIM Coordinator & Project Manager (Toronto, ON). It's a static site with no build process, no framework, and no package manager.

## Repository structure

```
index.html    everything — markup, inline <style>, no JS
profile.png   800x800 headshot (currently NOT wired into the page — see "Image placeholders" below)
```

There is no `package.json`, no bundler, no test suite, no linter, and no CI configured. Treat this as a plain static HTML file you edit directly.

## Development workflow

- Edit `index.html` directly with a text editor.
- Preview by opening the file in a browser, or serve it locally if you need relative paths to resolve realistically:
  ```bash
  python3 -m http.server
  ```
- There is nothing to build, install, or compile. There are no automated tests — verify changes by opening the page in a browser and checking the relevant section/breakpoint.
- Deployment is presumably static hosting (e.g. GitHub Pages) serving `index.html` as-is from the repo root — there's no deploy script in this repo.

## Conventions used in `index.html`

**Design tokens** — colors are defined once as CSS custom properties in `:root` and referenced everywhere (`--navy`, `--blue`, `--steel`, `--cream`, `--warm`, `--text`, `--muted`, `--accent`). Don't hardcode hex colors in new rules; use these variables.

**Typography** — two Google Fonts loaded via `<link>` in `<head>`:
- `DM Serif Display` — headings, names, section titles, large display numbers.
- `DM Sans` — body text, nav, labels.

**Page sections** — each `<section>` has an `id` matching a nav anchor in the `<nav>` at the top (`#home`, `#about`, `#experience`, `#projects`, `#contact`). If you add a new top-level section, add a corresponding nav link.

**Section anatomy** — most sections follow this pattern:
```html
<p class="section-label">SMALL UPPERCASE LABEL</p>
<h2 class="section-title">Serif heading</h2>
```
wrapped in `<div class="container">` (`max-width: 1100px`).

**Image placeholders** — none of the photos exist as real assets yet except `profile.png` (which is itself unused). Both the About photo and all six project cards use placeholder `<div>`s with an HTML comment showing the exact `<img>` tag to drop in once a real image is available, e.g.:
```html
<div class="photo-placeholder">
  <!-- Replace with: <img src="profile.png" alt="Kamaldeep Singh"> -->
  <span class="initials">KS</span>
</div>
```
When adding a real image for one of these slots: add the image file to the repo root, then replace the placeholder content with the commented `<img>` tag (don't leave both). Follow the same comment convention for any *new* image placeholder you introduce.

**Responsive behavior** — a single `@media (max-width: 900px)` block near the end of the `<style>` block handles the only breakpoint, mostly collapsing two-column grids to one column and reducing padding. Add responsive overrides there rather than creating new media queries.

**Content data** — experience entries, project cards, and stats are hand-written HTML (no data file/loop). Adding/editing a job or project means duplicating an existing `.exp-item` or `.project-card` block and editing the text in place.

## Things to be careful about

- `index.html` contains real personal contact info (a `mailto:` link with the site owner's email). Don't alter or remove contact details unless explicitly asked.
- Past git history shows this file has been repeatedly overwritten via direct uploads (create/delete/rename cycles) rather than incremental diffs — when editing, use targeted, minimal changes rather than wholesale rewrites, to avoid clobbering content unintentionally.
- Since all CSS is inline in one `<style>` block and there's no scoping, a class-name collision affects the whole page — check existing class names before introducing new ones.
