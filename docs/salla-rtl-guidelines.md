# Salla RTL Best Practices - Arabic Theme Development

## Overview

All Salla themes MUST support RTL (Right-to-Left) layout for Arabic content. Arabic is the primary language for Salla merchants and customers.

**RTL is NOT optional—it's mandatory.**

---

## Core Concept: Logical vs Physical Properties

### The Golden Rule

**Use LOGICAL properties that auto-flip for RTL, not PHYSICAL properties.**

```css
/* ✅ LOGICAL: Auto-flips for RTL */
.element {
    margin-inline-start: 20px;    /* Left in LTR, Right in RTL */
    margin-inline-end: 10px;      /* Right in LTR, Left in RTL */
    padding-inline: 15px;         /* Horizontal padding */
    padding-block: 10px;          /* Vertical padding */
}

/* ❌ PHYSICAL: Doesn't flip */
.element {
    margin-left: 20px;     /* Always left, even in RTL */
    margin-right: 10px;    /* Always right, even in RTL */
    padding: 10px 15px;    /* Ambiguous in RTL */
}
```

---

## CSS Logical Properties Reference

### Margins

```css
/* Physical → Logical */
margin-left     →  margin-inline-start
margin-right    →  margin-inline-end
margin-top      →  margin-block-start
margin-bottom   →  margin-block-end

/* Shorthand */
margin: 10px 20px;          /* Physical: top/bottom left/right */
margin-block: 10px;         /* Logical: top and bottom */
margin-inline: 20px;        /* Logical: start and end */
```

### Padding

```css
/* Physical → Logical */
padding-left    →  padding-inline-start
padding-right   →  padding-inline-end
padding-top     →  padding-block-start
padding-bottom  →  padding-block-end

/* Shorthand */
padding-inline: 20px;       /* Horizontal */
padding-block: 10px;        /* Vertical */
```

### Borders

```css
/* Physical → Logical */
border-left     →  border-inline-start
border-right    →  border-inline-end
border-top      →  border-block-start
border-bottom   →  border-block-end
```

### Border Radius

```css
/* Physical → Logical */
border-top-left-radius     →  border-start-start-radius
border-top-right-radius    →  border-start-end-radius
border-bottom-left-radius  →  border-end-start-radius
border-bottom-right-radius →  border-end-end-radius
```

### Positioning

```css
/* Physical → Logical */
left    →  inset-inline-start
right   →  inset-inline-end
top     →  inset-block-start
bottom  →  inset-block-end
```

---

## Text Alignment

### Use Logical Keywords

```css
/* ✅ CORRECT: Auto-flips */
.text {
    text-align: start;     /* Left in LTR, Right in RTL */
}

.text-end {
    text-align: end;       /* Right in LTR, Left in RTL */
}

/* ❌ WRONG: Doesn't flip */
.text {
    text-align: left;      /* Always left */
}
```

---

## Flexbox & Grid

### Flexbox Direction

```css
/* ✅ CORRECT: Auto-flips */
.flex-container {
    display: flex;
    flex-direction: row;   /* Auto RTL-aware */
}

/* Elements auto-flip from right to left in RTL */
```

### Grid Layout

```css
/* Grid auto-flips in RTL */
.grid {
    display: grid;
    grid-template-columns: 1fr 2fr 1fr;
    /* Columns flip right-to-left in RTL */
}
```

---

## Direction Detection

### HTML dir Attribute

```html
<!-- Raed/Twilight provides this automatically -->
<html dir="{{ theme.direction }}">
    <!-- Auto: dir="rtl" for Arabic, dir="ltr" for English -->
</html>
```

### CSS Direction Property

```css
/* Usually set on html/body automatically */
html {
    direction: rtl;  /* For Arabic */
}
```

---

## Icons & Images

### Flipping Icons

Some icons should flip in RTL (arrows, chevrons), others shouldn't (logos, symbols).

```css
/* ✅ Flip directional icons */
.icon-arrow {
    /* In RTL: auto-flips via transform */
}

[dir="rtl"] .icon-arrow {
    transform: scaleX(-1);  /* Horizontal flip */
}

/* ❌ Don't flip logos */
.logo {
    /* Never flip */
}
```

### Which Icons to Flip?

**Flip These:**
- ← → (Arrows)
- ◀ ▶ (Chevrons/Play buttons pointing left/right)
- ⟵ ⟶ (Back/Forward navigation)
- ↶ ↷ (Undo/Redo)

**Don't Flip These:**
- ✓ ✗ (Checkmarks, X)
- ⊕ ⊗ (Plus, Minus)
- ⚙ (Settings)
- 🏠 (Home)
- Logos
- Product images

---

## Lists & Bullets

```css
/* Bullets auto-flip to right side in RTL */
ul {
    padding-inline-start: 40px;  /* Auto-flips */
}

/* Custom bullets */
ul li::before {
    content: "•";
    margin-inline-end: 10px;  /* Space after bullet (left in RTL) */
}
```

---

## Forms

### Input Alignment

```css
input,
textarea,
select {
    /* Text aligns to start (right in RTL) */
    text-align: start;
}
```

### Placeholder Text

```html
<!-- Placeholder auto-aligns in RTL -->
<input type="text" placeholder="أدخل اسمك" dir="auto">
```

---

## Common Patterns

### 1. Card Layout

```css
.card {
    /* GOOD: Logical properties */
    padding-inline: 20px;
    padding-block: 15px;
    border-inline-start: 3px solid blue;
    
    /* Text aligns properly */
    text-align: start;
}

.card-image {
    /* GOOD: Logical margin */
    margin-inline-end: 15px;  /* Space after image */
}
```

### 2. Navigation Menu

```css
.nav {
    display: flex;
    /* Auto RTL-aware */
}

.nav-item {
    /* Spacing between items */
    margin-inline-end: 20px;
}

.nav-item:last-child {
    margin-inline-end: 0;
}
```

### 3. Hero Section with Text Overlay

```css
.hero {
    position: relative;
}

.hero-content {
    position: absolute;
    inset-inline-start: 40px;  /* Left in LTR, Right in RTL */
    inset-block-start: 50%;
    transform: translateY(-50%);
    
    /* Text aligns */
    text-align: start;
}
```

### 4. Product Card

```css
.product-card {
    display: flex;
    flex-direction: row;  /* Auto-flips in RTL */
}

.product-image {
    margin-inline-end: 20px;  /* Space after image */
}

.product-info {
    /* Content flows naturally */
    text-align: start;
}

.price {
    /* Price on the end (left in RTL) */
    margin-inline-start: auto;
}
```

---

## Typography in Arabic

### Font Selection

```css
/* Use Arabic-friendly fonts */
body {
    font-family: 'Cairo', 'Tajawal', 'Almarai', sans-serif;
}
```

**Recommended Arabic Fonts:**
- Cairo
- Tajawal
- Almarai
- IBM Plex Sans Arabic
- Noto Sans Arabic

### Font Size

```css
/* Arabic needs slightly larger font size */
body {
    font-size: 16px;  /* Minimum */
}

[dir="rtl"] body {
    font-size: 17px;  /* Slightly larger for Arabic */
}
```

### Line Height

```css
/* More generous for Arabic */
body {
    line-height: 1.8;  /* Arabic text needs more space */
}
```

---

## Numbers in Arabic

### Arabic vs Western Numerals

```html
<!-- Store setting controls this -->
{{ product.price }}

<!-- Outputs: -->
<!-- If arabic_numbers_enabled: ١٢٣٤ -->
<!-- If not: 1234 -->
```

### Checking Setting in Twig

```twig
{% if store.settings.arabic_numbers_enabled %}
    {# Use Arabic numerals (٠١٢٣) #}
{% else %}
    {# Use Western numerals (0123) #}
{% endif %}
```

---

## Testing RTL

### 1. Visual Testing

```css
/* Add temporary border to see direction */
* {
    outline: 1px solid red;  /* Debug only */
}
```

### 2. Browser DevTools

Chrome DevTools:
1. Open DevTools
2. Settings → Experiments
3. Enable "Emulation of :dir() pseudo-class"
4. Can toggle RTL in Elements panel

### 3. Switch Language

In Salla store:
- Switch language to Arabic
- Check all pages
- Verify layout flips correctly

---

## Common RTL Mistakes

### ❌ Mistake 1: Using Left/Right

```css
/* WRONG */
.sidebar {
    float: left;
    margin-right: 20px;
}

/* CORRECT */
.sidebar {
    float: inline-start;
    margin-inline-end: 20px;
}
```

---

### ❌ Mistake 2: Hardcoded Text Alignment

```css
/* WRONG */
h1 {
    text-align: left;
}

/* CORRECT */
h1 {
    text-align: start;
}
```

---

### ❌ Mistake 3: Absolute Positioning

```css
/* WRONG */
.badge {
    position: absolute;
    top: 10px;
    right: 10px;
}

/* CORRECT */
.badge {
    position: absolute;
    inset-block-start: 10px;
    inset-inline-end: 10px;
}
```

---

### ❌ Mistake 4: Transform Origin

```css
/* WRONG: Assumes left origin */
.dropdown {
    transform-origin: top left;
}

/* CORRECT: Use logical */
.dropdown {
    transform-origin: block-start inline-start;
}
```

---

### ❌ Mistake 5: Gradient Direction

```css
/* WRONG */
.gradient {
    background: linear-gradient(to right, red, blue);
}

/* CORRECT */
.gradient {
    background: linear-gradient(to inline-end, red, blue);
}
```

---

## Fallback for Older Browsers

Some browsers don't support logical properties yet. Use this pattern:

```css
.element {
    /* Fallback for old browsers */
    margin-left: 20px;
    
    /* Override with logical property */
    margin-inline-start: 20px;
}

[dir="rtl"] .element {
    /* Manual RTL for fallback */
    margin-left: 0;
    margin-right: 20px;
}
```

**But:** Salla's supported browsers (Chrome, Safari, Firefox) all support logical properties, so this is rarely needed.

---

## RTL-Aware JavaScript

### Detecting Direction

```javascript
// Get current direction
const isRTL = document.documentElement.dir === 'rtl';

// Or from Salla config
const direction = salla.config.get('theme.direction');
```

### Swipe Gestures

```javascript
// Handle swipe considering RTL
function handleSwipe(direction) {
    const isRTL = document.documentElement.dir === 'rtl';
    
    if (direction === 'left') {
        // In RTL, left swipe = next (opposite of LTR)
        isRTL ? previousSlide() : nextSlide();
    } else {
        isRTL ? nextSlide() : previousSlide();
    }
}
```

---

## Tailwind CSS & RTL

### Using Tailwind with RTL

```html
<!-- Tailwind auto-handles RTL -->
<div class="ml-4">  <!-- margin-left in LTR, margin-right in RTL -->
<div class="mr-4">  <!-- margin-right in LTR, margin-left in RTL -->

<!-- Explicit RTL variants (rarely needed) -->
<div class="ltr:ml-4 rtl:mr-4">
```

Tailwind automatically handles RTL if you set `dir="rtl"` on `<html>`.

---

## Testing Checklist

```
RTL Visual Check:
- [ ] Layout mirrors correctly
- [ ] Text aligns to right
- [ ] Margins/padding flip properly
- [ ] Navigation flows right-to-left
- [ ] Icons flip appropriately
- [ ] No overlapping text
- [ ] No cut-off content

Functionality:
- [ ] Forms work in RTL
- [ ] Dropdowns open correctly
- [ ] Sliders/carousels flow right-to-left
- [ ] Tooltips position correctly
- [ ] Modals center properly

Typography:
- [ ] Arabic font loads
- [ ] Line height sufficient
- [ ] Font size readable (17px+)
- [ ] No text clipping

Performance:
- [ ] Arabic font optimized
- [ ] No layout shift
```

---

## Quick Reference

### Conversion Cheat Sheet

| Physical Property | Logical Property |
|------------------|------------------|
| `margin-left` | `margin-inline-start` |
| `margin-right` | `margin-inline-end` |
| `padding-left` | `padding-inline-start` |
| `padding-right` | `padding-inline-end` |
| `border-left` | `border-inline-start` |
| `border-right` | `border-inline-end` |
| `left` | `inset-inline-start` |
| `right` | `inset-inline-end` |
| `text-align: left` | `text-align: start` |
| `text-align: right` | `text-align: end` |
| `float: left` | `float: inline-start` |
| `float: right` | `float: inline-end` |

---

## Summary

**RTL Requirements:**
✅ Use logical CSS properties  
✅ Use `start`/`end` for text alignment  
✅ Flip directional icons  
✅ Test with Arabic content  
✅ Use Arabic-friendly fonts  
✅ Generous line-height (1.8)  
✅ Font size 17px+ for Arabic  

**Remember:**
- Arabic is PRIMARY language for Salla
- RTL is NOT optional
- Test EVERY feature in RTL
- Logical properties are your friend
- When in doubt, use `start`/`end` not `left`/`right`

**The majority of your users read Arabic. If it breaks in RTL, your theme fails.**
