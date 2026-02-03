# Markdown → PowerPoint Converter

A client-side Markdown-to-PPTX converter. No backend required — the `.pptx` file is generated entirely in the browser using [PptxGenJS](https://github.com/alanm/PptxGenJS).

---

## Features

- **Slide splitting** — use `---` to start a new slide
- **Two-column layouts** — use `|COL|` to split a slide into left/right columns
- **Image support** — drag images into the image drop-zone, then reference them with `![alt](filename.png)`. Remote URLs also work.
- **6 polished themes** — Midnight Executive, Forest & Moss, Coral Energy, Ocean, Charcoal, Teal Trust
- **16:9 and 4:3** layout options
- **Full Markdown support** — headings, bullets, numbered lists, blockquotes, code blocks, tables, inline bold/italic/code

---

## Syntax Reference

| Syntax | What it does |
|---|---|
| `---` | New slide |
| `# Title` | Slide title |
| `## Heading` | Subtitle or body heading |
| `- item` | Bullet point |
| `1. item` | Numbered list item |
| `> text` | Blockquote |
| `` `code` `` | Inline code |
| ` ```...``` ` | Fenced code block |
| `\|COL\|` | Split slide into two columns |
| `![alt](file.png)` | Insert an uploaded image |
| `\| H1 \| H2 \|` | Markdown table |

### Two-Column Example

```markdown
## My Two-Column Slide

Left column bullet one
- Left bullet two

|COL|

- Right column bullet one
- Right bullet two
```

### Image + Text Two-Column Example

```markdown
## Photo Slide

![My photo](photo.jpg)

|COL|

- Caption line one
- Caption line two
- More details here
```

---

## Deploy to GitHub + Netlify

### Step 1 — Create a GitHub Repository

1. Go to [github.com](https://github.com) and sign in (create a free account if you don't have one).
2. Click the **+** icon in the top-right corner → **New repository**.
3. Name it something like `md-to-pptx`.
4. Leave all the defaults as-is (no README, no `.gitignore`).
5. Click **Create repository**.

### Step 2 — Put the Files in the Repository

#### Option A — Upload through the GitHub web UI (no terminal needed)

1. On your new empty repo page, you'll see the message *"Quick setup — if this is a new repository…"*
2. Click the link that says **creating a new file** (or the upload icon if you see one).
3. For the upload route: click **Upload file** → drag `pandoc-to-pptx.html` into the window.
4. Scroll down, type a commit message like `Initial commit` and click **Commit changes**.

> **Important:** GitHub Pages and Netlify both need an `index.html` at the root. After uploading, rename the file:
> 1. Click on `pandoc-to-pptx.html` in the repo file list.
> 2. Click the pencil ✎ (edit) icon.
> 3. Change the filename at the top from `pandoc-to-pptx.html` to `index.html`.
> 4. Commit the change.

#### Option B — Clone and push from your terminal

```bash
# 1. Clone the empty repo (replace YOUR_USERNAME with your GitHub username)
git clone https://github.com/YOUR_USERNAME/md-to-pptx.git
cd md-to-pptx

# 2. Copy the downloaded file into the folder and rename it
cp /path/to/pandoc-to-pptx.html index.html

# 3. Stage, commit, push
git add index.html
git commit -m "Initial commit — Markdown to PPTX converter"
git push origin main
```

### Step 3 — Deploy on Netlify

1. Go to [netlify.com](https://netlify.com) and sign up for a free account (you can sign in with your GitHub account).
2. From the Netlify dashboard, click **Add a site** → **Import an existing project**.
3. Click **GitHub** as your Git provider.
4. Authorize Netlify to access your GitHub account if prompted.
5. Find and select your `md-to-pptx` repository from the list.
6. On the **Deploy settings** screen:
   - **Base directory:** leave blank
   - **Build command:** leave blank (this is a static single-file site — no build step)
   - **Publish directory:** leave blank (defaults to the repo root)
7. Click **Deploy site**.
8. Wait a few seconds — Netlify will show you a green ✓ and a live URL like `https://your-site-name.netlify.app`.

### Step 4 — You're Live

Open the Netlify URL in a browser. The converter is fully functional — no server, no API keys, nothing to configure.

### Optional — Custom Domain

1. In the Netlify dashboard, go to **Site settings → Domain management**.
2. Click **Add a custom domain** and enter your domain (e.g., `myconverter.example.com`).
3. Follow the DNS instructions Netlify provides (usually adding a `CNAME` record in your domain registrar).

### Optional — Automatic Deploys

Every time you push a new commit to your GitHub repo, Netlify automatically rebuilds and redeploys. No action needed on your end.

---

## How It Works (under the hood)

- The entire app is a single `index.html` file — no bundler, no npm install, no build step.
- **PptxGenJS** is loaded from a CDN (`cdnjs.cloudflare.com`) and runs entirely in the browser.
- Images are read via the `FileReader` API and stored as base64 data URIs in memory.
- The `.pptx` file is generated client-side and downloaded via a programmatic click on a temporary object URL.

---

## License

MIT — use it however you like.
