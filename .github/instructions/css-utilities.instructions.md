---
description: CSS utility classes and styling practices for this Blazor project — Minecraft Theme.
---

# ⛏️ CSS Styling Practices — Minecraft Edition

## Overview
This project uses a **Minecraft-themed** custom CSS design system defined in `wwwroot/css/app.css`. All utilities are pixel-art inspired, using blocky borders, embossed 3D panels, and Minecraft color palettes. Typography uses **VT323** (pixel font) and **Silkscreen** (headings) from Google Fonts.

## Design Principles

1. **No rounded corners** — Minecraft is blocky. All `border-radius` is `0px`
2. **3D embossed borders** — Light top-left, dark bottom-right simulates 3D blocks
3. **Pixel-perfect fonts** — `VT323` for body text, `Silkscreen` for headings
4. **Minecraft color palette** — Dirt browns, grass greens, stone grays, gold/diamond accents
5. **Step-based transitions** — Use `steps()` timing instead of smooth easing

## CSS Variables (`:root`)

### Block Colors
```css
--mc-dirt, --mc-dirt-dark, --mc-dirt-light     /* Earth tones */
--mc-stone, --mc-stone-dark, --mc-stone-light  /* Stone grays */
--mc-grass, --mc-grass-dark, --mc-grass-light  /* Creeper green */
--mc-oak, --mc-oak-dark, --mc-oak-light        /* Wood tones */
--mc-darkoak, --mc-obsidian                     /* Dark blocks */
```

### Special Colors
```css
--mc-sky, --mc-water         /* Sky blue, water blue */
--mc-lava, --mc-redstone     /* Lava orange, redstone red */
--mc-gold, --mc-xp-green     /* Gold yellow, XP bar green */
--mc-diamond                  /* Diamond cyan */
```

### UI Panel
```css
--mc-panel-bg       /* #C6C6C6 — Inventory panel gray */
--mc-panel-border   /* #373737 — Dark border */
--mc-panel-light    /* #FFFFFF — Light 3D edge */
--mc-panel-dark     /* #555555 — Dark 3D edge */
```

## Available Utilities

### Layout
```css
.flex, .flex-col, .flex-1
.grid, .grid-cols-5
.items-center, .justify-center, .justify-between
```

### Spacing
```css
.p-1 through .p-6, .px-*, .py-*
.mb-2 through .mb-8, .mx-auto
.gap-1, .space-y-2
```

### Sizing
```css
.h-full, .w-full, .min-h-full
.max-w-xs, .max-w-sm, .max-w-md
.aspect-square
```

### Minecraft Colors (mapped from Tailwind names)
```css
.bg-white    → Panel gray (#C6C6C6)
.bg-gray-50  → Dirt with grass-top gradient
.bg-gray-100 → Stone gray
.bg-accent   → Grass green (primary action)
.bg-marked   → XP green (selected/marked)
.bg-amber-*  → Gold tones (winning/special)

.text-gray-* → Stone shade range
.text-green-* → Grass/creeper shades
.text-amber-* → Gold/oak shades
```

### Typography
```css
.text-xs through .text-5xl  /* Pixel-scaled sizes */
.font-semibold, .font-bold  /* Both use weight: 700 */
.text-center, .text-left

/* Font stacks: */
body     → 'VT323', 'Courier New', monospace
headings → 'Silkscreen', 'VT323', monospace
```

### Borders & Shadows (3D Embossed)
```css
.border, .border-b           /* 3px solid borders */
.rounded, .rounded-lg, .rounded-xl  /* ALL = 0px (blocky!) */
.shadow-sm → inset 3D panel effect
.shadow-xl → inset 3D panel + drop shadow
```

### Animation
```css
.transition-all       /* steps(3, end) timing */
.transition-colors    /* steps(3, end) timing */
.duration-150         /* 100ms duration */
.animate-[bounce_0.5s_ease-out]  /* Blocky step bounce */
```

### Special Effects
```css
/* Enchantment glow animation (winning bingo squares) */
@keyframes mc-enchant-glow { ... }

/* Enchanted text shimmer (BINGO indicator) */
@keyframes mc-enchant-text { ... }
```

## Button Styles

Buttons automatically receive the Minecraft 3D embossed look:

| State    | Appearance                              |
|----------|-----------------------------------------|
| Default  | Stone panel with light/dark borders     |
| Hover    | Lighter stone, gold text                |
| Active   | Pressed-in (inverted borders), shifts 1px |
| Disabled | Dimmed stone, gray text                 |

**Accent buttons** (`.bg-accent`) use grass green with emerald borders.

## Best Practices

1. **Compose utilities**: Combine classes for complex layouts
2. **Use CSS variables**: Reference `--mc-*` variables for consistent theming
3. **No border-radius**: Keep everything blocky — this is Minecraft!
4. **Pixel fonts only**: Never use sans-serif or serif fonts
5. **3D borders**: Always use light-top/dark-bottom border colors for depth
6. **Step transitions**: Use `steps()` timing for that pixelated animation feel

## Example Component Styling
```razor
<div class="flex flex-col items-center justify-center min-h-full bg-gray-50">
    <button class="w-full bg-accent text-white font-semibold py-4 px-8 text-lg">
        Start Game
    </button>
</div>
```

## File Structure
- `wwwroot/css/app.css` — Main Minecraft theme + utility classes
- `Layout/MainLayout.razor.css` — Dark oak sidebar, stone toolbar
- `Layout/NavMenu.razor.css` — Inventory-slot navigation with pixel icons