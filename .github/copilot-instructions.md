# Copilot Instructions for Financial Website

## Project Overview
This is a **single-page financial advisory website** built with Bootstrap 4, jQuery, and SCSS. It's a responsive, template-based site for a financial consulting firm (Pradeep Financial Advisory) featuring multiple content sections managed via anchor navigation.

## Architecture & Key Patterns

### Page Structure
The site uses **section-based navigation** with anchor links. All content sections are defined in `index.html` with consistent ID naming:
- `#home-section` - Hero/landing section
- `#about-section`, `#team-section`, `#services-section` 
- `#pricing-section`, `#faq-section`, `#testimonials-section`
- `#gallery-section`, `#blog-section`, `#contact-section`

The navbar uses `data-spy="scroll"` and `data-target=".site-navbar-target"` for automatic active link highlighting during scroll.

### Build & Compilation
- **Build Tool**: Prepros 6 (preprocessor/asset compiler)
- **SCSS Architecture** (in [scss/](scss/)):
  - `style.scss` - Entry point that imports all modules
  - `_site-base.scss` - Global styles, button/typography resets
  - `_site-navbar.scss` - Navigation and header styling
  - `_site-blocks.scss` - Reusable component blocks (~1800 lines)
  - `bootstrap/` - Bootstrap 4 customization
  
- **Auto-compilation**: Prepros watches SCSS files and outputs to `css/bootstrap.min.css` and `css/style.css`

### JavaScript Patterns
Located in [js/main.js](js/main.js):
- **jQuery-based**: Uses jQuery 3.3.1 for DOM manipulation
- **Class-toggle pattern**: Heavy use of `js-` prefixed classes for JS hooks (e.g., `.js-menu-toggle`, `.js-clone-nav`)
- **Event delegation**: Uses `$('body').on('click', selector)` for delegated event handling
- **Mobile menu**: Offcanvas menu with `.offcanvas-menu` class toggle on body
- **Plugins initialized on ready**:
  - AOS (Animate on Scroll) - `data-aos` attributes trigger animations
  - Owl Carousel - `.nonloop-block-13` wrapper for testimonials/galleries
  - jQuery UI Slider - `#slider-range` for price range filtering
  - Bootstrap datepicker, fancybox, isotope for galleries

## Key Developer Workflows

### Editing Content
1. **Modify HTML** in [index.html](index.html) - All content lives here
2. **Update styles**:
   - Component-specific: Edit `scss/_site-blocks.scss`
   - Global: Edit `scss/_site-base.scss` or `scss/_site-navbar.scss`
   - Prepros auto-compiles to `css/` - check compiled output for errors
3. **Add animations**: Use `data-aos="fade"` or `data-aos="slide"` attributes

### Common Tasks
- **Add new section**: Create `<section id="name-section">` in HTML, add navbar link, Prepros will auto-compile styles
- **Modify colors/spacing**: Adjust Bootstrap variables in `scss/bootstrap/_variables.scss`
- **Add carousel**: Copy `.nonloop-block-13` pattern from testimonials section, update Owl Carousel config in main.js

## Project-Specific Conventions

1. **CSS Naming**: Bootstrap utility classes + custom `.site-*` BEM-style naming
2. **Image Assets**: Stored in `images/` with responsive sizing handled via CSS `background-image` 
3. **Icon System**: Icomoon font icons (defined in `fonts/icomoon/`) - classes like `.icon-facebook`, `.icon-close2`
4. **Mobile Navigation**: Auto-cloned from desktop nav using `js-clone-nav` - maintains sync automatically
5. **Page Loader**: Shows for 1000ms on load, hides via jQuery (no skeleton screens)
6. **Smooth Scroll**: Built-in via Bootstrap `data-spy="scroll"` - links to `#section-id` auto-highlight

## External Dependencies & Integration Points

- **Bootstrap 4**: Used for grid, components, utilities
- **jQuery Plugins**: Owl Carousel (carousels), AOS (scroll animations), jQuery UI (sliders), Fancybox (lightbox)
- **Fonts**: Google Fonts (Open Sans), custom Icomoon + Flaticon icon fonts
- **No build tool required**: Open `index.html` directly in browser - only Prepros needed for SCSS editing
- **Single HTML file**: `index.html` is the main deliverable; `single.html` appears unused

## Important Notes for AI Agents

- **Always preserve anchor navigation structure** - sections must have unique IDs matching navbar links
- **Test responsive behavior** at 768px breakpoint (mobile/desktop switch point)
- **When adding JavaScript**: Use delegation with `$(body).on()` pattern, use `js-` class prefix for hooks
- **When modifying SCSS**: Changes auto-compile via Prepros config - check `prepros-6.config` for file mappings
- **Mobile menu behavior**: Automatically handled by cloning nav; don't duplicate nav structure
- **Data attributes matter**: `data-aos`, `data-spy`, `data-target` are critical to functionality
