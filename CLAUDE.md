# Form & Foliage Gardens — Project Brief for Claude Code

## What This Is

A marketing website for **Form & Foliage Gardens**, a small-batch specialty plant nursery in the Pacific Northwest. The site is in active iteration with a creative director. A working HTML prototype exists. Your job is to refine, componentize, and deploy it.

---

## Business Context

**What the company sells:**
- Seed-grown Japanese maples (*Acer palmatum*) — the core product and primary differentiator
- Hand-propagated specialty ornamental plants (rhododendrons, broadleaf ornamentals, bonsai starter material, etc.)
- Located in and selling throughout the **Puget Sound / Pacific Northwest region**

**How they sell:**
- Farmers markets and specialty plant sales (Bellevue, Issaquah, and various PNW events)
- No online store — intentionally. They want **contact/interest capture only**, not e-commerce
- No stock listings on the site — every plant is unique; the model is match-making, not shopping

**The differentiator (important for all copy):**
Most nurseries graft Japanese maples, producing genetic clones. Form & Foliage grows **from seed** — which means every plant is genetically unique. This is the "piece of future art" concept: a tree no one else has, that will spend a lifetime becoming something singular. This is not a marketing gimmick — it's botany, and it's the soul of the brand.

---

## Brand Positioning & Tone

**Positioning:** Semi-premium, artisan, future-heirloom. Think small-batch winery or independent ceramics studio — not garden center, not big-box nursery.

**The core idea:** *"A piece of future art."* The customer is not buying a plant; they are starting a relationship with a living thing that will outlive most furniture they'll ever own.

**Copy direction — always customer-benefit first:**
- Lead with what the customer gets, not what the nursery does
- "No nursery, no neighbor, no one has this exact tree" > "we grow from seed"
- "Already at home in the PNW" > "acclimated to local conditions"
- "A tree that rewards patience" > "long-lived specimen plants"
- Avoid nursery catalog language. Lean literary, unhurried, confident.

**Tone:** Warm but not cozy. Confident but not precious. Like a knowledgeable friend who also happens to be an artist.

---

## Design System

### Fonts
- **Display / Serif:** `Cormorant Garamond` (Google Fonts) — used for headlines, blockquotes, large numerals, plant names. Weight 300 (light) almost exclusively; italic for accent/emphasis.
- **Sans-serif / UI:** `Futura PT` — used for nav, eyebrows, labels, buttons, body text. **Load via Adobe Fonts or your preferred font service.** CSS variable is `--sans` — one-line swap once the font is loaded. Fallback stack: `'Futura', 'Century Gothic', 'Trebuchet MS', system-ui, sans-serif`.

> ⚠️ Futura PT is **not** on Google Fonts. It requires an Adobe Fonts embed or self-hosting. The current prototype uses the fallback stack visually — swap in the real embed when deploying.

### Color Palette (CSS variables)
```css
--ink:       #1b231c;   /* Near-black with green undertone — primary text, dark panels */
--cream:     #f4efe6;   /* Warm off-white — primary background */
--parchment: #ece6d8;   /* Slightly warmer — secondary backgrounds, cards */
--sage:      #556e57;   /* Muted green — eyebrows, labels, secondary text */
--maple:     #8c3328;   /* Deep terracotta red — accents, italic highlights, CTA button */
--gold:      #b08a4e;   /* Warm antique gold — decorative rules, hero eyebrow, links on dark */
--mist:      #c4d0c4;   /* Soft grey-green — body text on dark backgrounds */
```

### Typography Scale
- Hero title: `clamp(4rem, 7vw, 7rem)`, Cormorant, weight 300, italic for emphasis
- Section headings: `clamp(2rem–2.4rem, 3.5–4.5vw, 3.1–3.8rem)`, Cormorant, weight 300
- Body: `0.93–1rem`, Futura PT, weight 300, line-height 1.75–1.9
- Eyebrows/labels: `0.58–0.62rem`, Futura PT, weight 500, letter-spacing `0.2–0.22em`, `text-transform: uppercase`
- Buttons: `0.62rem`, Futura PT, weight 500, letter-spacing `0.2em`, uppercase

### Spacing & Layout
- Max content width: `1200px`
- Container padding: `3.5rem` horizontal (desktop), `1.5rem` (mobile)
- Sections: `7rem` vertical padding (desktop), compress on mobile
- Grid: 12-column for plant cards; 2-column for most content sections

### Aesthetic Rules
- **No rounded corners** — all elements are sharp-edged (`border-radius: 0`)
- **Generous negative space** — don't fill every pixel
- **Grain texture overlay** on body via SVG data URI (subtle, ~35% opacity)
- Borders use `rgba` with low opacity rather than solid colors — feels more refined
- Hover states: subtle `translateY(-4 to -5px)` on cards; `translateX` on arrow glyphs; background/color swap on buttons
- Scroll reveal: `IntersectionObserver` with `opacity` + `translateY` fade-up, staggered delays via `.reveal-delay-N` classes

---

## Current Site Structure

### Pages / Sections (single-page)
All in `index.html`. Sections with `id` anchors:

| Section | ID | Description |
|---|---|---|
| Navigation | `#nav` | Fixed, transparent → frosted glass on scroll |
| Hero | `#hero` | Full-height, dark left panel + photo right, animated title |
| Intro | `#intro` | 2-col grid: label left, copy + 2-col body text right |
| Differentiators | `#differentiators` | Dark background, 3-card grid |
| Plants | `#plants` | Photo gallery / portfolio — NO prices, NO stock |
| Story | `#story` | Dark background, photo left + copy right, 2-col |
| Find Us | `#find-us` | Market schedule list |
| Interest List | `#interest` | Lead capture form — THE primary conversion goal |
| Footer | footer | Brand, nav links, copyright |

### Image Files (keep in same directory as index.html)
```
img-fall-tree.jpg        # Specialty broadleaf in autumn color w/ rain — hero BG + story panel
img-macro-leaf.jpg       # Extreme macro of crimson maple leaf — hero corner inset + plant card
img-variegated-maple.jpg # Variegated pink/cream/green maple — hero plant card (largest)
img-maple-pot-1.jpg      # Salmon-pink young maple in nursery pot
img-maple-pot-2.jpg      # Cream/green maple in nursery pot
img-rhododendron.jpg     # Pink rhododendron — specialty plants card
```

---

## Hosting & Deployment

### Chosen Stack
- **Host:** GitHub Pages (free, serves static sites directly from a repo)
- **Domain registrar:** TBD — can configure a custom domain in GitHub Pages settings
- **Deployment method:** Push to `main` → GitHub Pages auto-deploys

### GitHub Pages Deployment Setup
1. Push the repo to GitHub (public repo, or private with GitHub Pro/Team)
2. Go to repo → Settings → Pages
3. Under "Source", select **Deploy from a branch**
4. Select `main` branch, `/ (root)` folder, click Save
5. Site will be live at `https://<username>.github.io/<repo-name>/`
6. (Optional) Add a custom domain under Settings → Pages → Custom domain

> For a custom domain: add a CNAME file to the repo root containing the domain, and configure DNS records (A records or CNAME) per GitHub's docs.

### Repository Structure (suggested)
```
/
├── index.html
├── img-fall-tree.jpg
├── img-macro-leaf.jpg
├── img-variegated-maple.jpg
├── img-maple-pot-1.jpg
├── img-maple-pot-2.jpg
├── img-rhododendron.jpg
├── CLAUDE.md
└── README.md
```

This is a **static site** — no build step needed. HTML/CSS/JS only. No framework, no bundler.

---

## Refinement Priorities (What Claude Code Should Work On)

### High Priority
1. **Futura PT integration** — add Adobe Fonts embed snippet (owner will provide the kit URL) and wire to `--sans` variable
2. **Form backend** — wire the interest list form to [Formspree](https://formspree.io) (free tier, no backend needed) or similar. Current form has a client-side success state only.
3. **Meta / SEO** — add `<meta description>`, Open Graph tags, `<title>` refinement, basic schema markup for local business
4. **Favicon** — create a simple botanical SVG favicon (maple leaf silhouette works)
5. **Mobile polish** — verify all breakpoints, especially hero on iOS Safari, and the market rows on small screens

### Medium Priority
6. **Instagram embed or link** — referenced in copy but not yet implemented. Either a simple `@formandfoliage` link with icon, or an embedded feed if the owner wants it
7. **Google Analytics or Plausible** — lightweight analytics, privacy-respecting (Plausible preferred — no cookie banner needed)
8. **Performance** — compress/optimize the 6 JPEG images (aim for <200KB each), add `loading="lazy"` to below-fold images, add `width`/`height` attributes
9. **Accessibility** — audit for color contrast (especially mist text on dark backgrounds), ensure all form fields have proper labels, add `aria-label` to icon-only elements

### Lower Priority / Future
10. **Care guide page** — a simple `/care` subpage with Japanese maple care basics for the PNW. Good for SEO, builds authority.
11. **Email newsletter integration** — Mailchimp or ConvertKit embed as alternative/supplement to the interest form
12. **Print stylesheet** — for any in-person market materials that might reference the site

---

## What NOT to Change Without Checking

- **No e-commerce, no stock listings, no prices** — intentional and important to the brand
- **No online shop** — the whole model is interest capture → personal follow-up
- **Keep the plant card layout as a portfolio/gallery**, not a product grid
- **Don't genericize the copy** — it's intentionally literary and restrained. Avoid nursery catalog language.
- **Don't add social proof widgets or review stars** — doesn't match the premium positioning
- **Keep forms simple** — no multi-step flows, no pop-ups, no exit-intent nonsense

---

## Key Copy Anchors (Don't Change These Lines)

These have been specifically crafted and approved:

- Hero headline: **"A piece of future art."**
- Intro headline: **"No nursery, no neighbor, no one has this exact tree."**
- Story blockquote: **"You're not decorating a garden. You're starting a relationship with a living thing."**
- Interest form heading: **"Tell us what you're looking for"**
- Interest form subhead: **"Let's find your plant"**

---

## Market / Find Us Data (Update as Needed)

Current placeholder markets — owner should confirm/update:
- Bellevue Farmers Market — Saturdays, May–Oct, Downtown Bellevue WA
- Issaquah Farmers Market — Saturdays, May–Oct, Pickering Barn, Issaquah WA
- PNW Plant Sales & Specialty Events — various, check Instagram

Instagram handle: `@formandfoliage` (confirm with owner before deploying)

---

## Interest Form Fields

The form collects:
- First Name (required)
- Last Name
- Email (required)
- City / Neighborhood
- Checkboxes: Variegated maples / Red & lobed forms / Laceleaf & weeping / Dwarf & compact / Specialty ornamentals
- Free-text notes ("Tell us more about what you're looking for")

Wire to Formspree: replace `<form id="interest-form">` with `<form action="https://formspree.io/f/YOUR_FORM_ID" method="POST">` and remove the client-side submit handler (or keep it as a UI enhancement after real submission).

---

## Notes for Creative Director Handoff

- All design decisions are in the CSS custom properties at the top of `index.html` — easy to swap colors, fonts, spacing globally
- The `--maple` red and `--gold` are the two accent colors — adjust saturation/hue here if needed
- Font weight is almost entirely `300` (light) for Cormorant — this is intentional and important to the refined feel. Don't bump to 400/500 unless there's a specific reason.
- The grain texture is a CSS-only SVG data URI — no external dependency
- Scroll reveal uses native `IntersectionObserver` — no library needed, works in all modern browsers
- The site is fully self-contained in one HTML file + 6 JPEGs — no npm, no build step, no dependencies beyond Google Fonts
