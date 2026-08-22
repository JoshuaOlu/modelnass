# Model NASS Website

The official website for [Model NASS](https://modelnass.ng) — a Care for Knowledge initiative.

Built with Jekyll and hosted on GitHub Pages.

---

## How the site is organised

```
modelnass/
├── _data/                   ← ALL routine updates happen here
│   ├── current_session.yml  ← Controls the homepage + nav CTA
│   ├── sessions.yml         ← Archive of every completed session
│   ├── team.yml             ← Steering committee members
│   └── about.yml            ← Programme description (rarely changes)
│
├── _includes/               ← Shared HTML fragments (nav, footer, etc.)
├── _layouts/                ← Page shells (base.html wraps every page)
├── assets/css/style.css     ← All styles
│
├── images/
│   ├── team/                ← Team member photos
│   └── sessions/
│       ├── 261/             ← Photos for Session 261
│       └── 262/             ← Photos for Session 262 (create when ready)
│
├── index.html               ← Homepage template — do not edit content here
├── about/index.html         ← About page template — do not edit content here
├── past-sessions/index.html ← Archive page template
└── team/index.html          ← Team page template
```

**The HTML files are templates. All content lives in `_data/`.
You should almost never need to open an HTML file.**

---

## The site has four modes

The homepage changes entirely depending on the `status` field in
`_data/current_session.yml`. Set it to the right value for what is
currently happening, and the homepage, nav CTA, and past-sessions
banner all update automatically.

| `status` | When to use | Nav CTA | Homepage hero |
|---|---|---|---|
| `recruiting` | Applications are open | Register Now | Full session brief + factions + register CTA |
| `upcoming` | Applications closed, session approaching | Stay in the Loop | Session confirmed, delegates selected, mailing list CTA |
| `just_happened` | Session done, next not yet announced | Express Interest | "Session X just happened" — links to report/video |
| `between` | Nothing imminent | Express Interest | Evergreen programme description + past sessions |

---

## Routine task: starting a new recruitment cycle

1. **Update `_data/current_session.yml`** — fill in all fields:
   - `status: "recruiting"`
   - Session number, name, title parts, tagline, subtitle
   - `date_text` (e.g. `"Saturday 14 March · Lagos"`)
   - `delegate_count`
   - `brief_heading` and `brief_body` paragraphs
   - `factions` (add, remove, or rename as needed)
   - `og_title`, `og_description`, `og_image`
   - `cta_heading` and `cta_body`

2. **Replace the OG/share image** at the path in `og_image`.

3. **Check `register_url`** — either set it in `current_session.yml`,
   or update the site-wide default in `_config.yml`.

---

## Routine task: applications have closed, session is confirmed

1. In `_data/current_session.yml`:
   - Set `status: "upcoming"`
   - Set `confirmed_date` (e.g. `"Saturday, 18 October 2026"`)
   - Set `confirmed_venue` (e.g. `"Civic Centre, Lagos"`) — or leave blank

The homepage hero switches to "Applications closed · Session confirmed".
The session brief section stays visible so visitors can read what delegates will debate.
The nav CTA becomes "Stay in the Loop" pointing to the mailing list form.

---

## Routine task: archiving a completed session

1. **Add the session to the top of `_data/sessions.yml`**:

```yaml
- number: 262
  name: "The Checkmate Initiative"
  tag: "October 2026 Session"
  date: "October 18, 2026"
  delegates: 72
  setting: "Federal Republic of Mona"
  theme: "Gender equity · Legislative reform"

  description:
    - "First paragraph about what happened..."
    - "Second paragraph if needed."

  highlights:
    - "Gender equity legislation"
    - "Faith and public policy"
    - "Amendment procedures"

  video_id: "YOUTUBE_ID_HERE"
  report_url: "https://..."

  photos:
    - "/images/sessions/262/photo-01.jpg"
    - "/images/sessions/262/photo-02.jpg"
```

2. **Set `status: "just_happened"`** in `_data/current_session.yml`.

The homepage hero automatically reads the name, delegate count, date,
and theme from the top entry in `sessions.yml` — no extra fields to fill.

3. **When ready to move to a full between-sessions holding state**,
   set `status: "between"`.

---

## Routine task: leaving fields blank

These fields in `sessions.yml` hide their sections automatically when blank:

- `video_id: ""` → no video embed or YouTube button
- `report_url: ""` → no report button
- `photos: []` → no photo gallery

Fill them in whenever the content is ready — the sections appear immediately.

---

## Adding session photos

1. Create: `images/sessions/<number>/`
2. Add photos named `photo-01.jpg`, `photo-02.jpg`, etc. (JPG or PNG)
3. List paths in `sessions.yml` under that session's `photos:` key

**Recommended size:** 1200×900px (4:3 ratio).
Photos link to the full image when clicked.

---

## Adding or updating team members

Edit `_data/team.yml`. Each member block:

```yaml
- name: "Full Name"
  role: "Role Title"
  bio: "One paragraph bio."
  photo: "/images/team/firstname-lastname.jpg"
  linkedin: "https://linkedin.com/in/username/"
  featured: true   # ONLY for the Chairperson — omit for all others
```

- Photos go in `/images/team/`
- Set `linkedin: ""` to hide the LinkedIn link
- Only one person should have `featured: true`

---

## Updating the mailing list / interest form URL

When no active recruitment is running, the site points visitors to a
"stay in the loop" Google Form. Set the URL in `_config.yml`:

```yaml
interest_url: "https://docs.google.com/forms/YOUR_FORM_URL"
```

---

## Updating social links or Monapedia URL

All in `_config.yml`:

```yaml
monapedia_url: "https://wiki.modelnass.ng"
instagram_url: "https://instagram.com/modelnassng"
twitter_url:   "https://x.com/modelnassng"
linkedin_url:  "https://linkedin.com/company/modelnassng"
cfk_url:       "https://careforknowledge.org"
```

---

## Updating the About page content

The About page is driven by `_data/about.yml`. You should rarely need
to touch it — it describes the programme itself, which doesn't change
between sessions. Edit it if the programme's framing, the delegate
experience, or the long-term vision needs updating.

---

## Running locally

```bash
bundle install
bundle exec jekyll serve
```

Open `http://localhost:4000`.

---

## Deployment

Pushes to `main` deploy automatically via GitHub Pages. No build step needed.
