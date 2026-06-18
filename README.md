# Lynnea Molone Art

Static portfolio and commission website for artist **Lynnea Molone** — murals, canvas paintings, staining, mailbox art, realism, and abstract. Built to showcase her work and accept custom project inquiries via email.

---

## Live Site

Deployed via GitHub Pages. Update `CNAME` with Lynnea's domain before publishing (currently contains a placeholder from a prior project).

---

## Tech Stack

- Plain HTML + CSS — no build step, no framework, no dependencies to maintain
- [Bootstrap 5.3.2](https://getbootstrap.com/) for grid and responsive layout
- [Font Awesome 6.4.2](https://fontawesome.com/) for icons
- Google Fonts: [Pacifico](https://fonts.google.com/specimen/Pacifico) (brand name), [Raleway](https://fonts.google.com/specimen/Raleway) (headings), [Nunito](https://fonts.google.com/specimen/Nunito) (body)
- Hosted on GitHub Pages

---

## File Structure

```
lynnea-molone-art/
├── index.html          # Entire site (single page)
├── custom.css          # All custom styles and theme variables
├── CNAME               # GitHub Pages custom domain — update before deploying
├── README.md           # This file
└── assets/
    ├── botanical-mural.jpg       # Botanical Brewing Co. — outdoor mural
    ├── veterans-mural.jpg        # Veterans Wall of Honor — indoor mural
    ├── woman-plants-mural.jpg    # Woman with plants — indoor mural
    ├── pelican-stained.jpg       # Pelican sunset — stained oval piece
    ├── hawkeyes-mailbox-1.jpg    # Iowa Hawkeyes custom mailbox (front)
    ├── hawkeyes-mailbox-2.jpg    # Iowa Hawkeyes custom mailbox (side)
    ├── canvas-collection.jpg     # Collection of original canvases
    ├── dragonfly.jpg             # "Dragonfly in Bloom" — for sale
    ├── figure-frame.jpg          # "Inner Dragon" — for sale
    ├── cosmic-canvas.jpg         # "Cosmic Portal" — for sale
    ├── gator-snake.jpg           # "The Encounter" — for sale
    └── blue-tree.jpg             # "Electric Willow" — for sale
```

---

## Page Sections

| Section | ID | Description |
| --- | --- | --- |
| Navbar | (sticky) | Glassmorphism nav with scroll color effect |
| Hero | `#home` | Full-screen animated gradient, Pacifico title |
| Specialty strip | (below hero) | Colorful pill badges for each service type |
| Portfolio gallery | `#portfolio` | 7-image grid; click any image for lightbox |
| Services | `#services` | 6 cards: Indoor Murals, Outdoor Murals, Staining, Mailbox Art, Canvas Paintings, Custom Commissions |
| Canvases for Sale | `#shop` | 5 canvas cards; each "Inquire" button opens a pre-filled email |
| Commission form | `#commission` | Project inquiry form fires `mailto:lynneamolone@gmail.com` |
| Footer | (bottom) | Brand, tagline, email, nav links |

---

## Color Palette

All theme colors are defined as CSS custom properties at the top of `custom.css`:

```css
:root {
  --lm-magenta: #E91E8C;   /* Primary — hero, buttons, nav accents */
  --lm-teal:    #00BCD4;   /* Secondary — brand tag, footer links */
  --lm-purple:  #7B1FA2;   /* Headings, gallery overlay gradient */
  --lm-yellow:  #FFD600;   /* Commission section accents, checklist icons */
  --lm-coral:   #FF5722;   /* Outdoor murals card, shop label */
  --lm-emerald: #00897B;   /* Available badge, custom commissions card */
  --lm-dark:    #1A1A2E;   /* Specialty strip, footer background */
  --lm-cream:   #FFFDF7;   /* Main page background, portfolio section */
  --lm-warm:    #FFF8EE;   /* For sale section background */
  --lm-lavender:#F3E8FF;   /* Services section background */
}
```

---

## Common Updates

### Adding or Updating Gallery Photos

Drop new images into `assets/` and add a new `.lm-gallery-item` block in the `#portfolio` section of `index.html`:

```html
<div class="lm-gallery-item" tabindex="0"
     data-src="./assets/your-photo.jpg"
     data-caption="Caption shown in lightbox">
  <img src="./assets/your-photo.jpg" alt="Description of the artwork" loading="lazy">
  <div class="lm-gallery-overlay"><span>Category Label</span></div>
</div>
```

The first item with class `lm-gi-tall` spans 2 rows; the fourth with `lm-gi-wide` spans 2 columns. All other items are uniform squares. You can remove those modifier classes to make all items uniform.

### Adding or Removing Canvases for Sale

Each canvas card in the `#shop` section follows this pattern:

```html
<div class="col-sm-6 col-lg-4">
  <div class="lm-canvas-card">
    <div class="lm-canvas-img">
      <img src="./assets/your-canvas.jpg" alt="Painting title and description" loading="lazy">
      <div class="lm-canvas-badge">Available</div>
    </div>
    <div class="lm-canvas-body">
      <h4 class="lm-canvas-title">Painting Title</h4>
      <p class="lm-canvas-info">Acrylic on canvas · Original · Any notes</p>
      <a href="mailto:lynneamolone@gmail.com?subject=Interested%20in%20%22Painting%20Title%22&body=Hi%20Lynnea..."
         class="btn lm-btn-primary w-100">Inquire to Purchase</a>
    </div>
  </div>
</div>
```

To mark a canvas as sold, replace the `lm-canvas-badge` text with `Sold` and change the background color:

```html
<div class="lm-canvas-badge" style="background:#94a3b8">Sold</div>
```

Or simply remove the entire `<div class="col-sm-6 col-lg-4">` block for that painting.

### Updating the Contact Email

All emails go to `lynneamolone@gmail.com`. To change it, find-and-replace `lynneamolone@gmail.com` across `index.html` — it appears in every "Inquire to Purchase" link and in the commission form's JavaScript at the bottom of the file.

### Updating the Commission Form

The form is at the bottom of `index.html` inside `<section id="commission">`. When submitted, it builds a `mailto:` link and opens the user's email client. No server or backend is needed. To add or change the project type options, edit the `<select id="cType">` dropdown.

---

## Deployment

1. Update `CNAME` with Lynnea's custom domain (e.g. `lynneamoloneart.com`)
2. Push to the `main` branch
3. In the GitHub repo settings → Pages → set source to `main` branch, root `/`
4. GitHub Pages will serve the site at the custom domain within a few minutes

No build step is needed — the site is plain HTML/CSS/JS and deploys as-is.

---

## Image Optimization (Before Launch)

The source images are original iPhone photos and may be several MB each. Before deploying to a public URL, optimize them to reduce load time:

```bash
# Using macOS built-in sips (lossless resize to max 1800px wide):
for f in assets/*.jpg; do sips -Z 1800 "$f"; done

# Or install ImageOptim (free Mac app) and drag the assets/ folder in
```

Target: under 300 KB per image for web use.
