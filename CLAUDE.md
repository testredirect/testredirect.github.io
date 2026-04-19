# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What This Is

A static HTML website for **TestRedirect** — a free online URL redirect checker hosted on GitHub Pages at testredirect.github.io. No build process, no package manager. Files are committed and served as-is via GitHub Pages.

## Development

No build or install step. To preview locally, open any `.html` file directly in a browser.

To deploy: commit and push to `main`. GitHub Pages serves automatically.

## Architecture

**Pure frontend — vanilla JavaScript, Bootstrap 5.3.2, all inline.**

- All CSS lives in `<style>` blocks inside each HTML file (no external stylesheet).
- All JS lives in `<script>` blocks inside each HTML file (no bundler, no modules).
- Bootstrap 5.3.2, Bootstrap Icons 1.11.1, and Google Fonts are loaded from CDN.

**The redirect-checking logic** makes a `POST` to the external API at `https://api.tickspike.com/api/v1/redirect-check/` with `Origin: https://testredirect.github.io`. There is no local processing — all chain analysis happens server-side.

**Key JS functions in `index.html`:**
- `checkRedirect()` — builds and fires the API request
- `showResults()` — renders the redirect chain from the API response
- `escapeHtml()` — XSS guard before injecting user/API data into DOM
- `toggleHopPanel()` — accordion expand/collapse for individual hops

**`bulk-redirect-checker.html`** has its own parallel implementation for batch URL checking.

## Pages

| File | Purpose |
|------|---------|
| `index.html` | Main tool (single URL checker) |
| `bulk-redirect-checker.html` | Batch URL checker |
| `about.html` | About page |
| `contact.html` | Contact / feedback form |
| `404.html` | Custom 404 |
| `privacy-policy.html` | Privacy policy |
| `terms-of-use.html` | Terms of use |

`sitemap.xml` and `robots.txt` are maintained manually — update them when adding or removing pages.

## SEO Conventions

Each page includes: canonical URL, Open Graph tags, Twitter Card tags, and a JSON-LD `WebApplication` structured data block. Follow the existing pattern when editing pages. The Google Site Verification meta tag lives in `index.html`.
