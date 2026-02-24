# Style Presets Reference — Domino Brand

Curated visual styles for Domino Slides, strictly following the **Domino Brand Guidelines (2025 Update)**. Every preset uses approved brand colors, typography, and design patterns. **Abstract shapes only — no illustrations. Line art motifs encouraged.**

---

## Brand Identity Quick Reference

| Element | Value |
|---------|-------|
| **Brand** | Domino Data Lab |
| **Primary Font** | New Grotesk (headlines, subheads, body) |
| **Mono Font** | New Grotesk Mono (CTAs, eyebrow text, data) |
| **Font Source** | Archive Foundry (licensed) |
| **Core Colors** | Black #000000, White #FFFFFF |
| **Brand Colors** | Domino Orange #FF6543, Light Purple #D4C9FC, Light Blue #A5C5F6 |
| **Logo** | White on dark backgrounds, black on light backgrounds |

---

## CRITICAL: Viewport Fitting (Non-Negotiable)

**Every slide MUST fit exactly in the viewport. No scrolling within slides, ever.**

### Content Density Limits Per Slide

| Slide Type | Maximum Content |
|------------|-----------------|
| Title slide | 1 heading + 1 subtitle |
| Content slide | 1 heading + 4-6 bullets (max 2 lines each) |
| Feature grid | 1 heading + 6 cards (2x3 or 3x2) |
| Code slide | 1 heading + 8-10 lines of code |
| Quote slide | 1 quote (max 3 lines) + attribution |

**Too much content? -> Split into multiple slides. Never scroll.**

### Required Base CSS (Include in ALL Presentations)

```css
/* ===========================================
   VIEWPORT FITTING: MANDATORY
   Copy this entire block into every presentation
   =========================================== */

/* 1. Lock document to viewport */
html, body {
    height: 100%;
    overflow-x: hidden;
}

html {
    scroll-snap-type: y mandatory;
    scroll-behavior: smooth;
}

/* 2. Each slide = exact viewport height */
.slide {
    width: 100vw;
    height: 100vh;
    height: 100dvh; /* Dynamic viewport for mobile */
    overflow: hidden; /* CRITICAL: No overflow ever */
    scroll-snap-align: start;
    display: flex;
    flex-direction: column;
    position: relative;
}

/* 3. Content wrapper */
.slide-content {
    flex: 1;
    display: flex;
    flex-direction: column;
    justify-content: center;
    max-height: 100%;
    overflow: hidden;
    padding: var(--slide-padding);
}

/* 4. ALL sizes use clamp() - scales with viewport */
:root {
    /* Typography */
    --title-size: clamp(1.5rem, 5vw, 4rem);
    --h2-size: clamp(1.25rem, 3.5vw, 2.5rem);
    --body-size: clamp(0.75rem, 1.5vw, 1.125rem);
    --small-size: clamp(0.65rem, 1vw, 0.875rem);

    /* Spacing */
    --slide-padding: clamp(1rem, 4vw, 4rem);
    --content-gap: clamp(0.5rem, 2vw, 2rem);
}

/* 5. Cards/containers use viewport-relative max sizes */
.card, .container {
    max-width: min(90vw, 1000px);
    max-height: min(80vh, 700px);
}

/* 6. Images constrained */
img {
    max-width: 100%;
    max-height: min(50vh, 400px);
    object-fit: contain;
}

/* 7. Grids adapt to space */
.grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(min(100%, 220px), 1fr));
    gap: clamp(0.5rem, 1.5vw, 1rem);
}

/* ===========================================
   RESPONSIVE BREAKPOINTS - Height-based
   =========================================== */

/* Short screens (< 700px height) */
@media (max-height: 700px) {
    :root {
        --slide-padding: clamp(0.75rem, 3vw, 2rem);
        --content-gap: clamp(0.4rem, 1.5vw, 1rem);
        --title-size: clamp(1.25rem, 4.5vw, 2.5rem);
    }
}

/* Very short (< 600px height) */
@media (max-height: 600px) {
    :root {
        --slide-padding: clamp(0.5rem, 2.5vw, 1.5rem);
        --title-size: clamp(1.1rem, 4vw, 2rem);
        --body-size: clamp(0.7rem, 1.2vw, 0.95rem);
    }

    .nav-dots, .keyboard-hint, .decorative {
        display: none;
    }
}

/* Extremely short - landscape phones (< 500px) */
@media (max-height: 500px) {
    :root {
        --slide-padding: clamp(0.4rem, 2vw, 1rem);
        --title-size: clamp(1rem, 3.5vw, 1.5rem);
        --body-size: clamp(0.65rem, 1vw, 0.85rem);
    }
}

/* Narrow screens */
@media (max-width: 600px) {
    .grid {
        grid-template-columns: 1fr;
    }
}

/* Reduced motion */
@media (prefers-reduced-motion: reduce) {
    *, *::before, *::after {
        animation-duration: 0.01ms !important;
        transition-duration: 0.2s !important;
    }
}
```

### Viewport Fitting Checklist

Before finalizing any presentation, verify:

- [ ] Every `.slide` has `height: 100vh; height: 100dvh; overflow: hidden;`
- [ ] All font sizes use `clamp(min, preferred, max)`
- [ ] All spacing uses `clamp()` or viewport units
- [ ] Breakpoints exist for heights: 700px, 600px, 500px
- [ ] Content respects density limits (max 6 bullets, max 6 cards)
- [ ] No fixed pixel heights on content elements
- [ ] Images have `max-height` constraints

---

## Typography System

### Primary: New Grotesk

New Grotesk is the brand typeface. It has a balance of character and utility, suited for everything from short headlines to long-form content.

**Usage:**
- All headlines and subheads
- All body copy
- All general-purpose text

**Web fallback stack:** `'New Grotesk', 'Inter', 'Helvetica Neue', Arial, sans-serif`

### Secondary: New Grotesk Mono

**Usage:**
- All CTA button labels (always uppercase)
- Eyebrow text (category labels above headlines)
- Data copy, code, and technical labels
- Navigation items

**Web fallback stack:** `'New Grotesk Mono', 'JetBrains Mono', 'SF Mono', 'Consolas', monospace`

### Typography Hierarchy

```css
/* Headlines — New Grotesk, bold weight */
h1 { font-family: var(--font-display); font-weight: 700; font-size: var(--title-size); }
h2 { font-family: var(--font-display); font-weight: 700; font-size: var(--h2-size); }
h3 { font-family: var(--font-display); font-weight: 600; font-size: clamp(1rem, 2.5vw, 1.75rem); }

/* Body — New Grotesk, regular weight */
p, li { font-family: var(--font-body); font-weight: 400; font-size: var(--body-size); }

/* Eyebrow — New Grotesk Mono, uppercase */
.eyebrow {
    font-family: var(--font-mono);
    font-weight: 400;
    font-size: var(--small-size);
    text-transform: uppercase;
    letter-spacing: 0.08em;
    color: var(--domino-orange);
}

/* CTA labels — New Grotesk Mono, uppercase */
.btn, button, .cta {
    font-family: var(--font-mono);
    font-weight: 500;
    text-transform: uppercase;
    letter-spacing: 0.06em;
}
```

---

## Color System

### Core Palette

The foundation. Used for accessibility, simplicity, and consistency.

```css
:root {
    --black: #000000;           /* RGB 30/30/30  — primary text on light, solid backgrounds */
    --white: #FFFFFF;           /* RGB 255/255/255 — primary text on dark, backgrounds */
}
```

### Brand Palette

These are **synonymous with Domino**. Used sparingly for moments of support, assurance, delight, CTAs, and brand interaction.

```css
:root {
    --domino-orange: #FF6543;   /* RGB 255/101/67  — CTAs, buttons, links, eyebrow text */
    --light-purple: #D4C9FC;    /* RGB 212/201/252 — subtle contrast, graphical elements, backgrounds */
    --light-blue: #A5C5F6;      /* RGB 165/197/246 — subtle contrast, graphical elements, backgrounds */
}
```

**Orange usage:** Strategically applied to highlight critical calls-to-action — buttons, links, eyebrow copy. Draws user attention effectively.

**Light Purple & Light Blue:** Add subtle contrast. Often appear in graphical elements, icons, or as slide backgrounds.

### Neutral Palette

For depth and hierarchy, distinguishing sections while maintaining cohesion.

```css
:root {
    --dark-grey: #3C3A42;       /* RGB 60/58/66   — secondary text, dark accents */
    --medium-grey: #777384;     /* RGB 119/115/132 — muted text, captions, dividers */
    --light-grey: #F1F0F4;      /* RGB 241/240/244 — subtle backgrounds, card fills */
}
```

### Supporting Palette

Secondary colors that support primary colors **without overwhelming them** (use at 20-30% max). For illustrations, data visualizations, and photography accents.

```css
:root {
    --blue: #3D81E7;            /* RGB 61/129/231  */
    --light-green: #C4F6A5;     /* RGB 196/246/165 */
    --green: #88E34F;           /* RGB 136/227/79  */
    --purple: #563FB3;          /* RGB 86/63/179   */
    --purple-2025: #8636F8;     /* RGB 134/54/248  */
    --pink-2025: #F020B3;       /* RGB 240/32/179  */
    --red-2025: #F8475E;        /* RGB 248/71/94   */
    --gold-2025: #FF9421;       /* RGB 255/148/33  */
    --gold: #BEB034;            /* RGB 190/176/52  */
    --light-gold: #E3DF99;      /* RGB 227/223/153 */
}
```

### Domino Gradient 2025

A multi-stop linear gradient for accentuating targeted content. **Never use as a predominant design element or in logos.** Use sparingly for key messages and important areas.

```css
:root {
    --domino-gradient: linear-gradient(
        135deg,
        #FF9421 0%,     /* Gold 2025 */
        #F8475E 34%,    /* Red 2025 */
        #F020B3 66%,    /* Pink 2025 */
        #8636F8 100%    /* Purple 2025 */
    );
}
```

### Color Usage Proportions

White and black dominate. Brand colors are accents, not backgrounds (except Light Purple and Light Blue as approved solid backgrounds).

| Role | Colors | Proportion |
|------|--------|------------|
| **Dominant** | White, Black | ~70% |
| **Brand accent** | Orange, Light Purple, Light Blue | ~20% |
| **Supporting** | Blues, greens, purples, golds | ~10% (max 20-30%) |

### Approved Solid Backgrounds

Per brand guidelines, solid-color slide backgrounds are limited to:
- **Black** (#000000)
- **White** (#FFFFFF)
- **Light Purple** (#D4C9FC)
- **Light Blue** (#A5C5F6)
- **Light Grey** (#F1F0F4) — for subtle variation

### Approved Color Combinations

On **brand-color backgrounds** (orange, purple, light green, light blue, light gold):
- Use **black** elements (text, icons, logo)

On **black backgrounds**:
- Use **white** elements for text/logo
- Use **orange, purple, green, blue, gold** for accent elements

On **white/light backgrounds**:
- Use **black** elements for text/logo
- Use **orange** for CTAs and links

---

## Buttons & Interactive Elements

### Primary Button

Domino Orange filled, pill-shaped, monospace uppercase label.

```css
.btn-primary {
    background: var(--domino-orange);
    color: var(--white);
    font-family: var(--font-mono);
    font-size: var(--small-size);
    text-transform: uppercase;
    letter-spacing: 0.06em;
    padding: clamp(0.5rem, 1.2vw, 0.75rem) clamp(1rem, 2.5vw, 1.5rem);
    border: none;
    border-radius: 999px; /* Pill shape */
    cursor: pointer;
}
```

### Secondary Button

Black filled on light, white filled on dark. Pill-shaped.

```css
.btn-secondary {
    background: var(--black);
    color: var(--white);
    font-family: var(--font-mono);
    font-size: var(--small-size);
    text-transform: uppercase;
    letter-spacing: 0.06em;
    padding: clamp(0.5rem, 1.2vw, 0.75rem) clamp(1rem, 2.5vw, 1.5rem);
    border: none;
    border-radius: 999px;
}
```

### Outline Button

Bordered, transparent fill. Use alongside primary button.

```css
.btn-outline {
    background: transparent;
    color: var(--domino-orange);
    font-family: var(--font-mono);
    font-size: var(--small-size);
    text-transform: uppercase;
    letter-spacing: 0.06em;
    padding: clamp(0.5rem, 1.2vw, 0.75rem) clamp(1rem, 2.5vw, 1.5rem);
    border: 1.5px solid var(--domino-orange);
    border-radius: 999px;
}
```

### Text Link

Monospace, uppercase, with arrow.

```css
.text-link {
    font-family: var(--font-mono);
    font-size: var(--small-size);
    text-transform: uppercase;
    letter-spacing: 0.08em;
    color: var(--black);
    text-decoration: none;
}
.text-link::after {
    content: ' \2192'; /* right arrow */
    margin-left: 0.25em;
}
```

---

## Brand Motif: Line Art Graphic

The line art graphic is a signature visual element. It features **simple, continuous strokes** with a refined, modern look. Use it as a background texture, divider, or accent element.

### Design Principles

- **Minimalist & Clean:** Simple continuous strokes, refined modern look
- **Scalable & Versatile:** Maintains clarity at any size
- **Organic & Geometric Balance:** Abstract curves, structured geometry, reflecting brand personality
- **Color:** Adheres to brand color guidelines; uses Domino Gradient 2025 for strokes or single brand colors
- **Spacing:** Should not overpower other elements; enhances visual hierarchy
- **Variations:** Can be zoomed into to fill space as texture; aim to create movement and balance

### CSS Line Art Pattern (Dark Background)

```css
.line-art-dark {
    position: absolute;
    inset: 0;
    overflow: hidden;
    pointer-events: none;
}

.line-art-dark::before {
    content: '';
    position: absolute;
    width: 150%;
    height: 150%;
    top: -25%;
    right: -25%;
    background: conic-gradient(from 0deg at 50% 50%,
        transparent 0deg,
        rgba(134, 54, 248, 0.15) 30deg,
        transparent 60deg,
        rgba(240, 32, 179, 0.12) 90deg,
        transparent 120deg,
        rgba(255, 148, 33, 0.1) 150deg,
        transparent 180deg
    );
    border-radius: 50%;
    filter: blur(60px);
}
```

### CSS Line Art Pattern (Light Background)

```css
.line-art-light {
    position: absolute;
    inset: 0;
    overflow: hidden;
    pointer-events: none;
}

.line-art-light::before {
    content: '';
    position: absolute;
    width: 120%;
    height: 120%;
    top: -10%;
    right: -20%;
    background:
        repeating-linear-gradient(
            45deg,
            transparent,
            transparent 20px,
            rgba(212, 201, 252, 0.3) 20px,
            rgba(212, 201, 252, 0.3) 21px
        ),
        repeating-linear-gradient(
            -30deg,
            transparent,
            transparent 25px,
            rgba(165, 197, 246, 0.2) 25px,
            rgba(165, 197, 246, 0.2) 26px
        );
}
```

---

## Dark Themes

### 1. Domino Dark Hero

**Vibe:** Bold, modern, high-impact, enterprise. The flagship dark presentation.

**Layout:** Dark background (#111111) with gradient spotlight effect and line art motif. White text, orange CTAs. Logo top-left.

**Typography:**
- Display: `New Grotesk` (700) / fallback `Inter` (700)
- Body: `New Grotesk` (400) / fallback `Inter` (400)
- Mono: `New Grotesk Mono` / fallback `JetBrains Mono`

**Colors:**
```css
:root {
    --font-display: 'New Grotesk', 'Inter', 'Helvetica Neue', sans-serif;
    --font-body: 'New Grotesk', 'Inter', 'Helvetica Neue', sans-serif;
    --font-mono: 'New Grotesk Mono', 'JetBrains Mono', monospace;

    --bg-primary: #111111;
    --bg-surface: #1a1a1a;
    --text-primary: #FFFFFF;
    --text-secondary: rgba(255, 255, 255, 0.7);
    --accent: #FF6543;              /* Domino Orange — CTAs, eyebrow */
    --accent-purple: #D4C9FC;       /* Light Purple — graphical elements */
    --accent-blue: #A5C5F6;         /* Light Blue — graphical elements */
    --domino-gradient: linear-gradient(135deg, #FF9421 0%, #F8475E 34%, #F020B3 66%, #8636F8 100%);
}
```

**Signature Elements:**
- Gradient spotlight blur in background (3 circles: #8636F8 40%, #F8475E 40%, #FF9421 40% opacity, blur=120)
- Line art motif with Domino Gradient 2025 strokes over dark background
- Eyebrow text in orange monospace uppercase above headlines
- Primary CTA: orange pill button; Secondary: outlined
- White logo lockup top-left corner
- Clean, generous whitespace

**Gradient Spotlight Effect:**
```css
.spotlight {
    position: absolute;
    border-radius: 50%;
    filter: blur(120px);
    pointer-events: none;
}
.spotlight-purple {
    width: 40vw; height: 40vw;
    background: rgba(134, 54, 248, 0.4);
    top: -10%; right: -5%;
}
.spotlight-pink {
    width: 30vw; height: 30vw;
    background: rgba(248, 71, 94, 0.4);
    bottom: 10%; left: 10%;
}
.spotlight-gold {
    width: 25vw; height: 25vw;
    background: rgba(255, 148, 33, 0.4);
    bottom: -5%; right: 20%;
}
```

---

### 2. Domino Dark Minimal

**Vibe:** Clean, confident, sophisticated. For technical or data-heavy content.

**Layout:** Pure black background. White text. Orange accent for key callouts. No line art — relies on typography and spacing.

**Typography:**
- Display: `New Grotesk` (700) / fallback `Inter` (700)
- Body: `New Grotesk` (400) / fallback `Inter` (400)
- Mono: `New Grotesk Mono` / fallback `JetBrains Mono`

**Colors:**
```css
:root {
    --font-display: 'New Grotesk', 'Inter', 'Helvetica Neue', sans-serif;
    --font-body: 'New Grotesk', 'Inter', 'Helvetica Neue', sans-serif;
    --font-mono: 'New Grotesk Mono', 'JetBrains Mono', monospace;

    --bg-primary: #000000;
    --bg-surface: #111111;
    --text-primary: #FFFFFF;
    --text-secondary: #777384;      /* Medium Grey */
    --accent: #FF6543;              /* Domino Orange */
    --divider: rgba(255, 255, 255, 0.1);
}
```

**Signature Elements:**
- Generous whitespace — let content breathe
- Thin horizontal divider lines (1px, 10% white opacity)
- Orange eyebrow text above section headers
- Data/metrics displayed large with monospace font
- Cards with subtle #111111 surface on #000000 background
- No gradient, no line art — pure typographic hierarchy

---

### 3. Domino Dark Gradient Accent

**Vibe:** Premium, energetic, forward-looking. For keynotes and product launches.

**Layout:** Dark background with Domino Gradient 2025 used as text fill on hero headlines or as border accents on cards.

**Typography:**
- Display: `New Grotesk` (700) / fallback `Inter` (700)
- Body: `New Grotesk` (400) / fallback `Inter` (400)
- Mono: `New Grotesk Mono` / fallback `JetBrains Mono`

**Colors:**
```css
:root {
    --font-display: 'New Grotesk', 'Inter', 'Helvetica Neue', sans-serif;
    --font-body: 'New Grotesk', 'Inter', 'Helvetica Neue', sans-serif;
    --font-mono: 'New Grotesk Mono', 'JetBrains Mono', monospace;

    --bg-primary: #0a0a0a;
    --bg-surface: #161616;
    --text-primary: #FFFFFF;
    --text-secondary: rgba(255, 255, 255, 0.6);
    --accent: #FF6543;
    --domino-gradient: linear-gradient(135deg, #FF9421 0%, #F8475E 34%, #F020B3 66%, #8636F8 100%);
}
```

**Signature Elements:**
- Gradient text on hero headlines:
  ```css
  .gradient-text {
      background: var(--domino-gradient);
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;
      background-clip: text;
  }
  ```
- Gradient border on feature cards:
  ```css
  .gradient-card {
      background: var(--bg-surface);
      border: 1px solid transparent;
      background-clip: padding-box;
      position: relative;
  }
  .gradient-card::before {
      content: '';
      position: absolute;
      inset: -1px;
      border-radius: inherit;
      background: var(--domino-gradient);
      z-index: -1;
  }
  ```
- Subtle line art motif in corners
- Orange pill CTAs
- Use gradient sparingly — only on 1-2 elements per slide

---

## Light Themes

### 4. Domino Light Corporate

**Vibe:** Professional, clean, trustworthy. The standard corporate presentation.

**Layout:** White background (#FFFFFF). Black text. Orange CTAs. Line art motif with gradient stroke as subtle decoration. Logo top-left in black.

**Typography:**
- Display: `New Grotesk` (700) / fallback `Inter` (700)
- Body: `New Grotesk` (400) / fallback `Inter` (400)
- Mono: `New Grotesk Mono` / fallback `JetBrains Mono`

**Colors:**
```css
:root {
    --font-display: 'New Grotesk', 'Inter', 'Helvetica Neue', sans-serif;
    --font-body: 'New Grotesk', 'Inter', 'Helvetica Neue', sans-serif;
    --font-mono: 'New Grotesk Mono', 'JetBrains Mono', monospace;

    --bg-primary: #FFFFFF;
    --bg-surface: #F1F0F4;         /* Light Grey — cards, sections */
    --text-primary: #000000;
    --text-secondary: #3C3A42;      /* Dark Grey */
    --text-muted: #777384;          /* Medium Grey */
    --accent: #FF6543;              /* Domino Orange — CTAs, links */
    --divider: rgba(0, 0, 0, 0.08);
}
```

**Signature Elements:**
- Light line art motif with gradient stroke in top-right or bottom-right corner
- Orange eyebrow text (monospace, uppercase) above section headlines
- Feature cards with Light Grey (#F1F0F4) background, no border
- Primary button: orange pill; Secondary: black pill
- Generous whitespace — "white space as the continent" (per brand guidelines)
- Black logo lockup top-left corner

---

### 5. Domino Purple

**Vibe:** Approachable, creative, distinctive. For thought leadership and community content.

**Layout:** Light Purple (#D4C9FC) background on select slides, alternating with white. Black text. Orange CTAs.

**Typography:**
- Display: `New Grotesk` (700) / fallback `Inter` (700)
- Body: `New Grotesk` (400) / fallback `Inter` (400)
- Mono: `New Grotesk Mono` / fallback `JetBrains Mono`

**Colors:**
```css
:root {
    --font-display: 'New Grotesk', 'Inter', 'Helvetica Neue', sans-serif;
    --font-body: 'New Grotesk', 'Inter', 'Helvetica Neue', sans-serif;
    --font-mono: 'New Grotesk Mono', 'JetBrains Mono', monospace;

    --bg-primary: #D4C9FC;         /* Light Purple — hero and section slides */
    --bg-secondary: #FFFFFF;        /* White — content slides */
    --bg-surface: rgba(255, 255, 255, 0.5); /* Semi-transparent cards on purple */
    --text-primary: #000000;
    --text-secondary: #3C3A42;
    --text-muted: #777384;
    --accent: #FF6543;              /* Domino Orange */
}
```

**Signature Elements:**
- Alternating slide backgrounds: purple for section titles, white for content
- Cards with semi-transparent white fill on purple backgrounds
- Black logo on purple backgrounds (approved combination)
- Orange pill buttons stand out against purple
- Line art motif in purple tones as subtle background pattern

---

### 6. Domino Blue

**Vibe:** Calm, trustworthy, technical. For product and engineering presentations.

**Layout:** Light Blue (#A5C5F6) background on select slides, alternating with white. Black text. Orange CTAs.

**Typography:**
- Display: `New Grotesk` (700) / fallback `Inter` (700)
- Body: `New Grotesk` (400) / fallback `Inter` (400)
- Mono: `New Grotesk Mono` / fallback `JetBrains Mono`

**Colors:**
```css
:root {
    --font-display: 'New Grotesk', 'Inter', 'Helvetica Neue', sans-serif;
    --font-body: 'New Grotesk', 'Inter', 'Helvetica Neue', sans-serif;
    --font-mono: 'New Grotesk Mono', 'JetBrains Mono', monospace;

    --bg-primary: #A5C5F6;         /* Light Blue — hero and section slides */
    --bg-secondary: #FFFFFF;        /* White — content slides */
    --bg-surface: rgba(255, 255, 255, 0.5);
    --text-primary: #000000;
    --text-secondary: #3C3A42;
    --text-muted: #777384;
    --accent: #FF6543;              /* Domino Orange */
}
```

**Signature Elements:**
- Alternating slide backgrounds: blue for section titles, white for content
- Platform diagrams and architecture slides use this theme
- Technical data in monospace on light grey cards
- Orange pill buttons for CTAs
- Black logo on blue backgrounds (approved combination)

---

### 7. Domino Light Grey

**Vibe:** Understated, corporate, structured. For internal and executive presentations.

**Layout:** Light Grey (#F1F0F4) background with white cards. Black text. Minimal decoration.

**Typography:**
- Display: `New Grotesk` (700) / fallback `Inter` (700)
- Body: `New Grotesk` (400) / fallback `Inter` (400)
- Mono: `New Grotesk Mono` / fallback `JetBrains Mono`

**Colors:**
```css
:root {
    --font-display: 'New Grotesk', 'Inter', 'Helvetica Neue', sans-serif;
    --font-body: 'New Grotesk', 'Inter', 'Helvetica Neue', sans-serif;
    --font-mono: 'New Grotesk Mono', 'JetBrains Mono', monospace;

    --bg-primary: #F1F0F4;         /* Light Grey */
    --bg-surface: #FFFFFF;          /* White cards */
    --text-primary: #000000;
    --text-secondary: #3C3A42;
    --text-muted: #777384;
    --accent: #FF6543;
    --divider: rgba(0, 0, 0, 0.06);
}
```

**Signature Elements:**
- White content cards with soft shadow (`0 1px 3px rgba(0,0,0,0.06)`)
- Clean data tables with alternating white/light-grey rows
- Monospace numbers for metrics and KPIs
- Orange accent limited to CTAs only — very restrained usage
- Thin divider lines between sections

---

## Specialty Themes

### 8. Domino Platform (Product UI Style)

**Vibe:** Clean, functional, data-forward. Mirrors Domino platform UI.

**Layout:** White background with structured grid. Sidebar navigation pattern. Screenshot call-out slides.

**Typography:**
- Display: `New Grotesk` (700) / fallback `Inter` (700)
- Body: `New Grotesk` (400) / fallback `Inter` (400)
- Mono: `New Grotesk Mono` / fallback `JetBrains Mono`

**Colors:**
```css
:root {
    --font-display: 'New Grotesk', 'Inter', 'Helvetica Neue', sans-serif;
    --font-body: 'New Grotesk', 'Inter', 'Helvetica Neue', sans-serif;
    --font-mono: 'New Grotesk Mono', 'JetBrains Mono', monospace;

    --bg-primary: #FFFFFF;
    --bg-sidebar: #000000;
    --bg-surface: #F1F0F4;
    --text-primary: #000000;
    --text-secondary: #3C3A42;
    --text-on-dark: #FFFFFF;
    --accent: #FF6543;
    --accent-purple: #8636F8;       /* Purple 2025 — interactive elements */
    --accent-blue: #3D81E7;         /* Blue — data elements */
}
```

**Signature Elements:**
- Left sidebar (black) with white nav items — mimics Domino platform
- "Eyebrow text" labels in orange monospace above screenshots
- Half-screen screenshot slides with call-out annotations
- Feature bullets with branded orange icons (checkmarks, dots)
- Platform architecture diagrams: thin black lines, orange highlights, icon grid

---

### 9. Domino Data Viz

**Vibe:** Analytical, precise, data-rich. For reports and analytics presentations.

**Layout:** White or light grey background. Charts and metrics as focal points. Supporting palette for data series.

**Typography:**
- Display: `New Grotesk` (700) / fallback `Inter` (700)
- Body: `New Grotesk` (400) / fallback `Inter` (400)
- Mono: `New Grotesk Mono` / fallback `JetBrains Mono` (for all data labels)

**Colors — Data Series:**
```css
:root {
    --font-display: 'New Grotesk', 'Inter', 'Helvetica Neue', sans-serif;
    --font-body: 'New Grotesk', 'Inter', 'Helvetica Neue', sans-serif;
    --font-mono: 'New Grotesk Mono', 'JetBrains Mono', monospace;

    --bg-primary: #FFFFFF;
    --bg-surface: #F1F0F4;
    --text-primary: #000000;

    /* Data series colors from supporting palette */
    --series-1: #FF6543;            /* Domino Orange */
    --series-2: #8636F8;            /* Purple 2025 */
    --series-3: #3D81E7;            /* Blue */
    --series-4: #88E34F;            /* Green */
    --series-5: #FF9421;            /* Gold 2025 */
    --series-6: #F020B3;            /* Pink 2025 */
}
```

**Signature Elements:**
- Large metric numbers in New Grotesk Mono
- Chart containers with Light Grey background
- Data labels always in monospace
- Clean axis lines, no unnecessary gridlines
- Orange used for primary/highlight data series
- Supporting palette for additional series (max 6 colors)

---

## Font Pairing Quick Reference

| Preset | Display Font | Body Font | Mono Font | Source |
|--------|-------------|-----------|-----------|--------|
| All Domino Presets | New Grotesk (700) | New Grotesk (400) | New Grotesk Mono | Archive Foundry |
| **Fallback** | Inter (700) | Inter (400) | JetBrains Mono | Google / JetBrains |

**Note:** New Grotesk requires a license from Archive Foundry. If the font is not available, Inter provides a clean, versatile fallback that maintains the brand's straightforward, grotesk aesthetic.

---

## Diagrammatic Style

For flowcharts, architecture diagrams, and process visuals:

- **Line weight:** Thin (1-2px), black on light backgrounds, white on dark
- **Connectors:** Simple arrows, right angles or gentle curves
- **Boxes:** Rounded corners (4-8px radius), minimal borders
- **Highlight color:** Domino Orange for active/important nodes
- **Icon style:** Simple outlined icons, not filled
- **Labels:** New Grotesk Mono, uppercase, small size
- **Person icons:** Simple line-drawn figures (circle head, body outline)
- **Checkmarks:** Small circled checkmarks with orange fill for completed steps

```css
.diagram-node {
    border: 1.5px solid var(--black);
    border-radius: 6px;
    padding: clamp(0.5rem, 1vw, 1rem);
    font-family: var(--font-mono);
    font-size: var(--small-size);
}

.diagram-node--active {
    border-color: var(--domino-orange);
    background: rgba(255, 101, 67, 0.08);
}

.diagram-arrow {
    stroke: var(--black);
    stroke-width: 1.5;
    fill: none;
    marker-end: url(#arrowhead);
}
```

---

## DO NOT USE (Off-Brand Patterns)

### Fonts
- Do NOT use: Archivo Black, Syne, Fraunces, Bodoni Moda, or other non-brand display fonts
- Do NOT use: system fonts (Arial, Helvetica) as display fonts
- Do NOT use: decorative/script fonts

### Colors
- Do NOT use colors outside the defined palettes
- Do NOT use generic tech-purple gradients (`#6366f1`, etc.)
- Do NOT use the Domino Gradient 2025 as a predominant element or in logos
- Do NOT combine non-approved color pairings (refer to Combinations chart, page 11)

### Layout
- Do NOT use generic hero sections without brand elements
- Do NOT clutter slides — embrace generous whitespace
- Do NOT place the logo on low-contrast backgrounds

### Decorations
- Do NOT use realistic illustrations — abstract shapes and line art only
- Do NOT use gratuitous glassmorphism or drop shadows
- Do NOT use non-brand motif patterns (halftones, scan lines, etc.)
- Do NOT use stock photography that doesn't align with brand photography guidelines (natural light, diverse, professional settings)

---

## Troubleshooting Viewport Issues

### Content Overflows the Slide

**Symptoms:** Scrollbar appears, content cut off, elements outside viewport

**Solutions:**
1. Check slide has `overflow: hidden` (not `overflow: auto` or `visible`)
2. Reduce content — split into multiple slides
3. Ensure all fonts use `clamp()` not fixed `px` or `rem`
4. Add/fix height breakpoints for smaller screens
5. Check images have `max-height: min(50vh, 400px)`

### Text Too Small on Mobile / Too Large on Desktop

**Symptoms:** Unreadable text on phones, oversized text on big screens

**Solutions:**
```css
/* Use clamp with viewport-relative middle value */
font-size: clamp(1rem, 3vw, 2.5rem);
/*              ^       ^      ^
            minimum  scales  maximum */
```

### Content Doesn't Fill Short Screens

**Symptoms:** Excessive whitespace on landscape phones or short browser windows

**Solutions:**
1. Add `@media (max-height: 600px)` and `(max-height: 500px)` breakpoints
2. Reduce padding at smaller heights
3. Hide decorative elements (`display: none`)
4. Consider hiding nav dots and hints on short screens

### Testing Recommendations

Test at these viewport sizes:
- **Desktop:** 1920x1080, 1440x900, 1280x720
- **Tablet:** 1024x768 (landscape), 768x1024 (portrait)
- **Mobile:** 375x667 (iPhone SE), 414x896 (iPhone 11)
- **Landscape phone:** 667x375, 896x414

Use browser DevTools responsive mode to quickly test multiple sizes.
