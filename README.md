# Model NASS Website

The official website for [Model NASS](https://modelnass.ng) — a Care for Knowledge initiative.

Built with Jekyll and hosted on GitHub Pages.

---

## How the site is organised

```
modelnass/
├── _data/                  ← ALL routine updates happen here
│   ├── current_session.yml ← Controls the entire homepage
│   ├── sessions.yml        ← Archive of every completed session
│   └── team.yml            ← Steering committee members
│
├── _includes/              ← Shared HTML fragments (nav, footer, etc.)
├── _layouts/               ← Page shells (base.html wraps every page)
├── assets/css/style.css    ← All styles
│
├── images/
│   ├── team/               ← Team member photos
│   └── sessions/
│       ├── 261/            ← Photos for Session 261
│       └── 262/            ← Photos for Session 262 (create when ready)
│
├── index.html              ← Homepage template (do not edit content here)
├── past-sessions/index.html← Archive page template
└── team/index.html         ← Team page template
```

**The three page HTML files are templates — you should rarely need to touch them.** All content lives in `_data/`.

---

## Routine task: promoting a new session on the homepage

When you're ready to advertise a new upcoming session:

1. **Open `_data/current_session.yml`** and update every field:
   - Session number, name, title parts, tagline, subtitle
   - `date_text` (e.g. `"Saturday 14 March 2026 · Lagos"`)
   - `delegate_count`
   - `brief_heading` and `brief_body` paragraphs
   - `factions` (the fault-line cards — add, remove, or rename as needed)
   - `og_title`, `og_description`, `og_image` (for social sharing)
   - `cta_heading` and `cta_body`

2. **Replace the OG/share image** at the path you set in `og_image` (usually `/images/share-preview-v2.png`) with the new session artwork.

3. **Update the registration link** — either edit `register_url` in this file, or update the site-wide default in `_config.yml`.

That's it. The homepage, the "Coming Next" block on the archive page, and the CTA on the team page all update automatically.

---

## Routine task: archiving a completed session

After a session ends, add it to the **top** of `_data/sessions.yml`. Copy and paste the block below, fill in every field, and save.

```yaml
- number: 262
  name: "The Checkmate Initiative"
  tag: "October 2026 Session"
  date: "October 18, 2026"
  delegates: 72
  setting: "Federal Republic of Mona"
  theme: "Gender equity · Legislative reform"

  description:
    - "First paragraph about the session..."
    - "Second paragraph if needed."

  highlights:
    - "Gender equity legislation"
    - "Faith and public policy"
    - "Amendment procedures"

  video_id: "YOUTUBE_ID_HERE"   # the ID after ?v= in the YouTube URL
  report_url: "https://..."     # link to the published report

  photos:
    - "/images/sessions/262/photo-01.jpg"
    - "/images/sessions/262/photo-02.jpg"
```

**Leave `video_id` or `report_url` as `""` if they're not ready yet** — the site hides those elements automatically and shows them as soon as you add the values.

**Leave `photos` as `[]` if photos aren't ready yet** — the gallery section is hidden until photos are added.

---

## Adding session photos

1. Create a folder: `images/sessions/<session-number>/`  
   e.g. `images/sessions/262/`

2. Name your photos clearly: `photo-01.jpg`, `photo-02.jpg`, etc. (JPG or PNG, both fine.)

3. Add the paths to `_data/sessions.yml` under the correct session's `photos:` list:

```yaml
photos:
  - "/images/sessions/262/photo-01.jpg"
  - "/images/sessions/262/photo-02.jpg"
  - "/images/sessions/262/photo-03.jpg"
```

Photos display in the order listed. They link to the full image when clicked.

**Recommended photo dimensions:** 1200×900px (4:3 ratio) for clean display in the grid.

---

## Adding or updating team members

Open `_data/team.yml`. Each member is a block:

```yaml
- name: "Full Name"
  role: "Role Title"
  bio: "One paragraph bio."
  photo: "/images/team/firstname-lastname.jpg"
  linkedin: "https://linkedin.com/in/username/"
  featured: true   # ONLY for the Chairperson — remove this line for all others
```

- Add new members by pasting a new block at the bottom (or wherever in the order you want them in the grid).
- To remove a member, delete their block.
- To update a bio, photo, or LinkedIn, just edit the relevant field.
- Photos go in `/images/team/`. Use the person's name as the filename.
- If someone has no LinkedIn, set `linkedin: ""` — the link will be hidden.

The `featured: true` line on one member renders them in the large Chairperson card at the top. Only one person should have this.

---

## Updating social links, registration URL, or Monapedia URL

These site-wide defaults live in `_config.yml`:

```yaml
register_url: "https://..."
monapedia_url: "https://wiki.modelnass.ng"
instagram_url: "https://instagram.com/modelnassng"
twitter_url:   "https://x.com/modelnassng"
linkedin_url:  "https://linkedin.com/company/modelnassng"
cfk_url:       "https://careforknowledge.org"
```

Note: the registration URL can also be overridden per-session in `_data/current_session.yml` — useful if you use a different form each time. If `register_url` is set there, it takes priority. If it's left blank, the site-wide default from `_config.yml` is used.

---

## Running locally

```bash
bundle install
bundle exec jekyll serve
```

Then open `http://localhost:4000`.

---

## Deployment

The site deploys automatically to GitHub Pages on every push to `main`. No build step needed — just commit and push.
