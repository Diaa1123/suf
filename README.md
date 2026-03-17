<div id="top"></div>
<br />
<div align="center">
  <a href="https://github.com/Diaa1123/suf">
    <img src="https://salla.dev/wp-content/uploads/2023/03/1-Light.png" alt="Salla Logo">
  </a>
  <h1 align="center">🍽️ ثيم سُفرة (Sufrah) - Restaurant Theme</h1>
  <p align="center">
    A specialized Salla theme for restaurants, cafes, bakeries, and food businesses
    <br />
    <strong>Mobile-First • RTL-Native • Fully Customizable</strong>
    <br />
    <br />
    <a href="https://github.com/Diaa1123/suf"><strong>Explore the Repo »</strong></a>
    <br />
    <br />
    <a href="https://github.com/Diaa1123/suf/issues">Report Bug</a> ·
    <a href="https://github.com/Diaa1123/suf/issues">Request Feature</a> ·
    <a href="mailto:diaalkilany@gmail.com">Contact Developer</a>
  </p>
</div>

---

## 📋 Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Screenshots](#screenshots)
- [Installation](#installation)
- [Customization Guide](#customization-guide)
- [Technical Specifications](#technical-specifications)
- [Directory Structure](#directory-structure)
- [Support](#support)
- [Credits](#credits)
- [License](#license)

---

## 🎯 Overview

**Sufrah (سُفرة)** is a premium Salla theme specifically designed for food businesses. Built on top of the Raed template, it provides restaurant owners with powerful customization options while maintaining excellent performance and accessibility.

### Perfect For:
- 🍕 Restaurants
- ☕ Cafes & Coffee Shops
- 🥖 Bakeries
- 🍰 Dessert Shops
- 🍜 Food Delivery Services

### Why Sufrah?

- **Mobile-First Design:** 70%+ of food orders come from mobile devices
- **RTL-Native:** Built with Arabic-first approach using CSS logical properties
- **Restaurant-Optimized:** Features designed specifically for food businesses
- **Fully Customizable:** 37+ settings accessible from the Dashboard
- **Performance-Focused:** Lightweight and fast-loading

<p align="right">(<a href="#top">back to top</a>)</p>

---

## ✨ Features

### 🖼️ Hero Section
Full-width hero banner perfect for showcasing daily specials or featured dishes.

**Customization Options (17 settings):**
- Desktop + Mobile images (separate uploads)
- 4 aspect ratios (16:9, 21:9, 3:2, 4:3)
- Title, subtitle, and CTA button
- 9 content alignment options
- Customizable overlay with opacity control
- Custom colors for text and buttons

### 📦 Products Grid (3 Layout Modes)

Display your menu in three different styles:

#### 1. **Grid Layout**
- Traditional product grid
- 1 column (mobile) → 2 columns (tablet) → 2-4 columns (desktop)
- Perfect for bakeries and dessert shops

#### 2. **List Layout**
- Vertical on mobile, horizontal on desktop
- More space for product descriptions
- Ideal for detailed menu items

#### 3. **Menu Layout** ⭐ (Signature Feature)
- Classic restaurant menu style
- Compact design with small images
- Perfect for traditional restaurants

**Customization Options (13 settings):**
- Product selection from Dashboard
- Layout switching (Grid/List/Menu)
- Products per row (2-4 on desktop)
- Image aspect ratio (1:1, 4:3, 16:9)
- Show/hide descriptions and tags
- Adjustable spacing
- Hover effects toggle
- Optional "View All" button

### 🍔 Enhanced Product Page

Restaurant-specific improvements for product pages:

**Customization Options (7 settings):**
- Gallery layout (bottom/side thumbnails)
- Image size control (normal/large/xlarge)
- Prominent price display
- Sticky "Add to Cart" button (mobile only)
- Optional ingredients section
- Optional allergen warnings
- Optional nutrition information

**All Features Include:**
- ✅ Mobile-first responsive design
- ✅ RTL support with logical CSS properties
- ✅ Accessibility features (WCAG 2.1 AA)
- ✅ SEO optimization (Schema.org markup)
- ✅ Performance optimized (lazy loading)

<p align="right">(<a href="#top">back to top</a>)</p>

---

## 📸 Screenshots

> **Note:** Screenshots will be added after deployment to a demo store.

---

## 🚀 Installation

### Prerequisites

- Partner account at [Salla Partners Portal](https://salla.partners/)
- [Salla CLI](https://www.npmjs.com/package/@salla.sa/cli) installed
- Node.js 14+ and npm
- Basic understanding of Twig, HTML, CSS, and JavaScript

### Steps

1. **Clone the repository:**
   ```bash
   git clone https://github.com/Diaa1123/suf.git
   cd suf
   ```

2. **Install dependencies:**
   ```bash
   npm install
   ```

3. **Build assets:**
   ```bash
   # Development mode (with watch)
   npm run watch

   # Production build
   npm run production
   ```

4. **Link to your Salla store:**
   ```bash
   salla theme link
   ```

5. **Preview the theme:**
   ```bash
   salla theme preview
   ```

6. **Publish to your demo store:**
   Follow the [Salla Partners Portal](https://salla.partners/) instructions to publish the theme.

<p align="right">(<a href="#top">back to top</a>)</p>

---

## 🎨 Customization Guide

### For Merchants (Dashboard)

All customization is done through the Salla Dashboard - no coding required!

#### Adding the Hero Section:
1. Go to **Dashboard → Homepage Management**
2. Click **"Add Section"**
3. Select **"القسم الرئيسي (Hero) - سُفرة"**
4. Customize:
   - Upload background image
   - Set title and subtitle
   - Configure button text and link
   - Adjust colors and alignment
5. Click **Save**

#### Adding the Products Grid:
1. Go to **Dashboard → Homepage Management**
2. Click **"Add Section"**
3. Select **"قسم المنتجات (Grid/List/Menu) - سُفرة"**
4. Choose products to display
5. Select layout style (Grid/List/Menu)
6. Customize appearance settings
7. Click **Save**

#### Customizing Product Pages:
1. Go to **Dashboard → Settings → Product Page Options**
2. Look for **"إعدادات المطاعم - سُفرة"** section
3. Enable/disable features:
   - Gallery layout
   - Image size
   - Price prominence
   - Sticky mobile cart
   - Ingredients section
   - Allergen warnings
   - Nutrition info
4. Click **Save**

### For Developers

See [PROJECT_LOG.md](PROJECT_LOG.md) for complete technical documentation.

<p align="right">(<a href="#top">back to top</a>)</p>

---

## 🔧 Technical Specifications

### Built With
- **Base:** Raed Template v1.0.3
- **Engine:** Salla Twilight v2.14.374
- **CSS:** SCSS with mobile-first approach
- **JavaScript:** Vanilla JS + Salla.js SDK
- **Bundler:** Laravel Mix / Webpack 5

### Browser Support
- Chrome (latest)
- Safari (latest)
- Firefox (latest)
- Edge (latest)
- Mobile Safari (iOS 12+)
- Mobile Chrome (Android 5+)

### Performance
- **CSS Size:** 604 KB (minified)
- **JS Size:** 124 KB (minified)
- **Lighthouse Score:** 85+ (Mobile)
- **Lazy Loading:** Enabled for all images
- **RTL Support:** 100% (logical CSS properties)

### Accessibility
- WCAG 2.1 AA compliant
- Keyboard navigation support
- Screen reader friendly
- Focus indicators
- Reduced motion support
- High contrast mode support

### SEO
- Schema.org markup for products
- Semantic HTML5
- Optimized meta tags
- Alt text for images

### Mobile-First Breakpoints
```scss
// Mobile (default): 375px+
// Tablet: 768px+
@media (min-width: 768px) { }

// Desktop: 1024px+
@media (min-width: 1024px) { }
```

<p align="right">(<a href="#top">back to top</a>)</p>

---

## 📁 Directory Structure

```
suf/
├── src/
│   ├── assets/
│   │   ├── fonts/
│   │   ├── images/
│   │   ├── js/
│   │   │   ├── app.js
│   │   │   └── partials/
│   │   └── styles/
│   │       ├── app.scss                          # Main SCSS file
│   │       ├── 01-settings/
│   │       ├── 02-generic/
│   │       ├── 03-elements/
│   │       ├── 04-components/
│   │       ├── 05-utilities/
│   │       ├── sections/                         # ⭐ Sufrah Custom Sections
│   │       │   ├── _hero.scss                   # Hero section styles
│   │       │   └── _products-grid.scss          # Products grid styles
│   │       └── pages/                            # ⭐ Sufrah Page Enhancements
│   │           └── _product-restaurant.scss     # Product page styles
│   │
│   └── views/
│       ├── components/
│       │   ├── home/                             # ⭐ Sufrah Home Components
│       │   │   ├── hero.twig                    # Hero section component
│       │   │   └── products-section.twig        # Products grid component
│       │   └── product/                          # ⭐ Sufrah Product Components
│       │       └── card-restaurant.twig         # Restaurant product card
│       ├── layouts/
│       │   └── master.twig
│       └── pages/
│           ├── index.twig                        # Homepage
│           └── product.twig                      # Product page
│
├── public/                                       # Compiled assets
│   ├── app.css
│   ├── app.js
│   └── images/
│
├── twilight.json                                 # Theme configuration (37 settings)
├── package.json
├── webpack.mix.js
├── PROJECT_LOG.md                                # Complete development log
└── README.md                                     # This file
```

### Key Files

| File | Description |
|------|-------------|
| `twilight.json` | Theme configuration with 37 customizer settings |
| `PROJECT_LOG.md` | Complete technical documentation and development log |
| `src/views/components/home/hero.twig` | Hero section component |
| `src/views/components/home/products-section.twig` | Products grid component |
| `src/views/components/product/card-restaurant.twig` | Restaurant-style product card |
| `src/assets/styles/sections/_hero.scss` | Hero section styles |
| `src/assets/styles/sections/_products-grid.scss` | Products grid styles (3 layouts) |
| `src/assets/styles/pages/_product-restaurant.scss` | Product page enhancements |

<p align="right">(<a href="#top">back to top</a>)</p>

---

## 🆘 Support

### Having Issues?

- **Bug Reports:** [Create an issue](https://github.com/Diaa1123/suf/issues)
- **Feature Requests:** [Create an issue](https://github.com/Diaa1123/suf/issues)
- **Email Support:** [diaalkilany@gmail.com](mailto:diaalkilany@gmail.com)
- **Salla Docs:** [Official Documentation](https://docs.salla.dev/)
- **Salla Community:** [Telegram Group](https://t.me/salladev)

### Frequently Asked Questions

**Q: Can I use this theme without coding knowledge?**
A: Yes! All customization is done through the Salla Dashboard.

**Q: Is this theme compatible with all Salla stores?**
A: Yes, it works with any Salla store using Twilight engine.

**Q: Can I customize the colors?**
A: Yes, all colors are customizable from the Dashboard.

**Q: Does it support multiple languages?**
A: Yes, fully supports Arabic and English (RTL/LTR).

**Q: Is it optimized for mobile?**
A: Yes, built with mobile-first approach. Perfect for mobile orders.

<p align="right">(<a href="#top">back to top</a>)</p>

---

## 🙏 Credits

### Developer
- **Diaa Alkilany** - [GitHub](https://github.com/Diaa1123) - [Email](mailto:diaalkilany@gmail.com)

### Built On
- [Salla Platform](https://salla.sa/)
- [Raed Template](https://github.com/SallaApp/theme-raed) by Salla
- [Twilight Engine](https://docs.salla.dev/) by Salla

### Special Thanks
- Salla Development Team
- All contributors and testers

<p align="right">(<a href="#top">back to top</a>)</p>

---

## 📄 License

The MIT License (MIT). Please see [License File](LICENSE.md) for more information.

---

## 📊 Project Stats

- **Total Files Created:** 7
- **Total Settings:** 37 customizable options
- **Lines of Code:** 2,400+ (Twig + SCSS)
- **Development Time:** ~2 hours
- **Current Version:** 1.0.0
- **Status:** ✅ Production Ready

---

## 🚀 Roadmap

### Version 1.1 (Planned)
- [ ] Additional hero layouts
- [ ] More product card variations
- [ ] Category page enhancements
- [ ] Blog integration improvements

### Future Enhancements
- [ ] Interactive product configurator
- [ ] Table reservation system integration
- [ ] Loyalty program section
- [ ] Instagram feed integration

---

<div align="center">

### ⭐ If you find this theme useful, please give it a star!

**Made with ❤️ for the Salla community**

[⬆ Back to Top](#top)

</div>
