# Dynamic Portfolio & CV — JSONBin CMS

A fully responsive, single-page portfolio and CV website with a built-in admin panel and cloud-based content management via [JSONBin.io](https://jsonbin.io).

`index.html` renders your CV dynamically from cloud data. `admin.html` is a password-protected editor where you manage all content and sync it to JSONBin. Every visitor always sees the latest version — no rebuild or redeploy needed.

---

## Features

| Feature | Details |
|---|---|
| **No-code editing** | Edit all CV content from the admin panel — no file changes needed |
| **Cloud storage** | Content stored on JSONBin (free tier) with auto-compression + chunking |
| **PDF download** | One-click print-to-PDF with a dedicated print layout (name, contacts, all sections) |
| **Projects section** | Card grid for company/personal projects with status badge, role, tech stack |
| **Timeline experience** | Work history rendered as a vertical timeline with accent dots |
| **Scroll spy nav** | Sidebar nav highlights the active section as you scroll |
| **Mobile hamburger** | Collapsible navigation on small screens |
| **Scroll animations** | Fade-in on scroll via IntersectionObserver |
| **Photo upload** | Profile photo uploaded and stored as base64 in JSONBin |
| **CV file link** | Optional direct file download link (e.g. Google Drive PDF) |
| **Contact form** | mailto: form with email validation and status feedback |
| **Password-protected admin** | Default `admin123`, changeable from the settings panel |
| **Auto chunking** | Splits data across multiple JSONBin bins if it exceeds 95 KB |
| **Offline fallback** | Caches last-loaded data in localStorage; shows it if fetch fails |

---

## Tech Stack

- **Frontend** — HTML5, CSS3, Vanilla JavaScript (no frameworks)
- **CMS backend** — [JSONBin.io](https://jsonbin.io) REST API
- **Compression** — [lz-string](https://github.com/pieroxy/lz-string) (`LZString.compressToUTF16`)
- **Fonts** — Google Fonts: Syne (headings) + DM Sans (body)
- **Hosting** — GitHub Pages (or any static host)

---

## File Structure

```
.
├── index.html    — public-facing CV / portfolio
├── admin.html    — password-protected content editor
└── README.md
```

---

## Getting Started

### 1. Create a JSONBin account

Sign up at [jsonbin.io](https://jsonbin.io) (free). Then:

- Click **Create Bin** → name it (e.g. `my-cv`).
- Copy the **Bin ID** from the bin's URL or info panel.
- Copy your **Master Key** (X-Master-Key) from Account → API Keys.

### 2. Configure the admin panel

Open `admin.html` in a browser and log in with the default password **`admin123`**.

Navigate to **Settings → Security & JSONBin**, then:

1. Paste your **Main Bin ID** and **API Key**.
2. Click **Save Config** — this stores the credentials in your browser's `localStorage` only (never sent to any server other than JSONBin).
3. Click **Push to JSONBin** — this uploads the default CV structure to your bin.
4. Optionally change the admin password in the same panel.

### 3. Set your public Bin ID in `index.html`

Open `index.html` in a text editor. Find and update this line near the top of the `<script>` block:

```js
const PUBLIC_BIN_ID = "your_bin_id_here";   // <-- replace with your Bin ID
```

This is the only code change you need to make. The Bin ID is public (read-only fetch, no API key required for reading a public bin).

### 4. Deploy to GitHub Pages

1. Push all files to a GitHub repository named `{your-username}.github.io`.
2. In the repo settings, go to **Pages** → set source to the `main` branch root.
3. Your CV is live at `https://{your-username}.github.io`.

---

## Admin Panel Sections

| Section | What you edit |
|---|---|
| **Hero** | Name, italic word, status tag, subtitle/tagline, badge text, profile photo, CV file URL |
| **Stats** | The 4 highlight numbers shown in the stats bar (e.g. "8+ Years Experience") |
| **Experience** | Work history — period, company, role, description, skill tags |
| **Projects** | Project cards — name, company, period, role, status, description, tech tags |
| **Skills** | Skill category cards — icon, title, description, skill tag list |
| **Education** | Degrees and certifications — degree, school, period, description |
| **Achievements** | Awards and recognition — year, title, organization, description |
| **Contact** | Email, phone, LinkedIn URL, GitHub URL, section blurb, footer text |
| **Settings** | Admin password change, JSONBin config, reset to defaults |

---

## Data Structure

The JSON stored in JSONBin follows this schema:

```json
{
  "hero": {
    "name": "Your Full Name",
    "nameItalic": "Full",
    "tag": "Open to opportunities",
    "subtitle": "Senior Engineer with X+ years...",
    "badge": "Available for work",
    "photoUrl": "data:image/jpeg;base64,...",
    "cvUrl": "https://drive.google.com/..."
  },
  "stats": [
    { "num": "8+", "label": "Years Experience" }
  ],
  "experience": [
    {
      "period": "2022 — Present",
      "company": "Company Name",
      "role": "Senior Engineer",
      "desc": "What you did and the impact.",
      "tags": ["Java", "Spring Boot", "Kubernetes"]
    }
  ],
  "projects": [
    {
      "name": "Project Name",
      "company": "Company Name",
      "period": "2023 — 2024",
      "role": "Backend Developer",
      "status": "live",
      "desc": "What the project does and your contribution.",
      "tech": ["Java", "PostgreSQL", "Docker"]
    }
  ],
  "skills": [
    {
      "icon": "⚙️",
      "title": "Backend",
      "desc": "Server-side development.",
      "items": ["Java", "Spring Boot", "Go"]
    }
  ],
  "education": [
    {
      "degree": "Bachelor of Computer Science",
      "school": "University Name",
      "period": "2016 — 2020",
      "desc": "Thesis / specialization."
    }
  ],
  "achievements": [
    {
      "year": "2024",
      "title": "Award Name",
      "org": "Organization",
      "desc": "What you achieved."
    }
  ],
  "contact": {
    "blurb": "Always happy to chat about new roles or projects.",
    "email": "you@example.com",
    "phone": "+62 8xx xxxx xxxx",
    "linkedin": "https://linkedin.com/in/yourhandle",
    "github": "https://github.com/yourhandle"
  },
  "footer": "© 2025 Your Name"
}
```

**Project `status` values:** `"live"` (green badge) · `"completed"` (blue badge) · `"wip"` (yellow "In Progress" badge)

---

## PDF Download

Click **Download PDF** on the CV page. This calls `window.print()` which opens the browser's print dialog — select **Save as PDF** as the destination.

The print layout automatically:
- Hides the sidebar, hero actions, contact form, and footer
- Shows a dedicated **print header** at the top with your name, subtitle, and contact details
- Flattens the experience timeline into clean text
- Applies `break-inside: avoid` on all cards and experience items

For the best result use Chrome or Edge — they produce the cleanest PDF output.

---

## Security Notes

- The **admin password** is stored in `localStorage` as plain text. This is intentional for a static-site personal tool — it prevents casual access but is not cryptographically secure. Do not use this as a shared multi-user CMS.
- Your **JSONBin API key** is stored in `localStorage` only and is never embedded in `index.html`. The public-facing page fetches data using only the public Bin ID (no key required for reading a public bin).
- All user-supplied content is passed through `escapeHtml()` before insertion into the DOM, covering `&`, `<`, `>`, `"`, and `'`.

---

## Customization

**Change the accent color:** Edit `--accent` in the `:root` block at the top of `index.html`.

**Add a new CV section:** 
1. Add a `<section>` with `data-spy` attribute in `index.html`
2. Add a nav link in the sidebar
3. Add rendering logic in the `render()` function
4. Add a panel and collect/render functions in `admin.html`
5. Add the field to the `DEFAULT` object and `collectAllData()`

**Change fonts:** Replace the Google Fonts `<link>` and update `font-family` references (`'Syne'` for headings, `'DM Sans'` for body).
