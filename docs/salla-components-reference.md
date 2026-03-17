# Salla Components Reference

## Overview

Salla provides pre-built components that you can use in your themes via Twig. These components handle common functionality and render consistent UI across Salla stores.

---

## Using Salla Components

### Basic Syntax

```twig
{% component 'component.name' %}

{# With parameters #}
{% component 'component.name' with {
    param1: value1,
    param2: value2
} %}
```

---

## Home Components

### {% component 'home' %}

Renders all enabled home page components (features + custom components).

**Usage:**
```twig
{# In pages/index.twig #}
{% component 'home' %}
```

This automatically renders:
- All enabled Theme Features from twilight.json
- All enabled Custom Components from twilight.json
- Components appear in order set in Partners Portal

---

## Product Components

### {% component 'product.card' %}

Renders a product card.

**Parameters:**
- `product` - Product object (required)
- `display` - Display mode: 'grid' | 'list' | 'slider'
- `show_add_btn` - Show add to cart button (boolean)

**Usage:**
```twig
{% for product in products %}
    {% component 'product.card' with {
        product: product,
        display: 'grid'
    } %}
{% endfor %}
```

**Product Object Properties:**
```twig
{{ product.id }}
{{ product.name }}
{{ product.description }}
{{ product.price }}
{{ product.sale_price }}
{{ product.image }}
{{ product.images }}      {# Array of images #}
{{ product.url }}
{{ product.in_stock }}
{{ product.rating }}
```

---

### {% component 'product.add-to-cart' %}

Add to cart button with quantity selector.

**Parameters:**
- `product` - Product object

**Usage:**
```twig
{% component 'product.add-to-cart' with {
    product: product
} %}
```

---

### {% component 'product.gallery' %}

Product image gallery with thumbnails.

**Parameters:**
- `product` - Product object

**Usage:**
```twig
{% component 'product.gallery' with {
    product: product
} %}
```

---

## Cart Components

### {% component 'cart.items' %}

Display cart items list.

**Usage:**
```twig
{% component 'cart.items' %}
```

---

### {% component 'cart.summary' %}

Cart totals and checkout button.

**Usage:**
```twig
{% component 'cart.summary' %}
```

---

## Header/Footer Components

### {% component 'header' %}

Site header with navigation.

**Usage:**
```twig
{% component 'header' %}
```

---

### {% component 'footer' %}

Site footer.

**Usage:**
```twig
{% component 'footer' %}
```

---

## Theme Features (Home Page)

### component-featured-products

Display selected featured products.

**Enable in twilight.json:**
```json
{
    "features": ["component-featured-products"]
}
```

---

### component-products-slider

Products in a slider/carousel.

**Enable in twilight.json:**
```json
{
    "features": ["component-products-slider"]
}
```

---

### component-fixed-banner

Static banner area.

**Enable in twilight.json:**
```json
{
    "features": ["component-fixed-banner"]
}
```

---

### component-photos-slider

Image slider/carousel.

**Enable in twilight.json:**
```json
{
    "features": ["component-photos-slider"]
}
```

---

### component-testimonials

Customer testimonials/reviews.

**Enable in twilight.json:**
```json
{
    "features": ["component-testimonials"]
}
```

---

### component-youtube

Embed YouTube videos.

**Enable in twilight.json:**
```json
{
    "features": ["component-youtube"]
}
```

---

### component-square-photos

Square photo grid.

**Enable in twilight.json:**
```json
{
    "features": ["component-square-photos"]
}
```

---

### component-store-features

Store feature highlights.

**Enable in twilight.json:**
```json
{
    "features": ["component-store-features"]
}
```

---

## Custom Includes

### Your Custom Components

```twig
{# Include your own component #}
{% include 'components.home.hero' %}

{# With variables #}
{% include 'components.home.hero' with {
    title: 'Custom Title'
} %}
```

---

## Component Data Access

### Accessing Component Settings

```twig
{# In custom component file #}
{{ component.field_id }}

{# Example: hero.twig #}
<h1>{{ component.title }}</h1>
<img src="{{ component.background_image }}">
```

### Looping Through Collections

```twig
{# slides is a collection field #}
{% for slide in component.slides %}
    <div class="slide">
        <img src="{{ slide.image }}">
        <h3>{{ slide.title }}</h3>
    </div>
{% endfor %}
```

---

## Best Practices

### 1. Use Salla Components When Available

```twig
{# GOOD: Use built-in #}
{% component 'product.card' with { product: product } %}

{# AVOID: Custom implementation #}
<div class="my-product-card">...</div>
```

### 2. Check Component Availability

```twig
{# Some components may not be available in all contexts #}
{% if product %}
    {% component 'product.card' with { product: product } %}
{% endif %}
```

### 3. Pass Required Parameters

```twig
{# GOOD: All required params #}
{% component 'product.card' with {
    product: product,
    display: 'grid'
} %}

{# AVOID: Missing required params #}
{% component 'product.card' %}
```

---

## Common Patterns

### Product Listing

```twig
<div class="products-grid">
    {% for product in products %}
        {% component 'product.card' with {
            product: product,
            display: 'grid'
        } %}
    {% endfor %}
</div>
```

### Custom Component with Salla Component

```twig
{# custom-products-section.twig #}
<section class="featured-products">
    <h2>{{ component.section_title }}</h2>
    
    <div class="products">
        {% for product in products %}
            {% component 'product.card' with {
                product: product,
                display: component.layout
            } %}
        {% endfor %}
    </div>
</section>
```

---

## Summary

**Salla Components Provide:**
✅ Consistent UI across themes  
✅ Automatic updates and bug fixes  
✅ Tested functionality  
✅ Merchant-familiar interfaces  

**Use Them:**
- For products display
- Cart functionality
- Header/footer
- Common UI patterns

**Build Custom:**
- Unique layouts
- Brand-specific designs
- Specialized features

Always prefer Salla components for standard functionality!
