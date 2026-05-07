# Jasmine Brittan — Portfolio Website

Personal portfolio website showcasing work at the nexus of engineering and policy.

---

## Table of Contents

1. [Hosting on GitHub Pages](#hosting-on-github-pages)
2. [File Structure](#file-structure)
3. [Privacy Toggle](#privacy-toggle)
4. [Adding New Gallery Tiles](#adding-new-gallery-tiles)
5. [Updating or Replacing Photos](#updating-or-replacing-photos)
6. [Adding a New Photo to an Existing Tile](#adding-a-new-photo-to-an-existing-tile)
7. [Editing Existing Tile Content](#editing-existing-tile-content)
8. [Removing a Tile](#removing-a-tile)
9. [Reordering Tiles](#reordering-tiles)
10. [Updating the About Section](#updating-the-about-section)
11. [Updating the Hero Banner Slides](#updating-the-hero-banner-slides)
12. [Updating the Speaker Section](#updating-the-speaker-section)
13. [Updating the Quote](#updating-the-quote)
14. [Updating Contact Details](#updating-contact-details)
15. [Updating the Nav Bar](#updating-the-nav-bar)
16. [Changing Colours and Fonts](#changing-colours-and-fonts)
17. [Changing the Passcode](#changing-the-passcode)
18. [Adding a Custom Domain](#adding-a-custom-domain)
19. [Quick Reference](#quick-reference)

---

## Hosting on GitHub Pages

1. Create a new GitHub repository (e.g., `jasmine-brittan.github.io` for a user site)
2. Upload **all** the contents of the zip — `index.html`, `README.md`, and the entire `images/` folder — to the root of the repository
3. Go to **Settings → Pages**
4. Under "Source", select **Deploy from a branch** → **main** → **/ (root)**
5. Click Save
6. Your site will be live at `https://your-username.github.io/` within a few minutes

### Updating the live site

Any time you edit `index.html` or add/change images in the `images/` folder and push to GitHub, the live site will automatically update within 1–2 minutes.

---

## File Structure

```
your-repo/
├── index.html          ← The entire website (single file)
├── README.md           ← This guide
└── images/
    ├── profile.jpg
    ├── nasa-1.jpg
    ├── nasa-2.jpg
    ├── cop27.jpg
    ├── chogm-samoa.jpg
    ├── namibia-flags.jpg
    ├── namibia-group.jpg
    ├── patchwork-conference.jpg
    ├── patchwork-no10.jpg
    ├── fulbright.jpg
    ├── baton-bearer.jpg
    ├── pdp-prize.jpg
    ├── upreach.jpg
    ├── brightsparks.jpg
    └── submarine.jpg
```

---

## Privacy Toggle

The site includes a toggle to hide your portfolio behind a passcode screen (useful when applying to finance roles).

- **To hide the site**: Click the small "SITE LIVE" pill in the bottom-right corner
- **To unlock**: Enter the passcode on the lock screen
- **Default passcode**: `jasmine2026`

> **Note**: This is client-side only (uses localStorage). It hides the site visually but doesn't provide true server-side protection. For full privacy, make the GitHub repo private.

---

## Adding New Gallery Tiles

Each section (Engineering, Politics, Awards, Events) uses gallery tiles. Adding a new tile requires **two steps**: adding the HTML tile and adding the modal popup data.

### Step 1: Add the image

1. Save your image to the `images/` folder with a clean filename (e.g., `new-role.jpg`)
2. Keep images under 500KB and in `.jpg` or `.png` format for best performance

### Step 2: Add the gallery card HTML

Find the relevant section in `index.html`. Gallery cards appear in **two places** for each section:
- The **home page** preview (shows ~4–6 tiles with a "View More" button)
- The **full page** (shows all tiles)

You need to add the card to **both** places.

A gallery card with a photo looks like this:

```html
<div class="gallery-card" onclick="openModal('your-unique-id')">
  <div class="gallery-card-img">
    <img src="images/your-image.jpg" alt="Description">
  </div>
  <h3>Title of the Entry</h3>
  <div class="year">2025</div>
</div>
```

If you don't have a photo yet, use a gradient placeholder instead:

```html
<div class="gallery-card" onclick="openModal('your-unique-id')">
  <div class="gallery-card-img gc-1">
    <div class="img-placeholder">ABC</div>
  </div>
  <h3>Title of the Entry</h3>
  <div class="year">2025</div>
</div>
```

Available gradient classes: `gc-1` through `gc-9` (each is a different colour combination).

**Important**: Insert the new tile in date order (newest first). Put it above older entries.

### Step 3: Add the modal popup data

Scroll to the bottom of `index.html` and find the `const modalData = {` section. Add a new entry:

```javascript
'your-unique-id': {
  label: 'Category',           // e.g., 'Engineering', 'Award', 'Conference'
  title: 'Your Title',         // e.g., 'Research Intern'
  org: 'Organisation · 2025',  // e.g., 'Google DeepMind · 2025'
  desc: 'A description of this role, award, or event. This appears in the popup when someone clicks the tile.',
  tag: 'Tag Name'              // e.g., 'AI / Data', 'Scholarship', 'Conference'
},
```

**Make sure**:
- The `'your-unique-id'` matches exactly in both the HTML `onclick="openModal('your-unique-id')"` and the JavaScript
- You include the trailing comma after the closing `}`
- The ID is unique across the whole site (no duplicates)

### Full example: Adding a new engineering role

1. Save the photo as `images/deepmind.jpg`

2. Add the gallery card to **both** the home page engineering section and the full engineering page, at the top (newest first):

```html
<div class="gallery-card" onclick="openModal('eng-deepmind')">
  <div class="gallery-card-img">
    <img src="images/deepmind.jpg" alt="Google DeepMind">
  </div>
  <h3>Research Scientist — DeepMind</h3>
  <div class="year">2026 — Present</div>
</div>
```

3. Add the modal data in the JavaScript section at the bottom:

```javascript
'eng-deepmind': {
  label: 'AI',
  title: 'Research Scientist',
  org: 'Google DeepMind · 2026 — Present',
  desc: 'Working on reinforcement learning for robotics applications.',
  tag: 'AI / Research'
},
```

---

## Updating or Replacing Photos

1. Save the new image to the `images/` folder with the **same filename** as the one you're replacing (e.g., replace `profile.jpg` with your new `profile.jpg`)
2. Push to GitHub — the site updates automatically
3. You may need to hard-refresh your browser (Ctrl+Shift+R / Cmd+Shift+R) to clear the cache

### To add a completely new image:

1. Save it to `images/` with a descriptive name (lowercase, hyphens instead of spaces, e.g., `mit-lab.jpg`)
2. Reference it in the HTML as `images/mit-lab.jpg`

### Image tips:
- **Recommended width**: 1200px max
- **Format**: `.jpg` for photos, `.png` for graphics with transparency
- **Size**: Keep under 500KB per image for fast loading
- **Aspect ratio**: Gallery card images display at 4:3 ratio; photos are cropped to fit via CSS `object-fit: cover`
- **HEIC files**: Convert to `.jpg` before uploading — HEIC is not supported by browsers

---

## Adding a New Photo to an Existing Tile

Find the tile in the HTML. If it currently has a gradient placeholder:

```html
<div class="gallery-card-img gc-1">
  <div class="img-placeholder">BH</div>
</div>
```

Replace the whole inner block with:

```html
<div class="gallery-card-img">
  <img src="images/your-new-image.jpg" alt="Description">
</div>
```

(Remove the `gc-1` class and the `img-placeholder` div.)

---

## Editing Existing Tile Content

### To change a title or year:
Find the gallery card in the HTML and edit the `<h3>` text and/or `.year` div directly.

### To change the popup description:
Find the matching entry in `const modalData = {` near the bottom of the file and edit the `title`, `org`, `desc`, or `tag` values.

---

## Removing a Tile

1. Delete the `<div class="gallery-card" ...>...</div>` block from the HTML — remember it appears in **two places** (home page preview AND the full sub-page)
2. Delete the corresponding entry from `const modalData = {` in the JavaScript
3. Optionally delete the image from the `images/` folder if no other tile uses it

---

## Reordering Tiles

Tiles display in the order they appear in the HTML code. To reorder, cut the entire `<div class="gallery-card">...</div>` block and paste it at the new position.

**Convention used**: Always order newest first (most recent dates at the top of each gallery).

---

## Updating the About Section

The About section has two parts:

### Short version (always visible)
Search for `id="about"` in the HTML. Edit the paragraphs directly within `<div class="about-text">`.

### Expanded version (shown when "Read More" is clicked)
Search for `id="about-expanded"` in the HTML. This contains:
- Three subsections with `<h3>` headings (Engineering Background, Policy & Commonwealth, Research Focus)
- Four stat cards at the bottom (the numbers in the coloured boxes)

Edit any of these directly in the HTML.

### To change the About photo:
Either replace the file `images/profile.jpg` with a new image (keeping the same filename), or change the `src` attribute in:
```html
<div class="about-photo"><img src="images/your-new-photo.jpg" alt="Jasmine Brittan"></div>
```

### To change the tags underneath:
Find `<div class="about-tags">` and add/remove/edit the `<span>` elements.

---

## Updating the Hero Banner Slides

The rotating banner at the top has 4 slides. Each slide looks like this:

```html
<div class="hero-slide">
  <div class="hero-slide-bg" style="background-image:url('images/your-image.jpg')"></div>
  <div class="hero-slide-overlay"></div>
  <div class="hero-slide-content">
    <h1>Your Headline <em>Italic Gold Accent</em></h1>
    <p>Your subtitle text goes here.</p>
  </div>
</div>
```

### To change a slide's background image:
Edit the `background-image:url(...)` value in the `style` attribute.

### To change the text:
Edit the `<h1>` and `<p>` inside `hero-slide-content`. Wrap words in `<em>` tags to make them gold and italic.

### To add or remove slides:
- Add/remove a `<div class="hero-slide">...</div>` block
- Update the dot indicators in `<div class="hero-dots">` — add/remove `<span onclick="goToSlide(N)"></span>` elements to match
- The first slide should have `class="hero-slide active"` and the first dot `class="active"`

### To change rotation speed:
Find this line in the JavaScript and change `8000` (in milliseconds, so 8000 = 8 seconds):
```javascript
setInterval(()=>{goToSlide((currentSlide+1)%slides.length);},8000);
```

---

## Updating the Speaker Section

Search for `Book Me as a Speaker` in the HTML. You can edit:

- The heading and description paragraphs
- **Speaking topics**: Add or remove `<span>` tags inside `<div class="speaker-topics">`
- **Previous speaking credits**: Edit the grey text below the topics
- **Get in Touch button**: Change the `mailto:` email address in the `<a href="mailto:...">` link
- **Speaker photo**: Change the `<img src="...">` path inside `<div class="speaker-img">`

---

## Updating the Quote

Search for `quote-band` in the HTML. Edit:
- The `<blockquote>` text (the quote itself)
- The `<cite>` text (the attribution underneath)

---

## Updating Contact Details

### Email address
Search for `jasminezbrittan@gmail.com` in the file and replace **all** instances. It appears in:
- Speaker section "Get in Touch" button (home page)
- Speaker page "Get in Touch" button (sub-page)
- Footer "Get in Touch" button

### LinkedIn URL
Search for `linkedin.com/in/jasmine-brittan` and replace. It appears in the footer social icon link.

---

## Updating the Nav Bar

The navigation is defined in **two places** (desktop and mobile):

### Desktop nav:
Search for `nav-inner`. The left and right link lists look like:
```html
<ul class="nav-left">
  <li><a href="#" onclick="return showPage('home')" data-page="home">Home</a></li>
  ...
</ul>
```

### Mobile menu:
Search for `mobile-menu`:
```html
<div class="mobile-menu" id="mobile-menu">
  <a href="#" onclick="showPage('home');closeMobile();return false">Home</a>
  ...
</div>
```

To add a completely new tab, you'd need to:
1. Add links in both desktop and mobile nav
2. Create a new `<div class="page" id="page-newname">...</div>` section in the HTML

---

## Changing Colours and Fonts

All colours are defined as CSS variables at the very top of the `<style>` block:

```css
:root {
  --navy: #1b2a4a;        /* Primary dark colour (nav text, headings) */
  --navy-deep: #0f1b33;   /* Deepest dark (footer, speaker block, page heroes) */
  --navy-light: #2c3e6b;  /* Lighter navy (gradients) */
  --gold: #c9a84c;        /* Primary accent (labels, highlights, buttons) */
  --gold-light: #e3c96e;  /* Hover state for gold elements */
  --gold-pale: #f5edda;   /* Light gold background (modal tags) */
  --cream: #faf8f4;       /* Quote band background */
  --white: #ffffff;        /* Page background */
  --text: #2d2d2d;        /* Main body text */
  --text-light: #6b6b6b;  /* Secondary/muted text */
  --border: #e2ddd5;      /* Dividers and borders */
}
```

Change any hex value to update the colour across the entire site instantly.

### Fonts
The site uses three Google Fonts, loaded via the `<link>` tag in the `<head>`:
- **Playfair Display** — all headings (`--heading`)
- **Raleway** — body text, nav, buttons (`--body`)
- **Libre Baskerville** — the quote block (`--accent-font`)

To change fonts:
1. Go to [Google Fonts](https://fonts.google.com/) and pick your fonts
2. Replace the `<link href="https://fonts.googleapis.com/css2?family=...">` URL in the `<head>`
3. Update the font names in the CSS variables

---

## Changing the Passcode

Find this line near the bottom of `index.html` in the `<script>` section:

```javascript
const PASSCODE='jasmine2026';
```

Replace `jasmine2026` with your preferred passcode.

---

## Adding a Custom Domain

1. In your GitHub repo, go to **Settings → Pages**
2. Under "Custom domain", enter your domain (e.g., `jasminebrittan.com`)
3. Create a file called `CNAME` in the repo root containing just your domain name:
   ```
   jasminebrittan.com
   ```
4. Configure your domain's DNS settings to point to GitHub Pages — GitHub provides step-by-step instructions when you enter the domain

---

## Quick Reference

| What you want to do | Where to look in `index.html` |
|---|---|
| Add a gallery tile | Find the section's `<div class="gallery-grid">` + add to `modalData` in JS |
| Change a popup description | Find the ID in `const modalData = {` near the bottom |
| Change a photo | Replace the file in `images/` or change the `src="..."` attribute |
| Edit the About text | Search for `id="about"` and `id="about-expanded"` |
| Edit the expanded About | Search for `id="about-expanded"` |
| Edit hero banner slides | Search for `hero-slide` |
| Change email | Search and replace `jasminezbrittan@gmail.com` |
| Change LinkedIn | Search and replace `linkedin.com/in/jasmine-brittan` |
| Change colours | Edit the `:root` CSS variables at the top of `<style>` |
| Change fonts | Edit the Google Fonts `<link>` URL and CSS variables |
| Change passcode | Edit `const PASSCODE=` near the bottom of `<script>` |
| Change slide rotation speed | Edit the `8000` value in `setInterval` |
| Change the quote | Search for `quote-band` |
| Add/edit speaker topics | Search for `speaker-topics` |

---

## Tech Stack

- Single HTML file — no build step, no dependencies, no frameworks
- Pure HTML, CSS, and vanilla JavaScript
- Google Fonts loaded via CDN
- Fully responsive (mobile, tablet, desktop)
- Scroll-reveal animations
- Sticky navigation with active section highlighting
- Client-side page routing (no page reloads)
