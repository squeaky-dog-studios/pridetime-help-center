# Agent Instructions: app-help-center

This repo is a **public help/support site** for the PrideTime and PhotoWear (future) watch face app, hosted for
free via GitHub Pages (Jekyll, deployed from the `main` branch). It is maintained by
Squeaky Dog Studios, a small side-project team. Read this whole file before making changes.

## Purpose of this repo

- Contains customer-facing help articles (install instructions, troubleshooting, FAQs).
- Support staff link directly to individual pages from customer support emails
  (via Zoho Desk), often as shortlinks. **Do not rename or move existing files** without
  checking with a human first — it will break links already sent to customers.
- Live site: `https://help.squeaky.dog/`
- Help center namespaces:
  - `https://help.squeaky.dog/pridetime/`
  - `https://help.squeaky.dog/photowear/`
- The `pridetime` and `photowear` app source code lives in **separate, private** repos. Do not assume
  access to it, and do not reference internal implementation details here — everything
  in this repo is public.

## File structure

```
app-help-center/
├── index.md              # homepage app selector — links to PrideTime/PhotoWear centers
├── _config.yml           # Jekyll config, do not remove existing keys without asking
├── pridetime/
│   ├── pridetime.md      # PrideTime landing page (/pridetime/)
│   └── images/           # PrideTime article images
├── photowear/
│   ├── photowear.md      # PhotoWear landing page (/photowear/)
│   └── images/           # PhotoWear article images
└── <article-name>.md     # help articles (can live in root; URL is controlled by permalink)
```

- Use the app-specific folders for assets:
  - PrideTime images in `/pridetime/images/`
  - PhotoWear images in `/photowear/images/`
- Use descriptive, kebab-case image filenames
  (e.g. `install-watch-face-instructions.jpg`), not generic names like `screenshot1.jpg`.

## Front matter

Every page needs Jekyll front matter at the top:

```yaml
---
title: How to Install PrideTime
---
```

Keep titles short and literal — customers scan these, they aren't SEO copy.

For namespace routing, pages also need a `permalink` that starts with the app path:

```yaml
---
title: How to Install PrideTime on Your Watch
permalink: /pridetime/install-watch-face/
---
```

```yaml
---
title: PhotoWear Troubleshooting
permalink: /photowear/troubleshooting/
---
```

- Use `/pridetime/...` permalinks for PrideTime pages.
- Use `/photowear/...` permalinks for PhotoWear pages.
- Keep app landing pages at `/pridetime/` and `/photowear/`.
- Do not use Jekyll posts for help articles; use normal pages with `permalink`.

## Writing style for help articles

- **Audience**: everyday smartwatch users, not developers. Assume no technical
  background. Avoid jargon like "WFF," "companion app push," or "intent" unless it's
  immediately explained in plain language.
- **Tone**: friendly, calm, concise. No marketing language, no exclamation-point
  enthusiasm. The reader is here because something confused them.
- **Structure**: numbered steps for anything sequential. One action per step. Bold the
  specific UI text the user needs to tap (e.g. **Allow**), matching it exactly to what
  appears on screen.
- **Images**: reference screenshots inline right after the step they illustrate, using
  standard Markdown image syntax with `relative_url`, for example:
  `![Step 1: tap the PrideTime icon]({{ '/pridetime/images/install-step1.jpg' | relative_url }})`
  Always include real, descriptive alt text — this is a support/accessibility page, not
  a design portfolio.
- **Length**: keep each article focused on one task. If a troubleshooting topic grows
  past ~5-6 distinct scenarios, propose splitting it into multiple pages rather than
  letting one page sprawl.
- Do not invent product behavior, button labels, or error messages you haven't been
  given. If a step is unclear or unconfirmed, leave a `<!-- TODO: confirm with human -->`
  comment rather than guessing.

## Technical constraints

- This is plain Jekyll on GitHub Pages' free tier — **no custom plugins**, no Ruby gems
  beyond what GitHub Pages supports by default (see GitHub's list of supported themes/
  plugins before adding anything to `_config.yml`).
- No JavaScript build step, no npm, no frameworks. Keep it to Markdown + Jekyll's
  built-in Liquid templating.
- YouTube embeds: use a plain `<iframe>` embed snippet in the Markdown file rather than
  a plugin, since custom plugins aren't supported on the free tier.
- Test that `_config.yml` stays valid YAML — a broken config silently fails the whole
  site build. If you edit it, mention in your summary what you changed and why.

## Workflow expectations

- This repo has no CI/tests to run — the only "build" is GitHub's own Jekyll deploy on
  push to `main`. There's no local preview step required, but if you want to sanity-check
  Markdown rendering, converting to HTML mentally / describing the rendered output to the
  human is sufficient — don't install a local Jekyll toolchain unless asked.
- Commit messages: short and factual (e.g. `Add troubleshooting page for blank watch face`).
- After creating a new article, update navigation so users can reach it:
  - `index.md` should remain the app selector (`/`, linking to `/pridetime/` and `/photowear/`).
  - Each app landing page should list that app's articles.
- When in doubt about tone, structure, or whether something is accurate, ask the human
  rather than guessing — this is a small side project, and incorrect instructions create
  real support burden.

## Non-goals (for now)

- Don't add analytics, cookie banners, ads, or third-party trackers.
- Don't add SEO metadata or a sitemap unless specifically asked — simplicity is the point.
- Don't restructure the repo (subfolders, build tools, etc.) without explicit human
  approval, even if it seems like a technical improvement.

**Custom domain note**: this site uses `help.squeaky.dog`. Keep links domain-agnostic:
prefer `relative_url` with root-relative paths in Markdown/Liquid (for example,
`{{ '/pridetime/' | relative_url }}`) instead of hardcoded full URLs.
