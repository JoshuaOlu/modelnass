# Model NASS Website

Static site built with Jekyll, hosted on GitHub Pages.

## Folder structure

```
modelnass.ng/
│
├── _config.yml              ← Site-wide settings (URLs, socials, etc.)
├── _layouts/
│   └── base.html            ← The ONE shared HTML shell (head, nav, footer)
├── _includes/
│   ├── nav.html             ← Navigation bar (edit once, updates everywhere)
│   ├── footer.html          ← Footer (edit once, updates everywhere)
│   └── monapedia-banner.html ← "Explore the world" strip, used where needed
│
├── assets/
│   └── css/
│       └── style.css        ← ALL styles (edit once, updates everywhere)
│
├── images/                  ← All images, icons, logos
│   ├── logo.png
│   ├── favicon.png
│   └── team/                ← Team member photos (name them firstname-lastname.jpg)
│
├── index.html               ← Homepage
├── past-sessions/
│   └── index.html           ← Past sessions page
└── team/
    └── index.html           ← Team page
```

## How to add a new page

1. Create a new folder, e.g. `about/`
2. Inside it, create `index.html` starting with:

```html
---
layout: base
title: About
description: One sentence for search engines.
---

<!-- Your page content here. No <html>, no <head>, no nav, no footer. -->
```

That's it. Jekyll handles the rest.

## How to change the nav or footer

Edit `_includes/nav.html` or `_includes/footer.html`. One file, all pages update.

## How to change a colour or font

Edit the `:root` block at the top of `assets/css/style.css`.

## How to change site-wide URLs (register link, Monapedia, socials)

Edit `_config.yml`. The templates pull from there automatically.

## How to add a team member

Open `team/index.html`, copy one `.team-card` block, and fill in the details.
Put their photo in `images/team/` and reference it like:
```html
<img class="team-card-photo" src="/images/team/firstname-lastname.jpg" alt="Name">
```

## How to add a new past session

Open `past-sessions/index.html`, copy one `.session-card` block above the `.next-section` div,
and update the content.

## Local development

```bash
gem install bundler
bundle install
bundle exec jekyll serve
# → open http://localhost:4000
```

## Deploying to GitHub Pages

Push to your `main` branch. GitHub Pages detects Jekyll automatically and builds the site.
No GitHub Actions needed.
