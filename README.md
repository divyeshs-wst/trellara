# Trellara — Starter Theme Skeleton

Foundation files for the **Trellara** custom Shopify theme, built by Wisdom Square Technologies.

## What's included

```
trellara/
├── layout/
│   └── theme.liquid              → Main HTML shell, loads engine CSS + theme CSS/JS
├── config/
│   ├── settings_schema.json      → Global theme settings (colors, fonts, layout width)
│   └── settings_data.json        → Default values for the above
├── assets/
│   └── trl-engine.css            → Core CSS custom properties (colors, spacing, radius, shadows)
├── snippets/
│   ├── trl-global-settings.liquid → Shared wrapper renderer (Class, ID, Display, Size,
│   │                                Spacing, Background, Border, Custom CSS)
│   └── trl-global-schema.txt     → Copy-paste schema block for the settings above —
│                                    paste into every widget's schema "settings" array
│                                    (kept as .txt, not .json, since it has comments in it
│                                    and is never loaded directly by Shopify)
├── blocks/
│   └── trl-button.liquid         → First working widget, shows the full pattern in use
├── sections/
│   ├── header-group.json         → Section group referenced by theme.liquid
│   ├── footer-group.json         → Section group referenced by theme.liquid
│   ├── trl-header.liquid         → Basic header (logo, menu, search/account/cart icons)
│   ├── trl-footer.liquid         → Basic footer (text, menu, copyright)
│   ├── trl-hero.liquid           → Homepage hero banner
│   ├── trl-404.liquid            → 404 page content
│   ├── trl-page.liquid           → Standard page template content
│   ├── trl-product.liquid        → Basic product page (image, price, variant picker, add to cart)
│   ├── trl-collection.liquid     → Basic product grid with pagination
│   ├── trl-cart.liquid           → Cart table with update/checkout
│   └── trl-search.liquid         → Search form + results
└── templates/
    ├── index.json                → Homepage (uses trl-hero)
    ├── 404.json                  → 404 page (uses trl-404)
    ├── page.json                 → Standard pages (uses trl-page)
    ├── product.json              → Product page (uses trl-product)
    ├── collection.json           → Collection page (uses trl-collection)
    ├── cart.json                 → Cart page (uses trl-cart)
    └── search.json               → Search page (uses trl-search)
```

## How the pattern works (per our earlier discussion)

Every widget has **two layers**:

1. **Widget-specific Style** — lives directly in the widget's own `{% schema %}` and Liquid markup (e.g. Button's label color, hover color). This is unique per widget.
2. **Global Wrapper Settings** — Class, ID, Display, Size, Spacing, Background, Border, Custom CSS. Built ONCE in `trl-global-settings.liquid` + `trl-global-schema.json`, reused by every widget.

**To build a new widget:**
1. Copy `blocks/trl-button.liquid` as a starting template.
2. Replace the widget-specific settings/markup with your own (Section 1–7 categories from our reference doc).
3. Copy the contents of `snippets/trl-global-schema.json` into the widget's own `settings` array (marked with a comment in `trl-button.liquid` showing where).
4. Wrap your widget's captured content through `{% render 'trl-global-settings', block: block, content: widget_content %}` — same as Button does.

## Naming convention (locked in per our discussion)

```
--trl-{scope}-{property}-{state}
```
Examples: `--trl-button-bg-hover`, `--trl-wrapper-bg`, `--trl-icon-color`

Keeping wrapper-level and content-level variables distinctly named (`--trl-wrapper-bg` vs `--trl-button-bg`) avoids the kind of variable collision that caused the earlier margin left/right swap bug.

## Status: now viewable in the Shopify editor

All previously-missing required pieces are now included: `trl-theme.css`/`trl-theme.js`, both section groups, basic header/footer/hero/404/page/product/collection/cart/search sections, all required templates, and a starter locale file. Re-upload this version and every page (Home, 404, product, collection, cart, search, and regular pages) should now render and show sections in the editor instead of the "this page doesn't have any sections" message.

## Still needed before this is a real, uploadable Theme Store submission

- [ ] Core structural widgets: Section/Container, Columns/Grid, Spacer (so the ~50-widget library can actually be dropped into these page templates)
- [ ] Replace placeholder header/footer/hero styling with real design system values
- [ ] Expand `locales/en.default.json` — current version is a minimal starter, not full translation coverage
- [ ] Run `theme-check` CLI before any Theme Store submission
- [ ] Add remaining widgets from the reference doc, following the Button pattern

## Build order (recap)
Phase 1 (this skeleton) → Phase 2 (Section/Columns/Spacer) → Phase 3 (one widget per pattern: text-only, icon+text, image+text, repeater, store-data) → Phase 4 (remaining ~45 widgets in groups) → Phase 5 (header/footer/cart/product/collection pages) → Phase 6 (Theme Store requirements).
