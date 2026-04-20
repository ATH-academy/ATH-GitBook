# Publishing on GitBook

This guide explains how to connect the `ATH-GitBook` repository to GitBook so you get a published site with **sidebar navigation**, **search**, **branding**, and optional custom domain.

<div class="docsify-callout docsify-callout--info">
<p><strong>Prefer Spanish?</strong> The steps are the same; GitBook’s UI can be set to your account language. The important part is syncing this GitHub repo to a Space.</p>
</div>

---

## What GitBook reads from the repo

| File | Role |
|------|------|
| `SUMMARY.md` | **Table of contents** = sidebar structure (order and hierarchy). |
| `README.md` | Home page (usually the first item under Welcome). |
| Other `*.md` files | Pages; paths in `SUMMARY.md` must match real file paths. |

<div class="docsify-callout docsify-callout--info">
<p><strong>Tip:</strong> To change the menu, edit <code>SUMMARY.md</code> only. Section titles use <code>##</code> and pages use <code>* [Label](path/to/file.md)</code>.</p>
</div>

---

## Alternative: GitHub Pages (no GitBook account)

If you want a public docs site **without** GitBook, this repo includes a [Docsify](https://docsify.js.org/) setup:

| File | Role |
|------|------|
| `index.html` | Loads Docsify, search, and theme overrides. |
| `sidebar.md` | Left navigation (mirror `SUMMARY.md` when you change the IA). |
| `.nojekyll` | Tells GitHub Pages not to run Jekyll (so paths and assets behave predictably). |

**Enable Pages:** GitHub → **Settings → Pages →** branch **main**, folder **/**. The default URL is `https://ath-academy.github.io/ATH-GitBook/`.

GitBook-specific blocks such as `{% hint %}` are replaced with plain HTML callout `<div>`s so the same Markdown renders on both GitBook and GitHub Pages.

---

## Steps on gitbook.com

1. Create or open a **Space** at [GitBook](https://www.gitbook.com/).
2. Under **Space settings → Integrations → Git Sync** (or **Import** when creating the space), choose **GitHub** and authorize the account/org that hosts `ATH-GitBook`.
3. Pick the repository and branch (e.g. `main`).
4. Optional **two-way sync**: you can edit in GitBook’s UI or treat Git as source of truth — for docs-as-code, **push to GitHub** and let GitBook rebuild the site.

---

## Making the site look polished

In the Space:

- **Customization → Theme**: brand colors, typography, light/dark.
- **Customization → Header & footer**: logo, links, CTAs.
- **Space → Domains**: custom domain (e.g. `docs.yourdomain.com`) via DNS per GitBook’s wizard.
- **SEO & social**: space title, description, Open Graph image for link previews.

The **sidebar** mirrors `SUMMARY.md`. For a cleaner IA:

- Use `## Group name` blocks in `SUMMARY.md`.
- Keep groups small and use parallel naming (e.g. “User Guide”, “Reference”).

---

## Local preview (optional)

The GitBook CLI has evolved; the reliable preview is the **Space preview** after each sync. If you use GitBook’s CLI locally, follow the current docs at [GitBook Docs](https://docs.gitbook.com/).

---

## Pre-publish checklist

- [ ] Every path in `SUMMARY.md` points to a file that exists in the repo.
- [ ] Images use relative paths or stable absolute URLs.
- [ ] Cross-links use relative paths (e.g. `../user-guide/dashboard.md`).

---

## See also

- [Changelog](../CHANGELOG.md) — documentation history.
- [Introduction](../README.md) — product landing page for this space.
