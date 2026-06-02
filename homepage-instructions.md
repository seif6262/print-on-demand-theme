# 🛠️ Claude Code — Homepage Section + Theme Styling Instructions
## Shopify Horizon Theme — Print on Demand Store

---

## 📋 Project Overview

Build a custom **Homepage Section** for a Shopify Horizon theme store for a **Print on Demand** brand targeting young adults (18–30). Then apply a **global color theme** across the entire theme, and finally **restyle the Product Page** to match the new design system.

---

## 🎨 Design System / Brand Tokens

Use these values consistently everywhere:

```css
/* === BRAND COLOR TOKENS === */
--color-brand-primary: #FFD600;       /* Electric Yellow — main accent */
--color-brand-primary-hover: #FFE033;
--color-brand-primary-text: #0A0A0A;  /* Text ON yellow backgrounds */

--color-bg-base: #0A0A0A;             /* Page background */
--color-bg-surface: #0D0D0D;          /* Sections alternate bg */
--color-bg-card: rgba(255,255,255,0.03);
--color-bg-card-hover: rgba(255,214,0,0.05);

--color-border-subtle: rgba(255,255,255,0.07);
--color-border-accent: rgba(255,214,0,0.3);

--color-text-primary: #FFFFFF;
--color-text-muted: rgba(255,255,255,0.5);
--color-text-faint: rgba(255,255,255,0.3);

/* === TYPOGRAPHY === */
--font-display: 'Syne', sans-serif;   /* Headings, logo, numbers */
--font-body: 'DM Sans', sans-serif;   /* Body text, buttons */

/* === SPACING === */
--section-padding-y: 80px;
--section-padding-x: 40px;
--card-radius: 16px;
--btn-radius: 100px;
```

**Google Fonts to load in `layout/theme.liquid` (inside `<head>`):**
```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Syne:wght@400;700;800&family=DM+Sans:wght@300;400;500&display=swap" rel="stylesheet">
```

---

## ✅ TASK 1 — Create Homepage Section (`homepage-hero.liquid`)

### File to create:
`sections/homepage-hero.liquid`

### What this section contains (top to bottom):

#### 1. Sticky Navigation Bar
- Logo placeholder: `[YOUR BRAND]` with `<span>` colored `#FFD600`
- Nav links: Products, Design Tool, Pricing, About
- Desktop: full nav links + "Start Designing" CTA button (yellow, pill shape)
- Mobile: hide nav links, show **hamburger button** (3 lines → X animation on open)
- Mobile menu: full-screen overlay, dark background `rgba(10,10,10,0.98)`, centered links in Syne 26px bold, closes on link click

#### 2. Hero Section
- Radial gradient background (yellow glow top center, very subtle)
- Animated badge: pulsing dot + text "Print on Demand — Ships in 48h"
- H1: `Your Design. <em>Printed</em> Your Way.` — `<em>` is colored `#FFD600`
- H1 font: Syne 800, clamp(42px, 7vw, 86px), letter-spacing -2px
- Subtext: muted, max-width 480px
- Two buttons: Primary (yellow fill) + Secondary (transparent, white border)

#### 3. Marquee Strip
- Yellow background `#FFD600`, dark text
- Scrolling items: T-Shirts ✦ Hoodies ✦ Mugs ✦ Phone Cases ✦ Tote Bags ✦ Stickers ✦ Posters ✦ Caps
- CSS animation `marquee`, 18s linear infinite, duplicate items for seamless loop

#### 4. How It Works (4 Steps)
- Section label: "HOW IT WORKS" uppercase yellow small text
- H2: "From idea to doorstep in 4 easy steps"
- Grid: 4 columns desktop, 2 columns tablet, 1 column mobile
- Each step: large faint number (01–04 in yellow 15% opacity), title, description
- Border between steps, hover: subtle yellow background tint

#### 5. Product Grid Section
- Section label + H2: "Print on anything."
- **Filter tabs** (All / Apparel / Accessories / Home & Living):
  - Pill buttons, inactive: dark bg + white border
  - Active/hover: yellow bg + dark text
  - JS filtering: show/hide cards by `data-cat` attribute
- **Product grid**: 4 columns desktop → 2 columns mobile → 1 column on very small screens
- Each product card:
  - Dark card bg with subtle border
  - Hover: lift (translateY -4px) + yellow border glow
  - Product emoji/image area (aspect-ratio 1:1)
  - Optional badge (Best Seller / New / Popular) — yellow pill, top-left absolute
  - Product name (Syne bold)
  - Price in yellow + color dots row
  - "Customize →" button (yellow tint bg, yellow text → yellow fill on hover)

**Default products to include:**

| Name | Emoji | Category | Price | Badge |
|------|-------|----------|-------|-------|
| Premium T-Shirt | 👕 | apparel | $14.99 | Best Seller |
| Unisex Hoodie | 🧥 | apparel | $29.99 | — |
| Snapback Cap | 🧢 | accessories | $18.99 | New |
| Phone Case | 📱 | accessories | $12.99 | — |
| Ceramic Mug | ☕ | home | $9.99 | — |
| Wall Poster | 🖼️ | home | $11.99 | Popular |
| Custom Socks | 🧦 | apparel | $8.99 | — |
| Tote Bag | 👜 | accessories | $13.99 | — |

#### 6. Why Us Section
- Two-column layout desktop (stats grid left, content right) → single column mobile
- Stats grid (2×2):
  - **50+** Products available — yellow accent box
  - **48h** Avg dispatch time
  - **10k+** Happy customers
  - **100%** Satisfaction guarantee
- Feature list (3 items): icon box + title + description
  - 🎨 No Minimums
  - ⚡ Lightning Fast
  - 🌍 Ships Worldwide

#### 7. CTA Banner
- Yellow background block, rounded corners, margin from edges
- H2 dark text: "Ready to create something awesome?"
- Subtext: "Join 10,000+ creators already printing with us."
- Dark button: bg `#0A0A0A`, text `#FFD600`
- Mobile: stack vertically, button full width

#### 8. Footer
- Simple: Logo left + copyright right
- Border top subtle
- Mobile: stack vertically

---

### Section Schema (add at bottom of .liquid file):

```liquid
{% schema %}
{
  "name": "Homepage Hero",
  "tag": "div",
  "class": "homepage-hero-section",
  "settings": [
    {
      "type": "text",
      "id": "brand_name",
      "label": "Brand Name",
      "default": "YOUR BRAND"
    },
    {
      "type": "text",
      "id": "hero_title_line1",
      "label": "Hero Title Line 1",
      "default": "Your Design."
    },
    {
      "type": "text",
      "id": "hero_highlight",
      "label": "Hero Highlighted Word",
      "default": "Printed"
    },
    {
      "type": "text",
      "id": "hero_title_line2",
      "label": "Hero Title Line 2",
      "default": "Your Way."
    },
    {
      "type": "textarea",
      "id": "hero_subtext",
      "label": "Hero Subtext",
      "default": "Upload your art, pick your product, and we handle the rest."
    },
    {
      "type": "text",
      "id": "cta_primary_text",
      "label": "Primary Button Text",
      "default": "Start Designing Free"
    },
    {
      "type": "url",
      "id": "cta_primary_url",
      "label": "Primary Button URL"
    },
    {
      "type": "text",
      "id": "cta_secondary_text",
      "label": "Secondary Button Text",
      "default": "Browse Products →"
    },
    {
      "type": "url",
      "id": "cta_secondary_url",
      "label": "Secondary Button URL"
    }
  ],
  "presets": [
    {
      "name": "Homepage Hero"
    }
  ]
}
{% endschema %}
```

---

## ✅ TASK 2 — Global Theme Color Override

### File to create or edit:
`assets/theme-overrides.css`

Then add this line inside `layout/theme.liquid` before `</head>`:
```html
{{ 'theme-overrides.css' | asset_url | stylesheet_tag }}
```

### CSS overrides to apply:

```css
/* ============================================
   GLOBAL THEME COLOR OVERRIDES
   Horizon Theme → Print on Demand Brand
   ============================================ */

:root {
  --color-background: #0A0A0A;
  --color-foreground: #FFFFFF;
  --color-primary: #FFD600;
  --color-primary-background: #FFD600;
  --color-button: #FFD600;
  --color-button-text: #0A0A0A;
  --color-border: rgba(255,255,255,0.08);
  --color-card-background: #111111;
}

/* Body & Page Background */
body {
  background-color: #0A0A0A !important;
  color: #FFFFFF !important;
  font-family: 'DM Sans', sans-serif !important;
}

/* All Headings */
h1, h2, h3, h4, h5, h6,
.h1, .h2, .h3, .h4 {
  font-family: 'Syne', sans-serif !important;
  color: #FFFFFF !important;
}

/* Primary Buttons */
.button,
.btn,
button[type="submit"],
.shopify-payment-button__button,
.product-form__submit {
  background-color: #FFD600 !important;
  color: #0A0A0A !important;
  border-color: #FFD600 !important;
  border-radius: 100px !important;
  font-family: 'DM Sans', sans-serif !important;
  font-weight: 700 !important;
  transition: background 0.2s, transform 0.15s !important;
}

.button:hover,
.btn:hover,
button[type="submit"]:hover,
.product-form__submit:hover {
  background-color: #FFE033 !important;
  transform: translateY(-2px) !important;
}

/* Links */
a { color: #FFFFFF; }
a:hover { color: #FFD600; }

/* Header / Navigation */
.header,
.site-header,
header[role="banner"] {
  background-color: rgba(10,10,10,0.95) !important;
  border-bottom: 1px solid rgba(255,255,255,0.07) !important;
}

.header__heading-link,
.header__menu-item,
.header a {
  color: rgba(255,255,255,0.7) !important;
  font-family: 'DM Sans', sans-serif !important;
}

.header__heading-link:hover,
.header__menu-item:hover,
.header a:hover {
  color: #FFD600 !important;
}

/* Cards */
.card,
.card-wrapper,
.product-card {
  background-color: #111111 !important;
  border: 1px solid rgba(255,255,255,0.07) !important;
  border-radius: 16px !important;
  transition: border-color 0.2s, transform 0.25s !important;
}

.card:hover,
.card-wrapper:hover,
.product-card:hover {
  border-color: rgba(255,214,0,0.3) !important;
  transform: translateY(-4px) !important;
}

/* Card Text */
.card__heading,
.card__heading a,
.card__information .price {
  color: #FFFFFF !important;
  font-family: 'Syne', sans-serif !important;
}

.price__current,
.price-item--regular {
  color: #FFD600 !important;
  font-weight: 700 !important;
}

/* Price compare */
.price__compare,
.price-item--compare {
  color: rgba(255,255,255,0.35) !important;
  text-decoration: line-through !important;
}

/* Badges / Sale Tags */
.badge,
.badge--sale,
.card__badge {
  background-color: #FFD600 !important;
  color: #0A0A0A !important;
  border-radius: 100px !important;
  font-weight: 700 !important;
  font-family: 'DM Sans', sans-serif !important;
}

/* Footer */
footer,
.footer {
  background-color: #0A0A0A !important;
  border-top: 1px solid rgba(255,255,255,0.07) !important;
  color: rgba(255,255,255,0.4) !important;
}

.footer a { color: rgba(255,255,255,0.6) !important; }
.footer a:hover { color: #FFD600 !important; }

/* Inputs & Forms */
input[type="text"],
input[type="email"],
input[type="password"],
input[type="number"],
textarea,
select {
  background-color: rgba(255,255,255,0.05) !important;
  border: 1px solid rgba(255,255,255,0.15) !important;
  color: #FFFFFF !important;
  border-radius: 12px !important;
  font-family: 'DM Sans', sans-serif !important;
}

input::placeholder,
textarea::placeholder {
  color: rgba(255,255,255,0.35) !important;
}

input:focus,
textarea:focus,
select:focus {
  border-color: rgba(255,214,0,0.5) !important;
  outline: none !important;
  box-shadow: 0 0 0 2px rgba(255,214,0,0.15) !important;
}

/* Announcement Bar */
.announcement-bar {
  background-color: #FFD600 !important;
  color: #0A0A0A !important;
  font-family: 'DM Sans', sans-serif !important;
  font-weight: 600 !important;
}

/* Collection Page */
.collection-hero__title,
.collection__title {
  font-family: 'Syne', sans-serif !important;
  color: #FFFFFF !important;
}

/* Pagination */
.pagination__item.active,
.pagination__item:hover {
  background-color: #FFD600 !important;
  color: #0A0A0A !important;
  border-color: #FFD600 !important;
}

/* Scroll bar */
::-webkit-scrollbar { width: 6px; }
::-webkit-scrollbar-track { background: #0A0A0A; }
::-webkit-scrollbar-thumb { background: rgba(255,214,0,0.3); border-radius: 3px; }
::-webkit-scrollbar-thumb:hover { background: #FFD600; }
```

---

## ✅ TASK 3 — Product Page Restyling

### File to edit:
`sections/main-product.liquid`

### Changes to apply:

#### Layout
- Two-column layout: **Images left (55%)** | **Info right (45%)**
- Dark page background matches global theme
- Add `padding: 60px 40px` to product section wrapper
- Mobile: stack to single column

#### Product Images
- Main image: rounded corners `border-radius: 16px`
- Image container background: `#111111`
- Thumbnail strip: horizontal scroll on mobile
- Active thumbnail: yellow border `2px solid #FFD600`

#### Product Info Panel
- Product title: Syne 800, clamp(28px, 4vw, 42px), white
- Price: Syne 700, 28px, `#FFD600`
- Compare-at price: strikethrough, `rgba(255,255,255,0.35)`
- Add a **savings badge** if compare price exists: yellow pill "Save X%"

#### Variant Selectors
- **Color swatches**: round dots (36×36px), border `2px solid transparent`
  - Selected: `border-color: #FFD600`
  - Hover: `border-color: rgba(255,214,0,0.5)`
- **Size buttons**: pill shape, dark bg, white text
  - Selected: yellow bg + dark text
  - Out of stock: faded + strikethrough text

#### Add to Cart Button
- Full width, height 56px
- Yellow bg `#FFD600`, dark text, Syne bold
- Hover: `#FFE033`, lift effect
- Border-radius: 100px

#### Product Description
- White text, DM Sans, 15px, line-height 1.7
- `color: rgba(255,255,255,0.65)` for readability
- Section separator: `border-top: 1px solid rgba(255,255,255,0.08)`

#### Trust Badges Strip (add below Add to Cart)
```html
<div class="trust-badges">
  <span>🚚 Fast Shipping</span>
  <span>🔒 Secure Payment</span>
  <span>↩️ Easy Returns</span>
</div>
```
Style: flex row, centered, small text, muted color, gaps

#### Sticky Add to Cart (Mobile)
- Fixed bottom bar on mobile: dark bg, price + "Add to Cart" button side by side
- Only show when main button is out of viewport
- JS: `IntersectionObserver` on main add-to-cart button

---

## 📁 Files Summary

| File | Action |
|------|--------|
| `sections/homepage-hero.liquid` | **CREATE** — full homepage section |
| `assets/theme-overrides.css` | **CREATE** — global color overrides |
| `layout/theme.liquid` | **EDIT** — add Google Fonts + CSS link in `<head>` |
| `sections/main-product.liquid` | **EDIT** — restyle product page |

---

## ⚠️ Important Notes for Claude Code

1. **Theme name is Horizon** — check existing class names before overriding (Horizon uses `.card-wrapper`, `.product-form__submit`, `.header__menu-item`)
2. **Always work on a duplicate theme** — never edit the live published theme directly
3. **Test on mobile** after every section (375px width minimum)
4. **Font loading** — confirm Google Fonts loads before using `font-family` in CSS
5. **Section schema** — make sure the section can be added via Shopify theme editor
6. **Color variables** — use CSS custom properties where possible for easy future changes
7. **JS** — keep all JavaScript at the bottom of `.liquid` files, inside `<script>` tags
8. **No external JS libraries** — use vanilla JS only

---

## 🎯 Final Result Should Look Like

- Dark `#0A0A0A` background throughout the entire store
- Electric Yellow `#FFD600` as the only accent color
- Syne font for all headings and display text
- DM Sans for body, buttons, labels
- Cards with dark background, subtle borders, yellow glow on hover
- Buttons: pill shape, yellow fill (primary) or yellow text on dark (secondary)
- Product page: clean two-column layout matching the homepage vibe
- Mobile: fully responsive, hamburger menu, stacked layouts, sticky add to cart

---

*Generated for: Print on Demand Shopify Store — Horizon Theme*
*Design vibe: Fun & Colorful × Dark Mode × Street Energy*
