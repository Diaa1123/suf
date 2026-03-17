# Raed Template - Structure & Best Practices

## Overview

Theme Raed is Salla's official starter theme - a collection of files and folders that define the Salla Store presentation layer. It's built on the Twilight Framework and serves as the foundation for creating custom themes.

**Repository:** https://github.com/SallaApp/theme-raed

---

## Directory Structure

```
theme-raed/
├── src/
│   ├── assets/
│   │   ├── fonts/           # Custom fonts
│   │   ├── images/          # Theme images and icons
│   │   │   └── defaults/    # Default placeholder images
│   │   ├── js/              # JavaScript files
│   │   │   ├── app.js       # Main app entry
│   │   │   └── partials/    # JS modules
│   │   └── styles/          # SCSS/CSS files
│   │       ├── main.scss    # Main stylesheet
│   │       ├── base/        # Base styles, variables
│   │       ├── components/  # Component styles
│   │       ├── pages/       # Page-specific styles
│   │       └── sections/    # Section styles
│   │
│   └── views/
│       ├── layouts/
│       │   └── master.twig  # Master layout template
│       │
│       ├── pages/
│       │   ├── index.twig        # Home page
│       │   ├── product.twig      # Single product
│       │   ├── products.twig     # Product listing
│       │   ├── cart.twig         # Shopping cart
│       │   ├── profile.twig      # Customer profile
│       │   └── ...               # Other pages
│       │
│       └── components/
│           ├── header.twig       # Site header
│           ├── footer.twig       # Site footer
│           │
│           ├── home/             # Home page components
│           │   ├── slider.twig
│           │   ├── brands.twig
│           │   ├── main-links.twig
│           │   ├── square-photos.twig
│           │   ├── enhanced-slider.twig
│           │   └── ...
│           │
│           └── product/          # Product components
│               ├── card.twig     # Product card
│               ├── gallery.twig  # Image gallery
│               └── ...
│
├── twilight.json         # Theme configuration
├── package.json          # NPM dependencies
├── tailwind.config.js    # Tailwind configuration
├── webpack.mix.js        # Laravel Mix config
└── README.md             # Theme documentation
```

---

## Core Files

### 1. twilight.json

The main configuration file located in root directory.

```json
{
    "version": "1.0.0",
    "theme_name": "Theme Raed",
    "repository": "https://github.com/SallaApp/theme-raed",
    "author_email": "support@salla.sa",
    
    "features": [
        "mega-menu",
        "fonts",
        "color",
        "breadcrumb",
        "unite-cards-height",
        "component-featured-products",
        "component-fixed-banner",
        "component-fixed-products",
        "component-products-slider",
        "component-photos-slider",
        "component-parallax-background",
        "component-testimonials",
        "component-square-photos",
        "component-store-features",
        "component-youtube",
        "menu-images",
        "filters"
    ],
    
    "settings": [
        {
            "type": "boolean",
            "label": "شريط علوي داكن",
            "id": "topnav_is_dark",
            "format": "switch",
            "selected": false
        }
    ],
    
    "components": [
        {
            "name": "custom-slider",
            "title": "صور متحركة (مخصص)",
            "icon": "sicon-image-carousel",
            "path": "home.custom-slider",
            "fields": [...]
        }
    ]
}
```

---

### 2. master.twig (layouts/master.twig)

The main layout template that all pages extend.

**Key Sections:**
```twig
<!DOCTYPE html>
<html dir="{{ theme.direction }}" lang="{{ lang.code }}">
<head>
    {# Meta tags, title, CSS #}
    {% hook 'head:start' %}
    
    <meta charset="UTF-8">
    <title>{{ page.title() }}</title>
    
    {# Theme CSS #}
    <link rel="stylesheet" href="{{ 'styles.css' | asset }}">
    
    {% hook 'head:end' %}
</head>
<body>
    {% hook 'body:start' %}
    
    {# Header #}
    {% include 'header.twig' %}
    
    {# Main Content #}
    <main>
        {% block content %}{% endblock %}
    </main>
    
    {# Footer #}
    {% include 'footer.twig' %}
    
    {# JavaScript #}
    <script src="{{ 'app.js' | asset }}"></script>
    
    {% hook 'body:end' %}
</body>
</html>
```

---

## Theme Features (Pre-Defined Components)

These are Salla's built-in components that should be used as-is:

### Available Features

1. **component-featured-products** - Showcase selected products
2. **component-fixed-banner** - Static banner area
3. **component-fixed-products** - Fixed product display
4. **component-products-slider** - Sliding product carousel
5. **component-photos-slider** - Image slider
6. **component-parallax-background** - Parallax scroll effect
7. **component-testimonials** - Customer testimonials
8. **component-square-photos** - Square image grid
9. **component-store-features** - Store feature highlights
10. **component-youtube** - YouTube video embed

### Usage

```twig
{# In pages/index.twig #}
{% component 'home' %}
{# This automatically renders all enabled features #}
```

**Best Practice:** Use Theme Features whenever possible for:
- Consistent merchant experience
- Automatic updates from Salla
- Proven, tested functionality

---

## Theme Components (Custom Components)

Components you can modify or create:

### Default Custom Components

1. **brands.twig** - Brand logos display
2. **square-photos.twig** - Enhanced square images
3. **main-links.twig** - Store main navigation links
4. **enhanced-slider.twig** - Advanced slider
5. **products-slider-with-header.twig** - Product slider with title

### Creating Custom Components

**Location:** `src/views/components/home/[component-name].twig`

**Register in twilight.json:**
```json
{
    "components": [
        {
            "name": "my-component",
            "title": "عنصري المخصص",
            "icon": "sicon-image",
            "path": "home.my-component",
            "fields": [
                {
                    "id": "title",
                    "type": "string",
                    "label": "العنوان",
                    "required": true
                }
            ]
        }
    ]
}
```

**Create component file:**
```twig
{# src/views/components/home/my-component.twig #}
<section class="my-component">
    <h2>{{ component.title }}</h2>
    {# Component content #}
</section>
```

---

## Overriding Core Files

### ❌ NEVER Modify Core Files Directly

Do NOT edit:
- `src/views/pages/*.twig` (original page templates)
- Salla's built-in components
- Core Raed structure files

### ✅ Proper Override Methods

#### Method 1: Include Pattern (Recommended)

```twig
{# pages/index.twig #}
{% extends "layouts.master" %}

{% block content %}
    {# Add your custom component #}
    {% include 'components.home.hero' %}
    
    {# Keep original content #}
    {{ parent() }}
{% endblock %}
```

#### Method 2: Component Override

Create new version with different name:
```
src/views/components/product/card-restaurant.twig
```

Use in page:
```twig
{% include 'components.product.card-restaurant' %}
```

#### Method 3: Extend and Modify Blocks

```twig
{# Extend original template #}
{% extends "original-template.twig" %}

{# Override specific block #}
{% block product_info %}
    {# Your custom implementation #}
{% endblock %}
```

---

## Global Variables

Available in all templates:

### Theme Variables

```twig
{{ theme.name }}                # Theme name
{{ theme.direction }}           # rtl or ltr
{{ theme.color.primary }}       # Primary color
{{ theme.color.text }}          # Text color
{{ theme.font.name }}           # Font family name
{{ theme.font.url }}            # Font CSS URL
{{ theme.settings.my_setting }} # Custom setting value
```

### Store Variables

```twig
{{ store.id }}                  # Store ID
{{ store.name }}                # Store name
{{ store.url }}                 # Store URL
{{ store.logo }}                # Store logo
{{ store.currency }}            # Currency code
{{ store.settings.* }}          # Store settings
```

### User Variables

```twig
{{ user.id }}                   # User ID
{{ user.name }}                 # User name
{{ user.email }}                # User email
{{ user.is_logged }}            # Boolean: logged in
```

### Page Variables

```twig
{{ page.title() }}              # Page title
{{ page.type }}                 # Page type
```

### Language Variables

```twig
{{ lang.code }}                 # Language code (ar/en)
{{ trans('key') }}              # Translation
```

---

## Pages Structure

### Home Page (pages/index.twig)

```twig
{% extends "layouts.master" %}

{% block content %}
    {# Renders all theme features & components #}
    {% component 'home' %}
{% endblock %}
```

### Product Page (pages/product.twig)

```twig
{% extends "layouts.master" %}

{% block content %}
    <div class="product-page">
        {# Product Gallery #}
        {% include 'components.product.gallery' %}
        
        {# Product Info #}
        <div class="product-info">
            <h1>{{ product.name }}</h1>
            <div class="price">{{ product.price }}</div>
            
            {# Add to Cart #}
            {% include 'components.product.add-to-cart' %}
        </div>
    </div>
{% endblock %}
```

### Products Listing (pages/products.twig)

```twig
{% extends "layouts.master" %}

{% block content %}
    <div class="products-grid">
        {% for product in products %}
            {% component 'product.card' with {
                product: product
            } %}
        {% endfor %}
    </div>
{% endblock %}
```

---

## Styling Guidelines

### File Organization

```
src/assets/styles/
├── main.scss              # Import all files
├── base/
│   ├── _variables.scss    # CSS variables
│   ├── _reset.scss        # CSS reset
│   └── _typography.scss   # Font styles
├── components/
│   ├── _header.scss
│   ├── _footer.scss
│   └── _buttons.scss
├── pages/
│   ├── _home.scss
│   └── _product.scss
└── sections/
    ├── _hero.scss         # New sections here
    └── _products.scss
```

### Mobile-First Pattern

```scss
// src/assets/styles/sections/_hero.scss

.hero {
    // Mobile (default - 375px+)
    padding: 20px;
    font-size: 24px;
    
    // Tablet (768px+)
    @media (min-width: 768px) {
        padding: 40px;
        font-size: 32px;
    }
    
    // Desktop (1024px+)
    @media (min-width: 1024px) {
        padding: 60px;
        font-size: 48px;
    }
}
```

### Import in main.scss

```scss
// main.scss
@import 'base/variables';
@import 'base/reset';
@import 'base/typography';

@import 'components/header';
@import 'components/footer';

@import 'sections/hero';        // Your new section
@import 'sections/products';

@import 'pages/home';
@import 'pages/product';
```

---

## JavaScript Structure

### File Organization

```
src/assets/js/
├── app.js              # Main entry point
└── partials/
    ├── cart.js         # Cart functionality
    ├── product.js      # Product interactions
    └── wishlist.js     # Wishlist features
```

### app.js Pattern

```javascript
// Import Salla SDK (auto-injected, just use it)

// Import modules
import './partials/cart';
import './partials/product';
import './partials/wishlist';

// App initialization
document.addEventListener('DOMContentLoaded', () => {
    // Your initialization code
    
    // Salla events
    salla.event.cart.onItemAdded((response) => {
        console.log('Item added to cart:', response);
    });
});
```

---

## Development Workflow

### 1. Initial Setup

```bash
# Clone or fork Raed
git clone https://github.com/SallaApp/theme-raed.git my-theme

cd my-theme

# Install dependencies
npm install
```

### 2. Development

```bash
# Run dev server with hot reload
npm run dev
# or
salla theme preview
```

### 3. Build for Production

```bash
# Build optimized assets
npm run build
```

---

## Best Practices

### 1. Use Raed's Patterns

```twig
{# GOOD: Follow Raed structure #}
src/views/components/home/hero.twig
src/assets/styles/sections/_hero.scss

{# AVOID: Random organization #}
src/views/hero-thing.twig
src/assets/hero-styles.css
```

### 2. Extend, Don't Replace

```twig
{# GOOD: Extend and add #}
{% extends "layouts.master" %}
{% block content %}
    {% include 'components.custom.hero' %}
    {{ parent() }}
{% endblock %}

{# AVOID: Complete replacement #}
{% block content %}
    {# Only custom content - loses all Raed features #}
{% endblock %}
```

### 3. Use Theme Features

```twig
{# GOOD: Use built-in features #}
{% component 'home' %}

{# AVOID: Rebuilding from scratch #}
{# Custom implementation of products slider #}
```

### 4. Maintain twilight.json

```json
// GOOD: Clean, organized
{
    "features": [
        "component-featured-products",
        "component-products-slider"
    ],
    "components": [
        {
            "name": "hero",
            "title": "Hero Section",
            ...
        }
    ]
}

// AVOID: Unused features, messy config
```

---

## Common Customization Patterns

### Adding a Hero Section

**1. Create component:**
```twig
{# src/views/components/home/hero.twig #}
<section class="hero" style="background-image: url('{{ component.background }}')">
    <h1>{{ component.title }}</h1>
    <p>{{ component.subtitle }}</p>
</section>
```

**2. Create styles:**
```scss
// src/assets/styles/sections/_hero.scss
.hero {
    min-height: 400px;
    background-size: cover;
    // ...
}
```

**3. Register in twilight.json:**
```json
{
    "components": [
        {
            "name": "hero",
            "title": "Hero Section",
            "icon": "sicon-image",
            "path": "home.hero",
            "fields": [
                {
                    "id": "background",
                    "type": "string",
                    "format": "image"
                },
                {
                    "id": "title",
                    "type": "string"
                }
            ]
        }
    ]
}
```

**4. Import styles:**
```scss
// main.scss
@import 'sections/hero';
```

**5. Use in page (automatic via {% component 'home' %})**

---

### Customizing Product Card

**1. Create override:**
```twig
{# src/views/components/product/card-custom.twig #}
<div class="product-card-custom">
    <img src="{{ product.image }}" alt="{{ product.name }}">
    <h3>{{ product.name }}</h3>
    <div class="price">{{ product.price }}</div>
    <button onclick="salla.cart.addItem({{ product.id }}, 1)">
        Add to Cart
    </button>
</div>
```

**2. Use custom card:**
```twig
{# In products listing #}
{% for product in products %}
    {% include 'components.product.card-custom' with {
        product: product
    } %}
{% endfor %}
```

---

## Preview & Testing

### Using Salla CLI

```bash
# Start preview mode
salla theme preview

# Alias
salla theme p
```

### Using Partners Portal

1. Go to Partners Portal dashboard
2. Select your theme
3. Click "Preview Theme"
4. Choose demo store
5. See live updates

---

## Resources

### Official Links

- **GitHub Repo:** https://github.com/SallaApp/theme-raed
- **Documentation:** https://docs.salla.dev
- **Issue Tracker:** GitHub Issues
- **Community:** Telegram Global Developer Community

### Getting Help

- Report bugs via GitHub Issues
- Ask questions in Telegram community
- Contact: support@salla.sa

---

## Summary

**Raed Template Provides:**
✅ Complete theme structure
✅ Pre-built components
✅ Mobile-first approach
✅ RTL support out of the box
✅ Tailwind CSS integration
✅ Salla SDK integration
✅ Best practices patterns

**Your Job:**
🎯 Extend (don't replace) core files
🎯 Add custom components in proper locations
🎯 Follow mobile-first patterns
🎯 Maintain twilight.json properly
🎯 Use Theme Features when possible
🎯 Test on real Salla stores

---

This is your foundation. Build on Raed, don't fight against it.
