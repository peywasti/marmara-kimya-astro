## Development

When starting the dev server, use background mode:

```
astro dev --background
```

Manage the background server with `astro dev stop`, `astro dev status`, and `astro dev logs`.

## Documentation

Full documentation: https://docs.astro.build

Consult these guides before working on related tasks:

- [Adding pages, dynamic routes, or middleware](https://docs.astro.build/en/guides/routing/)
- [Working with Astro components](https://docs.astro.build/en/basics/astro-components/)
- [Using React, Vue, Svelte, or other framework components](https://docs.astro.build/en/guides/framework-components/)
- [Adding or managing content](https://docs.astro.build/en/guides/content-collections/)
- [Adding styles or using Tailwind](https://docs.astro.build/en/guides/styling/)
- [Supporting multiple languages](https://docs.astro.build/en/guides/internationalization/)


# AGENT.md — Marmara Plastik Kimya Theme Recreation Guide

## Purpose

Recreate the visual language, layout system, responsive behavior, and component patterns of:

**https://marmara.keshawarzyar.ir/**

This document is based on the supplied HTML snapshots of the 13 pages:

- `/`
- `/urunler/`
- `/urunler/potasgen/`
- `/urunler/amino-mangaland/`
- `/urunler/calciboramin/`
- `/urunler/pf-nematod/`
- `/urunler/pf-trips/`
- `/urunler/supercopp/`
- `/urunler/hb-growth-n/`
- `/urunler/fulviazot/`
- `/urunler/borplus/`
- `/iletisim/`
- `/hakkimizda/`

The goal is to reproduce the **design**, not the WordPress/Astra/Elementor implementation itself. Do not copy WordPress-generated markup or Elementor IDs unless there is a strong technical reason.

---

## 1. Original Design Stack

The captured site is built with:

- WordPress
- Astra theme 4.13.9
- Astra child theme
- Elementor 4.2.2
- Elementor page-builder layouts
- Google Fonts:
  - `Karla` — body/UI text
  - `Rubik` — headings
- Font Awesome for icons
- WebP imagery
- A transparent-header Astra configuration
- Maximum content width around **1200px**

For a modern recreation, prefer a clean component-based implementation rather than reproducing Astra/Elementor.

Recommended choices:

- Semantic HTML
- CSS variables/design tokens
- CSS Grid/Flexbox
- Responsive CSS
- Reusable Header, Footer, Hero, ProductCard, ProductDetail, CTA and Contact components
- Optimized WebP/AVIF images
- No dependency on Elementor

---

# 2. Overall Visual Character

The site has a **clean agricultural / industrial / corporate** appearance.

Important characteristics:

- White/light backgrounds dominate content areas.
- Green is the primary brand color.
- Typography is modern and highly readable.
- Large whitespace is used between sections.
- Images are prominent but not excessively decorated.
- Corners are generally simple rather than heavily rounded.
- Buttons are compact, clean, and green.
- The visual style should feel professional and trustworthy rather than playful.
- Avoid gradients unless they are genuinely needed for image overlays.
- Avoid excessive shadows.
- Avoid glassmorphism.
- Avoid neon/saturated greens.
- Do not introduce a completely different visual language.

The design should communicate:

**agriculture + plant nutrition + biological/organic products + professional Turkish company**

---

# 3. Design Tokens

Use CSS variables similar to:

```css
:root {
  --color-primary: #1BAE70;
  --color-primary-dark: #06752E;
  --color-heading: #14261C;
  --color-text: #4E5652;
  --color-light: #F4F6F4;
  --color-white: #FFFFFF;
  --color-black: #000000;
  --color-muted: #4B4F58;
  --color-surface: #F6F7F8;

  --container-width: 1200px;

  --font-body: "Karla", sans-serif;
  --font-heading: "Rubik", sans-serif;
}
```

These values come directly from the captured Astra global palette.

Primary semantic mapping:

| Token | Value | Usage |
|---|---|---|
| Primary | `#1BAE70` | links, buttons, accents |
| Primary dark | `#06752E` | dark green accents/hover |
| Heading | `#14261C` | headings |
| Text | `#4E5652` | body copy |
| Light | `#F4F6F4` | light section backgrounds |
| Surface | `#F6F7F8` | subtle surfaces |
| White | `#FFFFFF` | header/content |
| Black | `#000000` | rare utility usage |

Do not arbitrarily add bright colors.

---

# 4. Typography

## Body

Use:

```css
font-family: "Karla", sans-serif;
font-weight: 400;
font-size: 20px;
line-height: 1.7;
```

The original site uses Karla for body/UI text.

For normal desktop body copy, 18–20px is appropriate. On mobile, reduce to approximately 16–18px while retaining comfortable line height.

## Headings

Use Rubik:

```css
font-family: "Rubik", sans-serif;
font-weight: 700;
color: #14261C;
```

Original desktop scale is approximately:

```text
H1: 87px
H2: 41px
H3: 28px
H4: 24px
H5: 18px
H6: 15px
```

The homepage hero uses a very large H1. For a modern responsive implementation:

```text
Desktop H1: clamp(48px, 6vw, 87px)
H2: clamp(30px, 3vw, 41px)
H3: 28px
H4: 24px
```

Do not force the desktop H1 size onto mobile.

Headings should not be uppercase by default.

---

# 5. Global Container

The original Astra configuration uses:

```text
1200px normal container width
```

Use:

```css
.container {
  width: min(1200px, calc(100% - 40px));
  margin-inline: auto;
}
```

For large desktop screens, keep content visually centered.

Recommended responsive padding:

```text
Desktop: 20–40px
Tablet: 24–32px
Mobile: 20px
```

The content should never touch the viewport edges.

---

# 6. Header

## Desktop

The original header contains:

- Logo on the left
- Navigation on the right
- Four primary links

Navigation:

```text
Anasayfa
Hakkımızda
Ürünler
İletisim
```

Use:

```text
Logo → left
Navigation → right
```

The logo is approximately 200px wide.

Original logo asset:

```text
marmara-kimya-1.png
```

The header uses Astra's transparent-header configuration, particularly on pages with a hero background.

### Header behavior

The visual header should:

- sit cleanly above/over the hero where appropriate
- have generous horizontal spacing
- avoid a heavy boxed appearance
- use a white/light logo/navigation treatment when placed over a dark hero
- switch to a normal light background where a transparent header would reduce readability

Navigation should have subtle hover/active green treatment.

Do not add unnecessary search, cart, account or mega-menu controls.

## Mobile

At approximately tablet/mobile breakpoint:

- Hide desktop navigation.
- Show a compact hamburger button.
- Keep logo visible.
- Menu opens vertically.
- Maintain large touch targets.
- Do not overcrowd the header.

A breakpoint around `922px` matches the original Astra behavior.

---

# 7. Homepage Structure

The homepage follows a simple sequence.

## Section A — Hero

Full-width visual hero.

Characteristics:

- Large background agricultural/industrial image
- Dark/soft overlay to make text readable
- Large white headline
- Generous vertical space
- Minimal content
- No crowded cards or controls

The captured headline is:

```text
PLASTİK KİMYA
sANAYE VE tICARET
```

The capitalization appears inconsistent in the source. When recreating the site, use the intended company typography rather than reproducing accidental capitalization errors.

The hero should feel spacious.

Recommended:

```css
.hero {
  min-height: 650px;
  display: grid;
  place-items: center;
  background-size: cover;
  background-position: center;
}
```

Use a subtle dark overlay rather than a strong black overlay.

---

# 8. Homepage — Agricultural Solutions Section

After the hero, the site presents two side-by-side content blocks.

### Block 1

Image:

```text
marmara-hero-6.webp
```

Heading:

```text
Tarımsal Çözümler
```

Text:

```text
Modern ve sürdürülebilir tarımda, zararlılara ve hastalıklara karşı yenilikçi yöntemler uygulanarak birim alanda en yüksek verim ile gelir elde edilmesi amaçlanmaktadır.
```

### Block 2

Image:

```text
marmara-hero-3.webp
```

Heading:

```text
Gübre Programları
```

Text:

```text
Gübreleme programları bitki yetiştirme için düzenli gübre uygulaması sağlar. Amaçları bitki büyümesini desteklemek, verimliliği artırmak ve besin eksikliklerini önlemektir.
```

Layout:

```text
Desktop:
[ image + text ] [ image + text ]

Mobile:
[ image ]
[ text ]

[ image ]
[ text ]
```

Use approximately 50/50 columns.

Images should preserve their aspect ratio.

---

# 9. Homepage — Product Showcase

The homepage includes a product showcase.

Products visible:

1. Amino Mangaland
2. Bor Plus
3. CalciBorAmin
4. Fulviazot
5. HB Growth N
6. PF Nematod
7. PF Trips
8. Potasgen

Use the supplied product images.

Recommended layout:

```text
Desktop:
4 columns × 2 rows

Tablet:
3 columns

Mobile:
2 columns or 1 column depending on card width
```

Each product card should be visually restrained:

- product image
- product name
- optional link
- white/light background
- small spacing
- no excessive shadow

Product packaging itself is the primary visual focus.

---

# 10. Product Listing Page

`/urunler/` contains:

- Featured products at the beginning
- Additional products underneath
- Product images
- Product titles
- Short descriptions for selected products
- "Daha fazla bilgi" links

Products:

```text
SuperCOPP
Potasgen
PF-Nematod
PF-Trips
HB Growth N
Fulviazot
CalciBorAmin
Bor Plus
Amino Mangaland
```

The listing should use a consistent reusable component:

```text
ProductCard
```

Suggested card structure:

```html
<article class="product-card">
  <a class="product-card__image">
    ...
  </a>

  <div class="product-card__body">
    <h3>Product Name</h3>
    <p>Short description...</p>
    <a> Daha fazla bilgi </a>
  </div>
</article>
```

Do not make every card visually different.

---

# 11. Product Detail Pages

Every product detail page follows a content-heavy editorial layout.

Examples:

```text
/urunler/potasgen/
/urunler/amino-mangaland/
/urunler/calciboramin/
/urunler/pf-nematod/
/urunler/pf-trips/
/urunler/supercopp/
/urunler/hb-growth-n/
/urunler/fulviazot/
/urunler/borplus/
```

The product pages contain:

- Product name
- Introductory description
- Long-form product explanation
- Benefits/functions
- Product features
- Guaranteed contents
- Usage/application information
- Crop-specific dosage tables

## Product hero

Recommended layout:

```text
Desktop:
┌─────────────────────────────┐
│ Product image │ Product info│
│               │ title       │
│               │ intro       │
└─────────────────────────────┘
```

On mobile:

```text
Product image
Product title
Description
```

Keep the product image large and clean.

---

# 12. Product Information Tables

Product pages contain agricultural dosage/specification tables.

These tables are important and must remain readable.

Typical columns include:

```text
Bitki türü
zamanı kullanmak
Kök
Yapraktan ilaçlama
```

or:

```text
isim
bilimsel ad
Yüzde
```

Use semantic `<table>` elements.

Desktop:

- normal horizontal table
- clear header
- adequate cell padding
- subtle borders

Mobile:

- allow horizontal scrolling rather than destroying the table structure

Example:

```css
.table-wrapper {
  overflow-x: auto;
}

table {
  width: 100%;
  border-collapse: collapse;
}
```

Never convert a complex agricultural dosage table into tiny unreadable text.

---

# 13. Product Content Typography

Long product pages should resemble a professional agricultural information document.

Use:

- H1 for product name
- H2 for major sections
- H3 for subsections
- paragraphs with comfortable spacing
- bullet lists for product functions/features
- tables for guaranteed contents and dosage

Do not use huge hero typography for every subsection.

Recommended content width:

```text
700–900px for long-form reading
```

Product images can occupy a wider column.

---

# 14. About Page

`/hakkimizda/`

The page is corporate and informational.

Main title:

```text
Hakkımızda
```

Company heading:

```text
MARMARA PLASTÍK KÍMYA SANAYİ VE TİCARET LİMİTED ŞİRKETİ
```

The page contains several paragraphs describing:

- plastic products
- irrigation systems
- industrial materials
- thermoplastic manufacturing
- chemical products
- agricultural inputs
- organic/inorganic materials
- fertilizers
- plant nutrition
- agricultural protection products

Layout should be:

```text
Page title
↓
Two-column intro/image where appropriate
↓
Long-form company information
↓
CTA
```

Keep the page professional and text-led.

---

# 15. Contact Page

`/iletisim/`

The contact page has two primary areas.

### Contact form

Fields:

```text
İsim *
E-posta *
Mesaj
Göndermek
```

### Contact information

```text
EMAIL
info@marmara-kimya.com

PHONE NUMBER
+90 (216) 442 10 38

ADDRESS
Istanbul / Kartal
Yalnız Selvi Mevkii
Sade Sit. No.5-11
```

There is also a social-media area.

Recommended desktop layout:

```text
[ Contact form ] [ Contact information ]
```

Mobile:

```text
Contact form
Contact information
Social links
```

Use a clean form with:

- white inputs
- subtle border
- clear labels
- green submit button
- accessible focus states

---

# 16. Global CTA

The homepage and internal pages end with a reusable CTA:

Heading:

```text
Bizimle konuş
```

Text:

```text
Sorularınız mı var? İşletmeniz, yeni ürünleriniz ve size nasıl yardımcı olabileceğimiz hakkında konuşmaya her zaman açığız.
```

Button:

```text
Temasta olmak
```

The CTA should be visually distinct from normal content.

Use a green/light-green or image-backed section depending on the page, while preserving the original restrained corporate style.

---

# 17. Footer

The original footer is simple.

It contains:

- horizontal navigation
- company logo
- copyright

Navigation repeats:

```text
Anasayfa
Hakkımızda
Ürünler
İletisim
```

Copyright:

```text
©2024 Marmara kimya. Tüm hakları saklıdır.
```

Recommended desktop:

```text
[ navigation ] [ logo ] [ copyright ]
```

Mobile:

```text
navigation
logo
copyright
```

Do not create a large multi-column marketing footer.

---

# 18. Responsive Rules

The design must be mobile-first.

## Desktop ≥ 1200px

- 1200px content container
- 2-column feature sections
- 3–4 column product grids
- transparent/full header
- large hero
- generous whitespace

## Tablet 768–1199px

- reduce typography
- reduce section spacing
- maintain 2-column content where practical
- product grid becomes 2–3 columns
- header remains compact

## Mobile < 768px

- single-column sections
- hamburger navigation
- product cards stacked or 2-column depending on screen width
- hero height reduced
- H1 reduced substantially
- tables horizontally scrollable
- CTA content centered
- no horizontal overflow

---

# 19. Spacing System

Use a consistent spacing scale instead of arbitrary values.

Suggested:

```text
8px
12px
16px
24px
32px
48px
64px
80px
96px
120px
```

Major sections should generally have:

```text
Desktop: 80–120px vertical padding
Tablet: 64–80px
Mobile: 48–64px
```

Avoid cramming sections together.

---

# 20. Image Treatment

The original site relies heavily on photography and product-packaging images.

Rules:

- Prefer WebP/AVIF.
- Preserve natural image proportions.
- Use `object-fit: cover` for hero/feature photography.
- Use `object-fit: contain` for product-packaging images.
- Do not artificially crop product packaging.
- Lazy-load below-the-fold images.
- Provide meaningful alt text.

Known visual assets include:

```text
marmara-kimya-1.png
marmara-hero-2.webp
marmara-hero-3.webp
marmara-hero-5.webp
marmara-hero-6.webp

product-aminomangaland.webp
product-borblus.webp
product-calciboramin.webp
product-fulviazot.webp
product-hbgrown.webp
product-pf-nematod.webp
product-pf-trips.webp
product-potasgen.webp
product-supercopp.webp
```

Use the highest-resolution versions available rather than the 300px WordPress thumbnails.

---

# 21. Buttons

Primary button style:

- green background
- white text
- compact
- medium weight
- clear hover state
- modest radius

Suggested:

```css
.button {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  padding: 12px 24px;
  background: #1BAE70;
  color: #fff;
  border-radius: 2px;
  font-family: "Karla", sans-serif;
  font-weight: 600;
  transition: background .2s ease, transform .2s ease;
}

.button:hover {
  background: #06752E;
}
```

Do not use pill-shaped buttons by default.

---

# 22. Accessibility

The recreated theme must improve on the original where appropriate.

Requirements:

- semantic headings
- semantic navigation
- keyboard-accessible menu
- visible focus states
- proper form labels
- descriptive image alt text
- sufficient color contrast
- buttons must be actual buttons/links
- tables must have table headers
- mobile menu must be keyboard accessible
- do not rely solely on color to communicate state

---

# 23. SEO / Content Structure

Preserve the site's content hierarchy.

Use:

```text
One H1 per page
H2 for major sections
H3/H4 for subsections
```

Product pages should retain all agricultural technical information.

Do not shorten or rewrite product descriptions during theme recreation.

URLs should remain:

```text
/
 /urunler/
 /urunler/{slug}/
 /hakkimizda/
 /iletisim/
```

Turkish characters should be preserved in visible content.

---

# 24. Component Architecture

Recommended components:

```text
Layout
├── Header
├── MobileNavigation
├── Main
└── Footer

Shared
├── Container
├── Section
├── Button
├── Image
└── CTA

Homepage
├── Hero
├── FeatureSplit
├── ProductGrid
├── ProductCard
└── CTA

Products
├── ProductListing
├── ProductCard
├── ProductHero
├── ProductContent
├── ProductFeatures
├── ProductSpecsTable
├── DosageTable
└── CTA

Contact
├── ContactForm
├── ContactDetails
└── SocialLinks
```

Keep components reusable.

---

# 25. Data Model

Product information should be data-driven rather than duplicated inside page components.

Example:

```ts
type Product = {
  slug: string
  name: string
  image: string
  intro: string
  sections: Section[]
  specifications?: Specification[]
  dosage?: DosageRow[]
}
```

Then render:

```text
/products/potasgen
/products/borplus
...
```

from the same ProductDetail component.

---

# 26. Important Fidelity Rules

When implementing the theme, prioritize these in order:

1. Overall page structure
2. Header/navigation
3. Typography
4. Green color palette
5. Hero proportions
6. Content width
7. Product image presentation
8. Section spacing
9. CTA/footer
10. Responsive behavior

Do not spend time reproducing Elementor's generated class names.

The result should **look like the Marmara site**, while the code should be substantially cleaner than the original WordPress/Elementor markup.

---

# 27. What NOT to Do

Do not:

- introduce a different color palette
- use purple/blue SaaS-style colors
- use huge rounded cards everywhere
- use glassmorphism
- add excessive animations
- add gradients to every section
- turn the site into a generic ecommerce storefront
- add a shopping cart unless explicitly requested
- add pricing cards
- add fake product ratings/reviews
- replace agricultural imagery with generic technology imagery
- remove technical product tables
- aggressively rewrite the Turkish content
- reproduce Elementor's generated DOM structure unnecessarily

The site is a **corporate agricultural products website**, not a SaaS dashboard or ecommerce marketplace.

---

# 28. Visual QA Checklist

Before considering implementation complete, compare every route against the captured reference.

Check:

- [ ] Header logo size and position
- [ ] Header navigation spacing
- [ ] Transparent header behavior
- [ ] Hero image crop
- [ ] Hero height
- [ ] H1 typography
- [ ] Green accent color
- [ ] Container width
- [ ] Section spacing
- [ ] Feature image proportions
- [ ] Product card alignment
- [ ] Product image sizing
- [ ] Product detail typography
- [ ] Tables
- [ ] Contact form
- [ ] Contact information
- [ ] CTA
- [ ] Footer
- [ ] Mobile menu
- [ ] Mobile typography
- [ ] No horizontal overflow

Test at minimum:

```text
1440 × 900
1280 × 800
1024 × 768
768 × 1024
390 × 844
```

---

## Final Implementation Principle

Build a **clean, responsive, component-based recreation of the Marmara Plastik Kimya visual system**.

The defining visual combination is:

> **Rubik headings + Karla body text + restrained green palette + large agricultural imagery + generous whitespace + simple corporate navigation + product-focused content + technical agricultural tables.**

Preserve the original information architecture and Turkish content, but implement the theme with modern semantic HTML/CSS/components rather than duplicating WordPress/Astra/Elementor internals.
