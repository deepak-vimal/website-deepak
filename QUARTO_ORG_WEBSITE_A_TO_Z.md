# Build Your Organization Website in RStudio + Quarto (A to Z)

This guide explains how to create a website similar in structure to <https://vaagdhara.org/> using **RStudio + Quarto**, while customizing:
- navbar items
- site icon/favicon
- logo
- homepage text
- auto-sliding image carousel with text overlay

---

## 0) What you need

- R (latest stable)
- RStudio (latest stable)
- Quarto (latest stable)

Install Quarto: <https://quarto.org/docs/get-started/>

Check installation in terminal:

```bash
quarto check
```

---

## 1) Create project in RStudio

1. Open **RStudio**.
2. Go to **File → New Project → New Directory → Quarto Website**.
3. Name your project (example: `my-org-website`).
4. Click **Create Project**.

You will get key files like:
- `_quarto.yml` (site config)
- `index.qmd` (home page)
- extra `.qmd` pages

---

## 2) Understand website structure

Recommended folder layout:

```text
my-org-website/
├─ _quarto.yml
├─ index.qmd
├─ about.qmd
├─ programs.qmd
├─ contact.qmd
├─ styles.css
├─ images/
│  ├─ logo.png
│  ├─ hero1.jpg
│  ├─ hero2.jpg
│  └─ hero3.jpg
└─ docs/            # generated website output (optional)
```

> Keep images in `images/` and use clean filenames.

---

## 3) Configure site basics in `_quarto.yml`

Use this starter config and edit names/colors/links:

```yaml
project:
  type: website
  output-dir: docs

website:
  title: "Your Organization Name"
  favicon: images/logo.png
  navbar:
    logo: images/logo.png
    left:
      - href: index.qmd
        text: Home
      - href: about.qmd
        text: About
      - href: programs.qmd
        text: Programs
      - href: contact.qmd
        text: Contact
    right:
      - icon: facebook
        href: https://facebook.com/yourpage
      - icon: instagram
        href: https://instagram.com/yourpage
      - icon: youtube
        href: https://youtube.com/@yourchannel

format:
  html:
    theme: cosmo
    css: styles.css
    toc: false
```

What you can change quickly:
- `title` → site name
- `favicon` and `navbar.logo` → your branding
- `navbar.left/right` → menu and social icons
- `theme` and `css` → look and feel

---

## 4) Create your pages

Create/edit these files:

- `index.qmd` (homepage)
- `about.qmd`
- `programs.qmd`
- `contact.qmd`

Example `about.qmd`:

```markdown
---
title: "About"
---

## Who We Are

We are a community-focused organization working on education, livelihood, and local governance.
```

---

## 5) Add homepage carousel with text overlay (auto sliding)

In `index.qmd`, add this full block:

```markdown
---
title: "Home"
---

<div id="homeCarousel" class="carousel slide" data-bs-ride="carousel" data-bs-interval="3000">
  <div class="carousel-indicators">
    <button type="button" data-bs-target="#homeCarousel" data-bs-slide-to="0" class="active" aria-current="true" aria-label="Slide 1"></button>
    <button type="button" data-bs-target="#homeCarousel" data-bs-slide-to="1" aria-label="Slide 2"></button>
    <button type="button" data-bs-target="#homeCarousel" data-bs-slide-to="2" aria-label="Slide 3"></button>
  </div>

  <div class="carousel-inner rounded-4 shadow">
    <div class="carousel-item active">
      <img src="images/hero1.jpg" class="d-block w-100 carousel-img" alt="Community work 1">
      <div class="carousel-caption custom-caption">
        <h2>Empowering Communities</h2>
        <p>Building sustainable futures together.</p>
      </div>
    </div>

    <div class="carousel-item">
      <img src="images/hero2.jpg" class="d-block w-100 carousel-img" alt="Community work 2">
      <div class="carousel-caption custom-caption">
        <h2>Education for All</h2>
        <p>Supporting children, youth, and families.</p>
      </div>
    </div>

    <div class="carousel-item">
      <img src="images/hero3.jpg" class="d-block w-100 carousel-img" alt="Community work 3">
      <div class="carousel-caption custom-caption">
        <h2>Inclusive Growth</h2>
        <p>Local partnerships for lasting change.</p>
      </div>
    </div>
  </div>

  <button class="carousel-control-prev" type="button" data-bs-target="#homeCarousel" data-bs-slide="prev">
    <span class="carousel-control-prev-icon" aria-hidden="true"></span>
    <span class="visually-hidden">Previous</span>
  </button>
  <button class="carousel-control-next" type="button" data-bs-target="#homeCarousel" data-bs-slide="next">
    <span class="carousel-control-next-icon" aria-hidden="true"></span>
    <span class="visually-hidden">Next</span>
  </button>
</div>

## Welcome to Our Organization

Write your homepage intro here (mission, impact, location, call-to-action).
```

- `data-bs-ride="carousel"` enables auto slide
- `data-bs-interval="3000"` changes slide every 3 seconds
- text inside `.carousel-caption` appears over image

---

## 6) Style the carousel and navbar in `styles.css`

```css
/* Brand logo sizing in navbar */
.navbar-brand img {
  max-height: 42px;
}

/* Carousel image height and crop behavior */
.carousel-img {
  height: 70vh;
  object-fit: cover;
}

/* Text overlay style */
.custom-caption {
  background: rgba(0, 0, 0, 0.45);
  border-radius: 12px;
  padding: 1rem 1.25rem;
}

.custom-caption h2,
.custom-caption p {
  color: #fff;
}

/* Small screen adjustments */
@media (max-width: 768px) {
  .carousel-img {
    height: 45vh;
  }

  .custom-caption h2 {
    font-size: 1.2rem;
  }

  .custom-caption p {
    font-size: 0.9rem;
  }
}
```

---

## 7) Add more sections to homepage

Below carousel in `index.qmd`, add quick blocks:

- Mission
- Key programs
- Latest updates
- Donate/Volunteer button

Example:

```markdown
## Our Mission

To strengthen local communities through rights-based development.

## Key Programs

- Education and Child Rights
- Women and Livelihood
- Natural Resource Governance
```

---

## 8) Add contact + map + social links

In `contact.qmd`:

```markdown
---
title: "Contact"
---

## Contact Us

**Address:** Your office address

**Email:** info@yourorg.org  
**Phone:** +91-XXXXXXXXXX

[Google Maps Location](https://maps.google.com)
```

---

## 9) Preview locally

Use either:

- RStudio **Render** button, or
- terminal:

```bash
quarto preview
```

This starts a local server and auto-refreshes when you edit files.

---

## 10) Build final website

```bash
quarto render
```

If `output-dir: docs` is set, your site files will be generated in `docs/`.

---

## 11) Deploy (easy option: GitHub Pages)

1. Push project to GitHub.
2. Open repository **Settings → Pages**.
3. Set source to **Deploy from a branch**.
4. Choose branch: `main`, folder: `/docs`.
5. Save.
6. Your website goes live in 1–5 minutes.

---

## 12) Keep design close to reference site, but your own brand

To make it “as it is like website” while still original:

- copy the **structure**, not exact text/assets
- use your own logo, colors, typography
- create your own sections and content
- keep legal-safe original media and copy

---

## 13) Common edits you asked for

- Change navbar menu: `_quarto.yml` → `website.navbar.left`
- Change social icons: `_quarto.yml` → `website.navbar.right`
- Change logo/favicon: replace image + update paths in `_quarto.yml`
- Change carousel images/text: `index.qmd`
- Change animation speed: `data-bs-interval` in `index.qmd`
- Change caption look: `styles.css`

---

## 14) Suggested next upgrades

- multilingual site (English + Hindi)
- blog/news updates section
- events calendar
- team member cards
- impact counters
- donation integration (Razorpay/Stripe links)
- SEO + Open Graph metadata

---

## 15) Quick checklist before launch

- [ ] Mobile responsive check
- [ ] Spelling and grammar reviewed
- [ ] Fast image sizes (compressed)
- [ ] Contact form or email visible
- [ ] Social links working
- [ ] HTTPS enabled (GitHub Pages does this)
- [ ] Favicon/logo visible on browser tab and navbar

---

If you want, next I can generate a **ready-to-use starter `_quarto.yml`, `index.qmd`, `styles.css`, `about.qmd`, `contact.qmd`** for your organization name and colors.
