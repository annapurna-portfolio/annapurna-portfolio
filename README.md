# Annapurni Somasundaram — UX/UI Portfolio

A self-contained, static portfolio website. No build step, no framework, no server required —
just HTML, CSS, and vanilla JavaScript.

## Folder structure

```
portfolio/
├── index.html              ← the entire site (all pages are hash-routed inside this one file)
├── README.md                ← this file
└── assets/
    ├── logos/                Brand/company logos used on case-study covers (svg/png)
    ├── thumbs/                Card-grid thumbnail images
    ├── screens/               Real product screenshots used inside case studies
    ├── polaris2/               Polaris case-study assets (real Lenovo UDC screens, logo, cover art)
    ├── xact2/                  X-Act case-study cover art
    ├── ppdm2/                  Dell PPDM case-study cover art
    ├── profile/                 Your portrait + HFI certification badge
    └── resume/                    Your downloadable résumé PDF
```

Every image the site uses is a real file under `assets/` — nothing is base64-inlined, so the
page loads fast and the repo stays easy to browse, diff, and edit.

## How the site works

- **Single page, hash-routed.** `index.html` renders the home page and every case study from
  JavaScript. Case studies live at `#/case/<project-id>` (e.g. `#/case/polaris`). There is no
  separate HTML file per project — everything is generated from one `projects` array near the
  top of the `<script>` tag.
- **No dependencies.** Fonts load from Google Fonts via `<link>` tags; everything else (layout,
  animation, routing) is plain CSS and JS in this one file. It will run by double-clicking
  `index.html` in any modern browser — no `npm install`, no local server needed.

## Previewing locally

Just open `index.html` in a browser. For the smoothest experience (some browsers restrict
`fetch`/asset loading from `file://` URLs), serve it locally instead:

```bash
cd portfolio
python3 -m http.server 8000
# then open http://localhost:8000
```

## Publishing it

This folder is ready to deploy as-is to any static host:

- **Netlify / Vercel** — drag and drop the whole `portfolio` folder onto their dashboard, or
  connect a git repo containing it. No build command needed; the publish directory is the
  folder root.
- **GitHub Pages** — push this folder to a repo and enable Pages on the `main` branch (root).
- **Any static host** (S3, Cloudflare Pages, Firebase Hosting, your own server) — upload the
  folder as-is.

## Editing content

Everything text-based lives inside `index.html`:

- **`const projects = [...]`** — one object per case study: title, summary, tags, meta
  (role/client/duration/tools), and a `blocks` array of `{h, body}` sections that make up the
  case-study page. Add, remove, or reorder projects here.
- **`const SKILLS`** and **`const EXPERIENCE`** — power the About section's skills list and
  work-history timeline.
- **`const CONTACT`** — your email, LinkedIn URL, and the path to your résumé PDF.

To swap an image, drop the new file into the matching `assets/` subfolder and update the path
referenced in the relevant project's `thumb`, `heroShot`, or block content.

To replace your résumé, overwrite
`assets/resume/Annapurni_Somasundaram_Resume.pdf` with the new file (keep the same filename, or
update the path in `CONTACT.resume` inside `index.html`).

## Notes

- The site is fully responsive (desktop, tablet, mobile) and works with keyboard navigation.
- Scroll-reveal animations respect `prefers-reduced-motion`.
- All case-study content reflects real projects, roles, and screenshots — nothing here is
  placeholder or fabricated data.
