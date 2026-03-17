# Salla Twilight Framework - Complete Documentation

## Overview

Twilight is Salla's theme engine that enables developers to create customizable themes for Salla Platform stores. It provides a complete framework for building modern, responsive e-commerce themes.

---

## Core Concepts

### What is Twilight?

Twilight enables developers to create memorable experiences for Salla store's look-and-feel for the benefit of Merchants and their Customers. With custom themes, developers can adapt merchant stores to growing needs over time.

**Key Features:**
- Continuously updated educational resources
- Enhanced Salla CLI commands
- GitHub integration for code management
- Web components with JavaScript SDK
- Quick access to store data through Twilight Engine

---

## Architecture

### Framework Components

The Twilight Framework consists of several packages:

1. **@salla.sa/base** - Foundation layer with core utilities
2. **@salla.sa/twilight** - Main SDK for Salla themes
3. **@salla.sa/twilight-components** - Web components library
4. **@salla.sa/twilight-tailwind-theme** - Tailwind CSS theme

### Technology Stack

- **Templating:** Twig (PHP templating engine)
- **CSS Framework:** Tailwind CSS (default, optional)
- **JavaScript SDK:** Twilight JS SDK for API communication
- **Web Components:** Custom elements for UI components

---

## Installation & Setup

### Using Twilight in Themes

When using Twilight within themes, **NO manual installation** is needed:
- Twilight theme engine automatically injects the latest version
- No need to include in bundle or HTML
- Automatic initialization via `{% hook 'body:end' %}`

### NPM Installation (for component development)

```bash
npm install @salla.sa/twilight
# or
yarn add @salla.sa/twilight
```

---

## Twilight JS SDK

### Initialization

**For Themes:** Initialization is automatic - no need to call `salla.init()`

The SDK automatically initializes thanks to the body:end hook:
```twig
{% hook 'body:end' %}
```

### Main SDK APIs

The SDK provides REST API endpoints for:

1. **Authorization APIs**
   - Customer login/logout
   - Session management
   - User authentication

2. **Cart APIs**
   ```javascript
   // Add item to cart
   salla.cart.addItem(productId, quantity, options);
   
   // Add item with multiple options
   salla.cart.addItem(productId, 1, {
       option1: 'value1',
       option2: 'value2'
   });
   ```

3. **Wishlist APIs**
   ```javascript
   // Add to wishlist
   salla.wishlist.toggle(productId);
   ```

4. **Product APIs**
5. **Order APIs**
6. **Customer APIs**

### Event System

Twilight provides powerful event handling:

```javascript
// Cart events
salla.event.cart.onItemAdded((response, product_id) => {
    console.log('Item added:', response);
});

salla.event.cart.onItemAddedFailed((error) => {
    console.log('Failed to add item:', error);
});

// Wishlist events
salla.event.wishlist.onAdded((response, product_id) => {
    console.log('Added to wishlist:', response, product_id);
});
```

### Configuration

```javascript
// Get configuration value
const userId = salla.config.get('user.id');
const currency = salla.config.get('currency.code');

// Set configuration value
salla.config.set('key', 'value');
```

### Version Information

```javascript
// Get package versions
console.log(Salla.versions.twilight);  // e.g., "v2.14.360"
console.log(Salla.versions.base);      // e.g., "v2.14.143"
```

---

## Twig Templating

### Twilight Twig Extensions

Twilight adds custom helpers and filters to standard Twig:

#### Helper Functions

**link.is_active(pattern)**
```twig
{% if link.is_active('product/*') %}
    {# Current page matches pattern #}
{% endif %}
```

**page.title()**
```twig
<title>{{ page.title() }}</title>
```

**link(path)**
```twig
<a href="{{ link('cart') }}">
    {# Output: https://www.my-store.com/cart #}
</a>
```

**trans_choice(key, count)**
```twig
{{ trans_choice('products.count', product_count) }}
{# Changes message based on count (singular/plural) #}
```

#### Filters

**asset** - Link to theme files
```twig
<link href="{{ 'styles.css' | asset }}" rel="stylesheet">
```

**camel_case** - Convert to camelCase
```twig
{{ 'hello world' | camel_case }}
{# Output: helloWorld #}
```

**salla** - Get predefined file links
```twig
<link href="{{ 'font' | salla }}" rel="stylesheet">
```

**currency** - Add currency sign
```twig
{{ 100 | currency }}
{# Output: 100 SAR #}
```

**date** - Format date with language consideration
```twig
{{ product.created_at | date('Y-m-d') }}
```

**is_placeholder** - Check if image is placeholder
```twig
{% if product.image | is_placeholder %}
    {# Show default image #}
{% endif %}
```

**slugify** - Replace spaces with dashes
```twig
{{ 'Hello World' | slugify }}
{# Output: hello-world #}
```

---

## Tailwind CSS Integration

### Default Configuration

Twilight Web Components are built on Tailwind CSS by default.

### tailwind.config.js

```javascript
module.exports = {
    content: [
        './src/**/*.{twig,js}',
        './node_modules/@salla.sa/twilight-components/**/*.js'
    ],
    theme: {
        extend: {
            colors: {
                primary: 'var(--color-primary)',
                // ... theme colors
            },
            fontFamily: {
                sans: ['var(--font-main)', 'sans-serif']
            }
        }
    }
}
```

### Adding Twilight Tailwind Theme

```javascript
// tailwind.config.js
module.exports = {
    presets: [
        require('@salla.sa/twilight-tailwind-theme')
    ],
    // ... your config
}
```

---

## CSS Variables

Twilight uses CSS Variables for theming:

```css
:root {
    --color-primary: #your-color;
    --color-text: #your-text-color;
    --font-main: 'Your Font', sans-serif;
    --border-radius: 8px;
}
```

### Using in Components

```twig
<button style="background: var(--color-primary); color: white;">
    Click Me
</button>
```

---

## Web Components

### Available Components

Twilight provides pre-built web components for common UI elements.

### Using Components

```html
<!-- Product Card -->
<salla-product-card 
    product-id="123" 
    show-add-to-cart="true">
</salla-product-card>

<!-- Button -->
<salla-button 
    type="primary" 
    size="large">
    Add to Cart
</salla-button>
```

### Customization

Components can be styled using:
1. **CSS Variables** (recommended)
2. **Tailwind Classes**
3. **Custom CSS Classes**

```css
/* Custom styling for salla-button */
salla-button {
    --button-bg: #custom-color;
    --button-radius: 12px;
}
```

---

## Salla Components (Twig)

### Using Salla Components

```twig
{# Render home components #}
{% component 'home' %}

{# Render product card #}
{% component 'product.card' with {
    product: product,
    display: 'grid'
} %}

{# Render slider #}
{% component 'home.slider' %}
```

### Available Components

- `home` - Home page components
- `product.card` - Product card display
- `home.slider` - Image slider
- `home.featured-products` - Featured products section
- And many more...

---

## Mobile-First Development

### Breakpoints (Tailwind Default)

```css
/* Mobile: default (no media query) */
.element { padding: 1rem; }

/* Tablet: 768px+ */
@media (min-width: 768px) {
    .element { padding: 2rem; }
}

/* Desktop: 1024px+ */
@media (min-width: 1024px) {
    .element { padding: 3rem; }
}
```

### Touch Targets

- Minimum: **44px × 44px**
- Recommended: **48px × 48px**

---

## RTL Support

### Logical Properties (Recommended)

```css
/* Use logical properties */
.card {
    margin-inline-start: 1rem;  /* Auto-flips for RTL */
    padding-inline: 1rem;       /* Horizontal padding */
    border-start-start-radius: 8px;
}

/* DON'T use physical properties */
.card {
    margin-left: 1rem;   /* Won't flip in RTL */
    padding: 1rem 2rem;  /* Ambiguous */
}
```

### Direction Detection

```twig
<div dir="{{ theme.direction }}">
    {# Auto RTL/LTR #}
</div>
```

---

## Performance Best Practices

### Image Optimization

```twig
{# Responsive images #}
<img 
    src="{{ product.image }}" 
    srcset="{{ product.image }}?w=400 400w,
            {{ product.image }}?w=800 800w"
    sizes="(max-width: 768px) 400px, 800px"
    loading="lazy"
    alt="{{ product.name }}">
```

### Lazy Loading

```html
<img loading="lazy" src="image.jpg">
```

### Code Splitting

Split CSS and JS by page/component for better performance.

---

## Best Practices

### 1. Use Salla Components

```twig
{# GOOD: Use built-in component #}
{% component 'product.card' with { product: product } %}

{# AVOID: Building from scratch #}
<div class="product-card">...</div>
```

### 2. Mobile-First CSS

```scss
// GOOD: Mobile first
.hero {
    padding: 20px;
    
    @media (min-width: 1024px) {
        padding: 60px;
    }
}

// AVOID: Desktop first
.hero {
    padding: 60px;
    
    @media (max-width: 1023px) {
        padding: 20px;
    }
}
```

### 3. Use CSS Variables

```css
/* GOOD: Themeable */
.button {
    background: var(--color-primary);
}

/* AVOID: Hard-coded */
.button {
    background: #3490dc;
}
```

### 4. RTL-Native

```css
/* GOOD: Auto-flips */
.card {
    margin-inline-start: 1rem;
}

/* AVOID: Manual RTL handling */
.card {
    margin-left: 1rem;
}
.rtl .card {
    margin-left: 0;
    margin-right: 1rem;
}
```

---

## Debugging

### Console Logging

```javascript
// Check Twilight version
console.log(Salla.versions.twilight);

// Check configuration
console.log(salla.config.get('store'));

// Listen to all events (development only)
salla.event.on('*', (eventName, data) => {
    console.log('Event:', eventName, data);
});
```

### Browser DevTools

- Use Elements panel to inspect web components
- Check Network tab for API calls
- Console for JavaScript errors

---

## Common Patterns

### Product Quick Add

```javascript
// Add product to cart
document.querySelector('.quick-add-btn').addEventListener('click', async (e) => {
    const productId = e.target.dataset.productId;
    
    try {
        await salla.cart.addItem(productId, 1);
        // Success handled by onItemAdded event
    } catch (error) {
        // Error handled by onItemAddedFailed event
    }
});
```

### Wishlist Toggle

```javascript
// Toggle wishlist
document.querySelector('.wishlist-btn').addEventListener('click', async (e) => {
    const productId = e.target.dataset.productId;
    await salla.wishlist.toggle(productId);
});
```

### Dynamic Content Loading

```javascript
// Load more products
async function loadMoreProducts(page) {
    const response = await fetch(`/api/products?page=${page}`);
    const data = await response.json();
    // Render products
}
```

---

## Resources

### Official Links

- **Documentation:** https://docs.salla.dev
- **GitHub:** https://github.com/SallaApp
- **NPM:** https://www.npmjs.com/package/@salla.sa/twilight
- **Telegram Community:** Developer support channel

### Getting Help

- GitHub Issues: Bug reports and feature requests
- Telegram Bot: Quick questions
- Global Developer Community: Developer discussions

---

This documentation covers the core Twilight Framework concepts. For specific component documentation, see the Salla Components Reference.
