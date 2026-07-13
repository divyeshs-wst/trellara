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
│   └── trl-global-schema.json    → Copy-paste schema block for the settings above —
│                                    paste into every widget's schema "settings" array
├── blocks/
│   └── trl-button.liquid         → First working widget, shows the full pattern in use
├── sections/                     → (empty — build Section/Container widget next)
└── templates/                    → (empty — required by Shopify, add as you build pages)
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

## Still needed before this is a real, uploadable theme

- [ ] `assets/trl-theme.css` and `assets/trl-theme.js` (referenced in `theme.liquid`, not yet created)
- [ ] `sections/header-group.json` and `sections/footer-group.json` (section groups referenced in `theme.liquid`)
- [ ] Core structural widgets: Section/Container, Columns/Grid, Spacer
- [ ] Required Shopify templates: `templates/index.json`, `templates/product.json`, `templates/collection.json`, `templates/cart.json`, `templates/404.json`, `templates/page.json`, `templates/search.json`
- [ ] `locales/en.default.json` for translations
- [ ] Run `theme-check` CLI before any Theme Store submission

## Build order (recap)
Phase 1 (this skeleton) → Phase 2 (Section/Columns/Spacer) → Phase 3 (one widget per pattern: text-only, icon+text, image+text, repeater, store-data) → Phase 4 (remaining ~45 widgets in groups) → Phase 5 (header/footer/cart/product/collection pages) → Phase 6 (Theme Store requirements).
