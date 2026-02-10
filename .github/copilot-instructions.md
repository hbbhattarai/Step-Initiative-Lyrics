# Step Initiative - Copilot Instructions

## Project Overview
**Step Initiative** is a static website showcasing global music collections across Nepali, Dzongkha, and English languages with song lyrics and cultural context. No backend or build system—pure HTML/CSS/JavaScript served as static files.

## Architecture Essentials

### File Structure
```
/workspaces/Step-Initiative---Lyrics-/
├── index.html              # Landing page with all song cards/sections
├── README.md               # Project overview
├── logo.png                # Branding asset
└── {Language}/             # Language folders (Nepali/, Dzongkha/, English/)
    └── {songN}.html        # Individual song lyric pages
```

### Key Design Patterns

**Landing Page (index.html):**
- Single-page with three language sections (`#nepali`, `#dzongkha`, `#english`)
- Music grid cards linking to language-specific folders
- Nav links use anchor navigation with smooth scroll behavior
- CSS variables define language-specific colors: `--nepali-color`, `--dzongkha-color`, `--english-color`

**Song Lyric Pages (e.g., Nepali/song1.html):**
- Centered content container with decorative gradient elements
- Verses wrapped in `.verse` divs with numbered badges
- Chorus sections use `.verse.chorus` class (different background)
- Music notes (`♪ ♫`) separate verses and mark interludes
- JavaScript: Copy-to-clipboard and print functionality
- Color scheme matches landing page (pink/coral for Nepali)

## Critical Developer Patterns

### CSS Architecture
- **No external stylesheets**—all styles in `<style>` tags within each HTML file
- **Inline gradient backgrounds** for visual hierarchy (e.g., `background: linear-gradient(135deg, #e84118, #c23616)`)
- **CSS variables** for reusable colors (see `:root` in index.html)
- **Flexbox + Grid** for responsive layouts (prefer `grid-template-columns: repeat(auto-fill, minmax(...))`for cards)
- **Semantic color naming**: `-color` suffix for language themes (`.nepali-icon`, `.nepali-btn`, `.nepali-badge`)

### JavaScript Interactions
- Vanilla JS only—no frameworks
- **Smooth scroll navigation** on nav link clicks (view `DOMContentLoaded` handler in index.html)
- **Intersection Observer** for fade-in animations on scroll (cards and sections)
- **Event delegation patterns** (e.g., querySelectorAll + forEach for button handlers)
- Dynamic class toggling for active states (`.nav-link.active`)

### Typography & Spacing
- **Font stack**: `'Segoe UI', Tahoma, Geneva, Verdana` (body); `'Georgia', serif` for verse content
- **Responsive font sizes** via media queries (e.g., h1: 3.5rem → 2.2rem on mobile)
- **Line-height: 1.8** for lyrics (readability)
- **white-space: pre-line** for verse formatting (preserves line breaks)

## Adding New Content

### New Language Section
1. Add to landing page index.html:
   - New `language-section` div with unique `id` (e.g., `id="burmese"`)
   - Update `:root` with `--burmese-color`, `--burmese-accent`
   - Create `.burmese-header`, `.burmese-icon`, `.burmese-badge`, `.burmese-btn` classes (copy from Nepali pattern)
   - Add nav link `<a href="#burmese">`

2. Create folder: `Burmese/`
3. Add song pages: `Burmese/song1.html` (use Nepali/song1.html as template, update colors/content)

### New Song Page
1. Copy existing song HTML (Nepali/song1.html is template)
2. Update title, subtitle, artist metadata in header
3. Add verse divs with `.verse-content` preserving formatting
4. Mark chorus with `.verse.chorus` class
5. Link from landing page card: `<a href="Nepali/song2.html">`

## Common Workflows

**Updating Landing Page Colors/Layout:**
- Edit `:root` variables for language colors
- Card styling in `.music-grid` and `.music-card` classes
- Test responsive breakpoints (`@media max-width: 768px, 992px, 1200px, 480px`)

**Adding Interactive Features:**
- Use vanilla JS event listeners (see DOMContentLoaded pattern)
- Avoid modifying HTML structure in JS—only class/style changes
- Use `navigator.clipboard.writeText()` for copy operations (tested pattern in song pages)

**Responsive Design Priority:**
- Mobile-first: test on 480px, 768px, 992px, 1200px breakpoints
- Cards stack to single column on mobile (`grid-template-columns: 1fr`)
- Navigation moves to column layout below 992px

## Known Conventions

- **Active nav state**: `.nav-link.active` (updated via scroll event)
- **Animations**: `float`, `pulse`, `animate` keyframes (4-6s duration, ease-in-out)
- **Decorative elements**: Absolute-positioned gradient circles with animation delays (`.bg-element-*`)
- **No external APIs** – all content is static
- **Emoji/Icons**: Font Awesome (v6.4.0) via CDN for music notes, hearts, flags
- **Print styles**: Button onclick `window.print()` triggers browser print (inherits page styles)

## Quick Reference: When Adding Features

| Task | Location | Example |
|------|----------|---------|
| Change language color | `.root` variables in index.html | `--nepali-color: #e84118` |
| Update homepage cards | `.music-grid`, `.music-card` styles | Adjust `minmax(320px, 1fr)` |
| New song page template | Copy `Nepali/song1.html` | Update `.verse-number` and `.verse-content` |
| Add nav section | `nav-links` and `language-section` divs | Follow language-specific class naming |
| Fix mobile layout | Media queries in `<style>` tags | Update breakpoints for flex/grid changes |

## Testing Checklist
- [ ] Responsive: test on 480px, 768px, 992px widths
- [ ] Navigation: all anchor links scroll smoothly, active state updates
- [ ] Print: Print button outputs readable lyrics without decoration overflow
- [ ] Copy: Clipboard copy preserves formatting, shows success feedback
- [ ] Animations: Elements fade in on scroll, hover effects work smoothly
