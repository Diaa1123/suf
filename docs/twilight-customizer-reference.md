# Twilight Customizer Reference - twilight.json Guide

## Overview

The `twilight.json` file is the configuration heart of your Salla theme. It defines:
- Theme metadata
- Customizer settings (global controls)
- Theme features (pre-defined components)
- Theme components (custom components)

**Location:** Root directory of theme

---

## File Structure

```json
{
    "version": "1.0.0",
    "theme_name": "My Theme",
    "repository": "https://github.com/user/my-theme",
    "author_email": "developer@example.com",
    "support_url": "https://example.com/support",
    
    "settings": [...],      // Global theme settings
    "features": [...],      // Pre-defined components
    "components": [...]     // Custom components
}
```

---

## Theme Metadata

### Basic Information

```json
{
    "version": "1.0.0",              // Semantic versioning
    "theme_name": "Theme Name",      // Display name
    "repository": "https://...",     // GitHub repo URL
    "author_email": "email@...",     // Support email
    "support_url": "https://..."     // Support website
}
```

---

## Settings (Global Theme Settings)

Settings are global values accessible anywhere in the theme via `{{ theme.settings.setting_id }}`.

### Setting Structure

```json
{
    "type": "string|boolean|number|items",
    "id": "unique_identifier",
    "label": "Display Label (Arabic)",
    "format": "text|switch|dropdown-list|hidden|image|...",
    "selected": "default_value",
    "value": "default_value",
    "required": false,
    "description": "Optional help text"
}
```

### Setting Types

#### 1. Boolean (Switch)

```json
{
    "type": "boolean",
    "id": "dark_mode",
    "label": "الوضع الداكن",
    "format": "switch",
    "selected": false
}
```

**Access in Twig:**
```twig
{% if theme.settings.dark_mode %}
    <body class="dark-theme">
{% endif %}
```

---

#### 2. String (Text Input)

```json
{
    "type": "string",
    "id": "welcome_text",
    "label": "نص الترحيب",
    "format": "text",
    "value": "مرحباً بك",
    "required": false
}
```

**Access in Twig:**
```twig
<h1>{{ theme.settings.welcome_text }}</h1>
```

---

#### 3. String (Textarea)

```json
{
    "type": "string",
    "id": "about_text",
    "label": "نص عن المتجر",
    "format": "textarea",
    "value": "نص طويل..."
}
```

---

#### 4. String (Image Upload)

```json
{
    "type": "string",
    "id": "hero_background",
    "label": "صورة الخلفية",
    "format": "image",
    "value": "images/default-hero.jpg"
}
```

**Access in Twig:**
```twig
<div style="background-image: url('{{ theme.settings.hero_background }}')">
</div>
```

---

#### 5. String (Color Picker)

```json
{
    "type": "string",
    "id": "primary_color",
    "label": "اللون الأساسي",
    "format": "color",
    "value": "#3490dc"
}
```

**Access in Twig:**
```twig
<style>
    :root {
        --primary-color: {{ theme.settings.primary_color }};
    }
</style>
```

---

#### 6. String (URL Input)

```json
{
    "type": "string",
    "id": "custom_link",
    "label": "رابط مخصص",
    "format": "url",
    "inputType": "url",
    "value": "https://example.com"
}
```

---

#### 7. String (Hidden Field)

```json
{
    "type": "string",
    "id": "placeholder_image",
    "format": "hidden",
    "value": "images/placeholder.png"
}
```

Used for internal values not shown to merchant.

---

#### 8. Items (Dropdown List)

```json
{
    "type": "items",
    "id": "layout_style",
    "label": "نمط التصميم",
    "format": "dropdown-list",
    "selected": [
        {
            "id": "grid",
            "value": "Grid",
            "name": "شبكة"
        },
        {
            "id": "list",
            "value": "List",
            "name": "قائمة"
        }
    ]
}
```

**Access in Twig:**
```twig
{% if theme.settings.layout_style == 'grid' %}
    <div class="grid-layout">
{% endif %}
```

---

#### 9. Number (Range Slider)

```json
{
    "type": "number",
    "id": "products_per_row",
    "label": "عدد المنتجات في الصف",
    "format": "range",
    "min": 2,
    "max": 6,
    "step": 1,
    "value": 4,
    "unit": "منتج"
}
```

---

#### 10. Static Content

```json
{
    "type": "static",
    "format": "description",
    "id": "help_note",
    "value": "<div style='padding: 16px; background: #f0f0f0;'>ملاحظة مساعدة</div>"
}
```

Used for help text, images, or HTML content in customizer.

---

## Features (Pre-Defined Components)

Theme Features are Salla's built-in components. Include only those supported by your theme.

### Available Features

```json
{
    "features": [
        "mega-menu",                      // Enhanced navigation
        "fonts",                          // Custom fonts
        "color",                          // Color customization
        "breadcrumb",                     // Breadcrumb navigation
        "unite-cards-height",             // Equal card heights
        "component-featured-products",    // Featured products section
        "component-fixed-banner",         // Fixed banner area
        "component-fixed-products",       // Fixed products display
        "component-products-slider",      // Products carousel
        "component-photos-slider",        // Photo slider
        "component-parallax-background",  // Parallax effect
        "component-testimonials",         // Customer reviews
        "component-square-photos",        // Square photo grid
        "component-store-features",       // Store features list
        "component-youtube",              // YouTube embed
        "menu-images",                    // Menu with images
        "filters"                         // Product filters
    ]
}
```

### Best Practice

✅ **DO:** Include features your theme uses  
❌ **DON'T:** List features you don't support  

Features enable automatic rendering via `{% component 'home' %}`.

---

## Components (Custom Components)

Define your own customizable components for merchants.

### Component Structure

```json
{
    "components": [
        {
            "name": "unique-component-name",
            "title": "Component Display Title",
            "icon": "sicon-icon-name",
            "path": "home.component-file-name",
            "fields": [...]
        }
    ]
}
```

### Component Fields

Fields define what merchants can customize in each component.

---

### Field Types

#### 1. String (Text)

```json
{
    "id": "title",
    "type": "string",
    "label": "العنوان",
    "placeholder": "أدخل العنوان هنا",
    "required": true
}
```

---

#### 2. String (Textarea)

```json
{
    "id": "description",
    "type": "string",
    "format": "textarea",
    "label": "الوصف",
    "placeholder": "أدخل الوصف",
    "required": false
}
```

---

#### 3. String (Image)

```json
{
    "id": "background_image",
    "type": "string",
    "format": "image",
    "label": "صورة الخلفية",
    "required": true
}
```

---

#### 4. String (URL)

```json
{
    "id": "button_link",
    "type": "string",
    "format": "url",
    "label": "رابط الزر",
    "placeholder": "https://example.com",
    "inputType": "url",
    "required": false
}
```

---

#### 5. String (Color)

```json
{
    "id": "text_color",
    "type": "string",
    "format": "color",
    "label": "لون النص",
    "value": "#000000"
}
```

---

#### 6. Boolean (Switch)

```json
{
    "id": "show_title",
    "type": "boolean",
    "text": "إظهار العنوان",
    "format": "switch",
    "selected": true
}
```

---

#### 7. Items (Select/Radio)

```json
{
    "id": "display_style",
    "type": "items",
    "format": "dropdown-list",
    "label": "نمط العرض",
    "selected": [
        {
            "id": "grid",
            "value": "Grid",
            "name": "شبكة"
        },
        {
            "id": "list",
            "value": "List",
            "name": "قائمة"
        }
    ]
}
```

---

#### 8. Collection (Repeatable Fields)

**Most powerful field type** - allows merchants to add multiple items.

```json
{
    "id": "slides",
    "type": "collection",
    "format": "collection",
    "required": true,
    "minLength": 1,
    "maxLength": 10,
    "label": "قائمة الصور",
    "item_label": "صورة",
    "fields": [
        {
            "id": "image",
            "type": "string",
            "format": "image",
            "required": true
        },
        {
            "id": "title",
            "type": "string",
            "label": "العنوان",
            "placeholder": "أدخل العنوان"
        },
        {
            "id": "link",
            "type": "string",
            "format": "url",
            "label": "الرابط",
            "inputType": "url"
        }
    ]
}
```

**Access in Twig:**
```twig
{% for slide in component.slides %}
    <div class="slide">
        <img src="{{ slide.image }}" alt="{{ slide.title }}">
        <h3>{{ slide.title }}</h3>
        <a href="{{ slide.link }}">المزيد</a>
    </div>
{% endfor %}
```

---

#### 9. Number (Range)

```json
{
    "id": "spacing",
    "type": "number",
    "format": "range",
    "label": "المسافة",
    "min": 10,
    "max": 100,
    "step": 5,
    "value": 50,
    "unit": "px"
}
```

---

#### 10. Static (HTML/Help Text)

```json
{
    "type": "static",
    "format": "description",
    "id": "help_text",
    "value": "<div style='background: #fff3cd; padding: 16px;'>تنبيه مهم هنا</div>"
}
```

---

## Complete Component Examples

### Example 1: Hero Section

```json
{
    "name": "hero-section",
    "title": "القسم الرئيسي",
    "icon": "sicon-image",
    "path": "home.hero",
    "fields": [
        {
            "type": "static",
            "format": "description",
            "id": "hero_note",
            "value": "<div style='padding: 16px; background: #e3f2fd;'>القسم الرئيسي يظهر في أعلى الصفحة</div>"
        },
        {
            "id": "background_image",
            "type": "string",
            "format": "image",
            "label": "صورة الخلفية",
            "required": true
        },
        {
            "id": "title",
            "type": "string",
            "label": "العنوان الرئيسي",
            "placeholder": "أدخل العنوان",
            "required": true
        },
        {
            "id": "subtitle",
            "type": "string",
            "format": "textarea",
            "label": "النص الفرعي",
            "placeholder": "أدخل الوصف"
        },
        {
            "id": "button_text",
            "type": "string",
            "label": "نص الزر",
            "placeholder": "اطلب الآن",
            "required": false
        },
        {
            "id": "button_link",
            "type": "string",
            "format": "url",
            "label": "رابط الزر",
            "placeholder": "https://...",
            "inputType": "url"
        },
        {
            "id": "text_color",
            "type": "string",
            "format": "color",
            "label": "لون النص",
            "value": "#ffffff"
        },
        {
            "id": "overlay_opacity",
            "type": "number",
            "format": "range",
            "label": "شفافية الطبقة",
            "min": 0,
            "max": 100,
            "step": 5,
            "value": 50,
            "unit": "%"
        }
    ]
}
```

**Component File (src/views/components/home/hero.twig):**
```twig
<section class="hero" 
         style="background-image: url('{{ component.background_image }}');">
    
    <div class="hero-overlay" 
         style="opacity: {{ component.overlay_opacity / 100 }};"></div>
    
    <div class="hero-content" 
         style="color: {{ component.text_color }};">
        
        <h1>{{ component.title }}</h1>
        
        {% if component.subtitle %}
            <p>{{ component.subtitle }}</p>
        {% endif %}
        
        {% if component.button_text and component.button_link %}
            <a href="{{ component.button_link }}" class="btn">
                {{ component.button_text }}
            </a>
        {% endif %}
    </div>
</section>
```

---

### Example 2: Image Slider with Collection

```json
{
    "name": "custom-slider",
    "title": "صور متحركة",
    "icon": "sicon-image-carousel",
    "path": "home.custom-slider",
    "fields": [
        {
            "id": "is_wide",
            "type": "boolean",
            "text": "عرض كامل",
            "format": "switch",
            "selected": true
        },
        {
            "id": "slides",
            "type": "collection",
            "format": "collection",
            "required": true,
            "minLength": 1,
            "maxLength": 10,
            "label": "قائمة الصور",
            "item_label": "صورة",
            "fields": [
                {
                    "id": "image",
                    "type": "string",
                    "format": "image",
                    "required": true
                },
                {
                    "id": "title",
                    "type": "string",
                    "label": "العنوان",
                    "placeholder": "أدخل العنوان"
                },
                {
                    "id": "description",
                    "type": "string",
                    "format": "textarea",
                    "label": "الوصف"
                },
                {
                    "id": "link",
                    "type": "string",
                    "format": "url",
                    "label": "الرابط",
                    "inputType": "url"
                }
            ]
        }
    ]
}
```

**Component File:**
```twig
<div class="slider {% if component.is_wide %}slider--wide{% endif %}">
    {% for slide in component.slides %}
        <div class="slide">
            <img src="{{ slide.image }}" alt="{{ slide.title }}">
            
            <div class="slide-content">
                {% if slide.title %}
                    <h3>{{ slide.title }}</h3>
                {% endif %}
                
                {% if slide.description %}
                    <p>{{ slide.description }}</p>
                {% endif %}
                
                {% if slide.link %}
                    <a href="{{ slide.link }}" class="slide-link">المزيد</a>
                {% endif %}
            </div>
        </div>
    {% endfor %}
</div>
```

---

### Example 3: Products Display with Options

```json
{
    "name": "products-section",
    "title": "عرض المنتجات",
    "icon": "sicon-box",
    "path": "home.products-section",
    "fields": [
        {
            "id": "section_title",
            "type": "string",
            "label": "عنوان القسم",
            "placeholder": "المنتجات المميزة"
        },
        {
            "id": "layout",
            "type": "items",
            "format": "dropdown-list",
            "label": "نمط العرض",
            "selected": [
                {
                    "id": "grid",
                    "value": "grid",
                    "name": "شبكة"
                },
                {
                    "id": "list",
                    "value": "list",
                    "name": "قائمة"
                },
                {
                    "id": "slider",
                    "value": "slider",
                    "name": "شريط متحرك"
                }
            ]
        },
        {
            "id": "products_per_row",
            "type": "number",
            "format": "range",
            "label": "عدد المنتجات في الصف",
            "min": 2,
            "max": 6,
            "step": 1,
            "value": 4
        },
        {
            "id": "show_description",
            "type": "boolean",
            "text": "إظهار الوصف",
            "format": "switch",
            "selected": true
        }
    ]
}
```

---

## Conditional Fields

Show/hide fields based on other field values.

### Using Conditions

```json
{
    "id": "button_color",
    "type": "string",
    "format": "color",
    "label": "لون الزر",
    "conditions": [
        {
            "setting": "show_button",
            "operator": "==",
            "value": true
        }
    ]
}
```

This field only appears when `show_button` is `true`.

### Available Operators

- `==` - Equals
- `!=` - Not equals
- `>` - Greater than
- `<` - Less than
- `>=` - Greater or equal
- `<=` - Less or equal

### Multiple Conditions

```json
{
    "id": "advanced_option",
    "type": "string",
    "label": "خيار متقدم",
    "conditions": [
        {
            "setting": "enable_advanced",
            "operator": "==",
            "value": true
        },
        {
            "setting": "user_level",
            "operator": "==",
            "value": "expert"
        }
    ]
}
```

All conditions must be true (AND logic).

---

## Access Settings in Theme

### In Twig Templates

```twig
{# Access global settings #}
{{ theme.settings.setting_id }}

{# Access component fields #}
{{ component.field_id }}

{# Check if exists #}
{% if theme.settings.custom_logo %}
    <img src="{{ theme.settings.custom_logo }}">
{% endif %}

{# Loop through collection #}
{% for item in component.items %}
    {{ item.title }}
{% endfor %}
```

### In JavaScript

```javascript
// Get theme setting via Salla SDK
const primaryColor = salla.config.get('theme.settings.primary_color');
```

### In CSS (via Twig)

```twig
<style>
    :root {
        --primary: {{ theme.settings.primary_color }};
        --spacing: {{ theme.settings.spacing }}px;
    }
</style>
```

---

## Best Practices

### 1. Clear Field Labels (Arabic)

```json
// GOOD
{
    "label": "صورة الخلفية الرئيسية",
    "placeholder": "اختر صورة بحجم 1920×800 بكسل"
}

// AVOID
{
    "label": "Image",
    "placeholder": "Upload"
}
```

### 2. Set Sensible Defaults

```json
// GOOD: Default value provided
{
    "id": "hero_height",
    "type": "number",
    "value": 500,
    "min": 300,
    "max": 800
}
```

### 3. Use Help Text

```json
{
    "type": "static",
    "format": "description",
    "value": "<div style='padding: 12px; background: #f0f0f0;'>💡 نصيحة: استخدم صور بحجم 1920×800 للحصول على أفضل نتيجة</div>"
}
```

### 4. Organize with Static Dividers

```json
{
    "type": "static",
    "format": "description",
    "value": "<hr style='margin: 24px 0;'>"
}
```

### 5. Validate Inputs

```json
{
    "id": "email",
    "type": "string",
    "inputType": "email",
    "required": true
}

{
    "id": "website",
    "type": "string",
    "format": "url",
    "inputType": "url"
}
```

### 6. Use Collections for Repeating Data

```json
// GOOD: Using collection
{
    "id": "team_members",
    "type": "collection",
    "fields": [
        {"id": "name", "type": "string"},
        {"id": "photo", "type": "string", "format": "image"}
    ]
}

// AVOID: Multiple individual fields
{
    "id": "member1_name",
    "type": "string"
},
{
    "id": "member2_name",
    "type": "string"
}
```

---

## Icon Reference

Use Salla icons for component icons:

- `sicon-image` - Image/photo
- `sicon-image-carousel` - Slider/carousel
- `sicon-box` - Products/items
- `sicon-layout-grid-rearrange` - Grid/layout
- `sicon-list` - List view
- `sicon-text` - Text content
- `sicon-settings` - Settings/config

Full icon list: https://salla.dev/salla-icons

---

## Validation & Requirements

### Required Fields

```json
{
    "id": "title",
    "type": "string",
    "required": true,
    "label": "العنوان (مطلوب)"
}
```

### Min/Max Length

```json
{
    "id": "slides",
    "type": "collection",
    "minLength": 1,    // At least 1 item
    "maxLength": 10    // Maximum 10 items
}
```

### Range Constraints

```json
{
    "id": "opacity",
    "type": "number",
    "min": 0,
    "max": 100,
    "step": 5
}
```

---

## Testing Your Configuration

### 1. Validate JSON

Use JSON validator to check syntax:
```bash
# Check if valid JSON
cat twilight.json | jq '.'
```

### 2. Preview in Partners Portal

- Push to GitHub
- Open theme in Partners Portal
- Check customizer UI
- Test all fields

### 3. Test in Demo Store

- Preview theme on demo store
- Change all settings
- Verify changes appear correctly

---

## Common Mistakes

### ❌ Wrong Type

```json
// WRONG: Using string for switch
{
    "type": "string",
    "format": "switch"
}

// CORRECT:
{
    "type": "boolean",
    "format": "switch"
}
```

### ❌ Missing Required Fields

```json
// WRONG: No id
{
    "type": "string",
    "label": "Title"
}

// CORRECT:
{
    "id": "title",
    "type": "string",
    "label": "Title"
}
```

### ❌ Invalid Field in Collection

```json
// WRONG: Collection needs 'fields' not 'field'
{
    "type": "collection",
    "field": [...]  // ← Wrong key
}

// CORRECT:
{
    "type": "collection",
    "fields": [...]
}
```

---

## Summary

**twilight.json is your theme's control panel:**

✅ **Metadata:** Version, name, repo  
✅ **Settings:** Global theme controls  
✅ **Features:** Salla's built-in components  
✅ **Components:** Your custom components  

**Key Points:**
- Use clear Arabic labels
- Provide sensible defaults
- Add help text for complex fields
- Use collections for repeating data
- Test thoroughly in Partners Portal

This file makes your theme customizable without code!
