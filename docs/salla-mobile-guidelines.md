# Salla Mobile-First Guidelines

## Philosophy

**Mobile is PRIMARY, not secondary.**

In Saudi Arabia and the Gulf region, **70-80% of e-commerce traffic comes from mobile devices**. Your theme MUST work perfectly on mobile first, then enhance for larger screens.

---

## Breakpoints

### Salla Standard Breakpoints

```css
/* Mobile: 375px - 767px (PRIMARY) */
/* Default styles - no media query needed */
.element {
    padding: 20px;
}

/* Tablet: 768px - 1023px */
@media (min-width: 768px) {
    .element {
        padding: 40px;
    }
}

/* Desktop: 1024px+ */
@media (min-width: 1024px) {
    .element {
        padding: 60px;
    }
}
```

### Tailwind Breakpoints (if using Tailwind)

```html
<!-- Mobile: default (no prefix) -->
<div class="p-5">

<!-- Tablet: md: prefix (768px+) -->
<div class="p-5 md:p-10">

<!-- Desktop: lg: prefix (1024px+) -->
<div class="p-5 md:p-10 lg:p-15">
```

---

## Mobile-First CSS Pattern

### The Golden Rule

**Start with mobile, add complexity for larger screens.**

```scss
// ✅ CORRECT: Mobile-First
.hero {
    // Mobile (375px+) - DEFAULT
    padding: 20px;
    font-size: 24px;
    flex-direction: column;
    
    // Tablet (768px+) - ENHANCE
    @media (min-width: 768px) {
        padding: 40px;
        font-size: 32px;
    }
    
    // Desktop (1024px+) - FURTHER ENHANCE
    @media (min-width: 1024px) {
        padding: 60px;
        font-size: 48px;
        flex-direction: row;
    }
}
```

```scss
// ❌ WRONG: Desktop-First
.hero {
    // Desktop defaults
    padding: 60px;
    font-size: 48px;
    flex-direction: row;
    
    // Scaling down
    @media (max-width: 1023px) {
        padding: 40px;
        font-size: 32px;
    }
    
    @media (max-width: 767px) {
        padding: 20px;
        font-size: 24px;
        flex-direction: column;
    }
}
```

---

## Viewport Meta Tag

**Always include in `<head>`:**

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```

This ensures proper scaling on mobile devices.

---

## Touch Targets

### Minimum Sizes

**WCAG 2.1 Requirements:**
- Minimum: **44px × 44px**
- Recommended: **48px × 48px**

```scss
// ✅ GOOD: Large enough for fingers
.button {
    min-height: 48px;
    min-width: 48px;
    padding: 12px 24px;
}

// ❌ BAD: Too small
.button {
    padding: 4px 8px;  // Way too small!
}
```

### Spacing Between Targets

```scss
// Add space between tappable elements
.nav-links a {
    min-height: 44px;
    margin-bottom: 8px;  // Space between links
}
```

---

## Typography

### Font Sizes

```scss
// Mobile (default)
body {
    font-size: 16px;  // Never below 16px (prevents zoom on iOS)
}

h1 {
    font-size: 28px;  // Mobile
    
    @media (min-width: 768px) {
        font-size: 36px;  // Tablet
    }
    
    @media (min-width: 1024px) {
        font-size: 48px;  // Desktop
    }
}
```

### Line Height

```scss
// Mobile: More generous line-height for readability
body {
    line-height: 1.6;
}

.long-text {
    line-height: 1.8;  // Even more for long paragraphs
}
```

---

## Layout Patterns

### 1. Single Column (Mobile) → Multi-Column (Desktop)

```scss
.products-grid {
    // Mobile: 1 column
    display: grid;
    grid-template-columns: 1fr;
    gap: 20px;
    
    // Tablet: 2 columns
    @media (min-width: 768px) {
        grid-template-columns: repeat(2, 1fr);
        gap: 30px;
    }
    
    // Desktop: 3-4 columns
    @media (min-width: 1024px) {
        grid-template-columns: repeat(4, 1fr);
        gap: 40px;
    }
}
```

### 2. Stack (Mobile) → Side-by-Side (Desktop)

```scss
.hero {
    // Mobile: Stack vertically
    display: flex;
    flex-direction: column;
    
    // Desktop: Side by side
    @media (min-width: 1024px) {
        flex-direction: row;
        align-items: center;
    }
}
```

### 3. Full Width (Mobile) → Contained (Desktop)

```scss
.container {
    // Mobile: Full width with padding
    width: 100%;
    padding: 0 20px;
    
    // Tablet: Add max-width
    @media (min-width: 768px) {
        max-width: 720px;
        margin: 0 auto;
    }
    
    // Desktop: Wider max-width
    @media (min-width: 1024px) {
        max-width: 1200px;
    }
}
```

---

## Images

### Responsive Images

```html
<!-- Mobile-first with srcset -->
<img 
    src="image-small.jpg" 
    srcset="
        image-small.jpg 400w,
        image-medium.jpg 800w,
        image-large.jpg 1200w
    "
    sizes="
        (max-width: 767px) 400px,
        (max-width: 1023px) 800px,
        1200px
    "
    alt="Description"
    loading="lazy"
>
```

### CSS Background Images

```scss
.hero {
    // Mobile image
    background-image: url('hero-mobile.jpg');
    background-size: cover;
    
    // Tablet image
    @media (min-width: 768px) {
        background-image: url('hero-tablet.jpg');
    }
    
    // Desktop image
    @media (min-width: 1024px) {
        background-image: url('hero-desktop.jpg');
    }
}
```

### Image Optimization

- **Mobile:** Max 800px width, <200KB
- **Tablet:** Max 1200px width, <300KB
- **Desktop:** Max 1920px width, <500KB

---

## Navigation

### Mobile Menu Pattern

```scss
.main-nav {
    // Mobile: Hidden by default, hamburger menu
    display: none;
    position: fixed;
    top: 0;
    right: 0;
    width: 280px;
    height: 100vh;
    background: white;
    transform: translateX(100%);
    transition: transform 0.3s;
    
    &.is-open {
        display: block;
        transform: translateX(0);
    }
    
    // Desktop: Horizontal menu
    @media (min-width: 1024px) {
        display: flex;
        position: static;
        width: auto;
        height: auto;
        transform: none;
        flex-direction: row;
    }
}

.menu-toggle {
    // Mobile: Show hamburger
    display: block;
    
    // Desktop: Hide hamburger
    @media (min-width: 1024px) {
        display: none;
    }
}
```

---

## Performance

### Critical CSS

```html
<head>
    <!-- Inline critical mobile CSS -->
    <style>
        /* Mobile-only critical styles */
        body { margin: 0; font-size: 16px; }
        .header { padding: 10px; }
    </style>
    
    <!-- Load full CSS async -->
    <link rel="stylesheet" href="styles.css" media="print" onload="this.media='all'">
</head>
```

### Lazy Loading

```html
<!-- Images below the fold -->
<img src="image.jpg" loading="lazy" alt="...">
```

### Reduce HTTP Requests

```scss
// Combine small icons into CSS (data URIs or SVG)
.icon-search {
    background-image: url('data:image/svg+xml,...');
}
```

---

## Forms

### Mobile-Friendly Inputs

```html
<!-- Full width on mobile -->
<input 
    type="text" 
    placeholder="أدخل اسمك"
    style="width: 100%; min-height: 48px; font-size: 16px;"
>

<!-- Proper input types -->
<input type="email">     <!-- Shows @ key on mobile -->
<input type="tel">       <!-- Shows number pad -->
<input type="number">    <!-- Number input -->
```

### Form Layout

```scss
.form-group {
    // Mobile: Full width
    width: 100%;
    margin-bottom: 20px;
    
    // Desktop: Side by side
    @media (min-width: 1024px) {
        width: 48%;
        display: inline-block;
    }
}
```

---

## Testing

### Required Mobile Tests

```
✅ Physical Device Testing (MANDATORY)
   - iPhone (Safari)
   - Android (Chrome)
   
✅ Browser DevTools Testing
   - Chrome DevTools (Mobile view)
   - Firefox Responsive Mode
   
✅ Screen Sizes to Test
   - 375px (iPhone SE)
   - 390px (iPhone 12/13/14)
   - 414px (iPhone Plus)
   - 360px (Android)
   
✅ Orientation Tests
   - Portrait (default)
   - Landscape
```

### Mobile Testing Checklist

```
Performance:
- [ ] Page loads in < 3 seconds on 3G
- [ ] No horizontal scroll at any width
- [ ] Images optimized (< 200KB on mobile)
- [ ] Lighthouse Mobile score > 85

Touch Interaction:
- [ ] All buttons min 44×44px
- [ ] Spacing between clickable elements
- [ ] No hover-only interactions
- [ ] Touch/tap feedback visible

Layout:
- [ ] Text readable without zoom (16px+)
- [ ] No text cut off
- [ ] Proper RTL on mobile
- [ ] Forms easy to fill on mobile

Functionality:
- [ ] Navigation accessible
- [ ] Cart works perfectly
- [ ] Checkout flows smoothly
- [ ] Search functional
```

---

## Common Mobile Mistakes

### ❌ Don't: Desktop-First Thinking

```scss
// WRONG
.container {
    width: 1200px;  // Breaks on mobile!
}
```

```scss
// CORRECT
.container {
    width: 100%;
    max-width: 1200px;
}
```

---

### ❌ Don't: Tiny Touch Targets

```scss
// WRONG
.close-btn {
    width: 20px;
    height: 20px;
}
```

```scss
// CORRECT
.close-btn {
    width: 44px;
    height: 44px;
    padding: 12px;
}
```

---

### ❌ Don't: Hover-Only Interactions

```scss
// WRONG: Only works on hover
.dropdown {
    display: none;
}
.menu:hover .dropdown {
    display: block;
}
```

```scss
// CORRECT: Click/tap to toggle
.dropdown {
    display: none;
}
.menu.is-open .dropdown {
    display: block;
}
```

---

### ❌ Don't: Fixed Viewport Width

```html
<!-- WRONG -->
<meta name="viewport" content="width=1024">
```

```html
<!-- CORRECT -->
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```

---

## Mobile-Specific Features

### Swipe Gestures

```javascript
// Enable swipe on mobile
let touchStartX = 0;
let touchEndX = 0;

element.addEventListener('touchstart', (e) => {
    touchStartX = e.changedTouches[0].screenX;
});

element.addEventListener('touchend', (e) => {
    touchEndX = e.changedTouches[0].screenX;
    handleSwipe();
});

function handleSwipe() {
    if (touchEndX < touchStartX) {
        // Swipe left
    }
    if (touchEndX > touchStartX) {
        // Swipe right
    }
}
```

### Pull to Refresh (Disable if needed)

```css
/* Prevent pull-to-refresh on mobile */
body {
    overscroll-behavior-y: contain;
}
```

---

## Accessibility on Mobile

```scss
// Larger text for better readability
body {
    font-size: 16px;  // Minimum
    
    @media (min-width: 1024px) {
        font-size: 18px;  // Can be larger on desktop
    }
}

// High contrast for sunlight readability
.button {
    background: #000;
    color: #fff;
    // Strong contrast ratio
}

// Focus indicators for keyboard navigation
button:focus {
    outline: 3px solid #4A90E2;
    outline-offset: 2px;
}
```

---

## Quick Reference

### Mobile-First Workflow

```
1. Design for 375px first
2. Build HTML structure
3. Style for mobile (no media queries)
4. Test on real device
5. Add tablet enhancements (768px+)
6. Add desktop enhancements (1024px+)
7. Test all breakpoints
```

### Performance Budget

```
Mobile Target:
- First Contentful Paint: < 1.5s
- Time to Interactive: < 3.5s
- Speed Index: < 3.4s
- Total Page Size: < 1.5MB
- Lighthouse Mobile: > 85
```

---

## Summary

**Mobile-First Means:**
✅ Design for 375px first  
✅ Touch targets min 44px  
✅ Font size min 16px  
✅ Test on real devices  
✅ No horizontal scroll  
✅ Fast load times (< 3s)  
✅ Images optimized  
✅ Simple, clear navigation  

**Remember:**
**70-80% of your users are on mobile in Saudi/Gulf.** 
If it doesn't work perfectly on mobile, it doesn't work.

Mobile is not an afterthought—it's the PRIMARY platform.
