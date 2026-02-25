# A–Z Guide: Build a Professional NGO Website (Like Vaagdhara Style) with RStudio + Quarto

This guide gives a complete, practical process to create your NGO website with:
- custom navbar
- logo + favicon
- homepage hero carousel (auto slide)
- text overlay on images
- modern sections (mission, impact, programs, gallery, contact)
- mobile-friendly design

> Goal: follow the **structure quality** of a site like `vaagdhara.org`, but use your **own branding, text, photos, and identity**.

---

## A. Plan before coding (important)

Write these first in a notes file:

1. NGO Name
2. Tagline (1 line)
3. Mission (2–3 lines)
4. 4–6 main menu items
5. 3 homepage highlight messages
6. 8–15 real project photos
7. Contact info + Google Maps link + social links

If you prepare this first, your website will look much better and more professional.

---

## B. Install required software

Install:
- **R**
- **RStudio**
- **Quarto**

Check installation:

```bash
quarto check
```

---

## C. Create a Quarto website project in RStudio

1. Open RStudio.
2. `File -> New Project -> New Directory -> Quarto Website`.
3. Project name: `my-ngo-website`.
4. Click Create.

You will get:
- `_quarto.yml` (global website settings)
- `index.qmd` (home page)
- sample pages

---

## D. Use this recommended folder structure

```text
my-ngo-website/
├── _quarto.yml
├── index.qmd
├── about.qmd
├── programs.qmd
├── impact.qmd
├── gallery.qmd
├── contact.qmd
├── donate.qmd
├── styles.css
├── images/
│   ├── logo.png
│   ├── hero1.jpg
│   ├── hero2.jpg
│   ├── hero3.jpg
│   └── (other images)
└── docs/        # rendered output for GitHub Pages
```

---

## E. Configure `_quarto.yml` (navbar, logo, icons)

Replace your `_quarto.yml` with this starter:

```yaml
project:
  type: website
  output-dir: docs

website:
  title: "Your NGO Name"
  favicon: images/logo.png
  navbar:
    logo: images/logo.png
    left:
      - href: index.qmd
        text: Home
      - href: about.qmd
        text: About Us
      - href: programs.qmd
        text: Programs
      - href: impact.qmd
        text: Impact
      - href: gallery.qmd
        text: Gallery
      - href: contact.qmd
        text: Contact
      - href: donate.qmd
        text: Donate
    right:
      - icon: facebook
        href: https://facebook.com/yourngo
      - icon: instagram
        href: https://instagram.com/yourngo
      - icon: youtube
        href: https://youtube.com/@yourngo

format:
  html:
    theme: flatly
    css: styles.css
    toc: false
    smooth-scroll: true
```

---

## F. Build a strong homepage (`index.qmd`)

Paste this in `index.qmd`:

```markdown
---
title: "Home"
---

<div id="homeCarousel" class="carousel slide" data-bs-ride="carousel" data-bs-interval="3500" data-bs-pause="false">
  <div class="carousel-indicators">
    <button type="button" data-bs-target="#homeCarousel" data-bs-slide-to="0" class="active" aria-current="true" aria-label="Slide 1"></button>
    <button type="button" data-bs-target="#homeCarousel" data-bs-slide-to="1" aria-label="Slide 2"></button>
    <button type="button" data-bs-target="#homeCarousel" data-bs-slide-to="2" aria-label="Slide 3"></button>
  </div>

  <div class="carousel-inner hero-shadow rounded-4">
    <div class="carousel-item active">
      <img src="images/hero1.jpg" class="d-block w-100 carousel-img" alt="Community program image 1">
      <div class="carousel-caption custom-caption">
        <h2>Empowering Rural Communities</h2>
        <p>Together we create dignity, opportunity, and local leadership.</p>
      </div>
    </div>

    <div class="carousel-item">
      <img src="images/hero2.jpg" class="d-block w-100 carousel-img" alt="Community program image 2">
      <div class="carousel-caption custom-caption">
        <h2>Education, Health, and Livelihood</h2>
        <p>Integrated programs for lasting social transformation.</p>
      </div>
    </div>

    <div class="carousel-item">
      <img src="images/hero3.jpg" class="d-block w-100 carousel-img" alt="Community program image 3">
      <div class="carousel-caption custom-caption">
        <h2>Your Support Changes Lives</h2>
        <p>Partner with us to scale impact for families and youth.</p>
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

## Our Mission

We work with communities to advance rights, livelihoods, and inclusive development through participatory action.

## What We Do

- Education and child development
- Women-led livelihood collectives
- Climate and natural resource stewardship
- Youth leadership and skills

## Latest Impact Snapshot

- 120+ villages reached
- 18,000+ people engaged
- 320+ women linked to livelihoods

[Support Our Work](donate.qmd){.btn .btn-primary .btn-lg}
```

### Why this is better
- Auto-runs slideshow (`data-bs-ride`) and keeps moving (`data-bs-pause="false"`).
- Overlay text is readable on all images.
- CTA button adds action, not just information.

---

## G. Add professional styling (`styles.css`)

Paste this in `styles.css`:

```css
/* ---------- Brand ---------- */
.navbar-brand img {
  max-height: 44px;
}

.navbar {
  box-shadow: 0 2px 14px rgba(0, 0, 0, 0.08);
}

/* ---------- Hero carousel ---------- */
.carousel-img {
  height: 72vh;
  object-fit: cover;
}

.hero-shadow {
  box-shadow: 0 10px 26px rgba(0, 0, 0, 0.16);
}

.custom-caption {
  background: linear-gradient(135deg, rgba(0,0,0,.62), rgba(0,0,0,.28));
  border-radius: 14px;
  padding: 1rem 1.2rem;
  max-width: 700px;
  margin-inline: auto;
}

.custom-caption h2,
.custom-caption p {
  color: #fff;
}

/* ---------- Section spacing ---------- */
main.content {
  padding-bottom: 2rem;
}

h2 {
  margin-top: 2rem;
}

/* ---------- Mobile ---------- */
@media (max-width: 768px) {
  .carousel-img {
    height: 48vh;
  }

  .custom-caption h2 {
    font-size: 1.1rem;
  }

  .custom-caption p {
    font-size: 0.88rem;
  }
}
```

---

## H. Create remaining pages quickly

### `about.qmd`
- who you are
- history
- vision + mission
- leadership/team photo

### `programs.qmd`
- each program with heading + image + short text
- add 1 success story under each

### `impact.qmd`
- key numbers
- before/after outcomes
- annual report PDF link

### `gallery.qmd`
- photos grouped by program/event

### `contact.qmd`
Include:
- address
- email
- phone
- map link
- social links

### `donate.qmd`
Include:
- donation options (UPI, bank transfer, platform)
- transparency statement
- thank-you message

---

## I. Add image quality best practices

To make website look premium:

1. Use landscape photos for hero (`1920x900` preferred).
2. Compress images (TinyPNG/Squoosh).
3. Keep each image usually under 300–500 KB.
4. Use meaningful alt text for accessibility.

---

## J. Add trust-building sections (highly recommended)

Add on homepage or About page:
- Partners/Supporters logos
- Testimonials
- Annual report links
- Registration / legal details
- “Where funds go” chart image

This increases credibility for donors and partners.

---

## K. Preview locally while editing

```bash
quarto preview
```

Use this mode to continuously review design and content.

---

## L. Build production output

```bash
quarto render
```

This generates final website in `docs/`.

---

## M. Publish on GitHub Pages

1. Push project to GitHub.
2. Go to `Settings -> Pages`.
3. Source: `Deploy from a branch`.
4. Branch: `main`, Folder: `/docs`.
5. Save.
6. Wait 1–5 minutes.

Your website will be live.

---

## N. SEO and sharing setup (important)

In `_quarto.yml`, add basic metadata under `website:`:

```yaml
website:
  title: "Your NGO Name"
  site-url: "https://yourdomain.org"
  description: "Community-led development NGO focused on education, livelihoods, and rights."
```

Also create custom social share image (1200x630).

---

## O. Suggested color and font strategy

- Choose 2 brand colors + 1 accent color.
- Use one clean font style (Quarto theme default is okay to start).
- Keep high contrast for readability.
- Avoid too many animations.

---

## P. 7-day practical launch plan

### Day 1
Set structure + navbar + pages.

### Day 2
Build homepage carousel and mission/impact sections.

### Day 3
Complete About + Programs pages.

### Day 4
Complete Impact + Gallery + Contact + Donate pages.

### Day 5
Polish design, spacing, and mobile responsiveness.

### Day 6
Proofread content + compress images + validate links.

### Day 7
Deploy to GitHub Pages + final QA.

---

## Q. Final pre-launch checklist

- [ ] Logo and favicon visible
- [ ] Navbar links work
- [ ] Carousel auto-slides smoothly
- [ ] Text overlay readable on all slides
- [ ] Mobile view tested
- [ ] Contact details correct
- [ ] Social links correct
- [ ] Donate page functional
- [ ] No spelling mistakes
- [ ] Site deployed and opens on HTTPS

---

## R. Next step (if you want)

I can generate a **fully customized starter kit** for your NGO with:
- your NGO name
- your navbar names
- your color palette
- your logo filename
- 3 real hero captions for your mission

Then you can directly paste and launch.
