## Why

The current AI-Assisted Engineering website has several UX issues that reduce its professional polish: cramped section spacing, inconsistent visual hierarchy, text-heavy expert cards, and overwhelming video grids. These issues diminish the premium "tech forward" impression the site should convey.

**Design Direction:** Elevate the existing dark theme into a **futuristic HUD / Sci-Fi FUI aesthetic**—professional, expensive-looking, with subtle neon glow effects and technical visual elements that reinforce the AI/tech positioning.

## What Changes

### Design System Enhancements

#### Visual Style: HUD / Sci-Fi FUI
- Thin glowing borders on cards and key elements
- Subtle scanline overlays on hero section
- Corner bracket decorations (FUI-style) on featured cards
- Pulse animations for status indicators
- Neon cyan/magenta accents complementing existing purple gradient

#### Color Palette Additions
```css
/* HUD Accent Colors (complement existing --color-primary: #667eea) */
--hud-cyan: #00FFFF;           /* Primary HUD accent */
--hud-magenta: #FF00FF;        /* Secondary/alert accent */
--hud-green: #00FF00;          /* Status indicators */
--hud-amber: #FFAA00;          /* Warning states */

/* Glow Effects */
--glow-cyan: 0 0 10px rgba(0, 255, 255, 0.5), 0 0 20px rgba(0, 255, 255, 0.3);
--glow-primary: 0 0 10px rgba(102, 126, 234, 0.5), 0 0 20px rgba(102, 126, 234, 0.3);
```

#### Typography Enhancement
- **Option A (Recommended):** Add `Orbitron` for headlines only, keep `Inter` for body text
- **Option B:** Full monospace with `Share Tech Mono` (headlines) + `Fira Code` (body)
- Headlines get subtle text-shadow glow effect

### Global Improvements

- Increase section padding from ~60-80px to 120px for better visual breathing room
- Add HUD-style card hover states (lift + neon border glow + shadow)
- Ensure all backgrounds use dark theme palette (no white backgrounds)
- Establish clear typography hierarchy (h1: 4rem → h2: 2.5rem → h3: 1.5rem → h4: 1.125rem)
- Replace emoji icons with SVG icons (Lucide/Heroicons)

### Section-Specific Changes

- **Hero**:
  - Add pill badge with glow effect
  - Larger headlines with optional Orbitron font
  - Enhanced CTA buttons with neon hover glow
  - Code block with scanlines overlay + pulsing status indicator
  - Subtle radial gradient background enhancement

- **Why AI Stats**:
  - Gradient numbers with neon glow text-shadow
  - Animated count-up on scroll
  - HUD-style card borders with corner brackets

- **Tutorials**:
  - Limit video grid to 6 items max
  - Add "View all tutorials" link
  - Glowing play button on hover

- **Events**:
  - Center layout for 2-card view
  - Enhanced date badges with HUD styling
  - Animated top border on hover (scale from left)

- **Experts**:
  - Simplify cards with shorter bios (2-line limit)
  - Social icon links with glow hover
  - "Watch their talks" CTA
  - Gradient ring around profile photos

- **Master the Tools**:
  - Replace emoji icons with SVG icons
  - Unify into consistent feature grid with mini-stats row
  - HUD-style icon containers with subtle glow

### Micro-interactions & Effects

- Smooth hover transitions (150-300ms) on all interactive elements
- Scroll-triggered fade-in-up animations for sections
- Code block status indicator with pulse animation
- Neon border glow transitions on card hover
- Optional subtle scanlines on hero (respect `prefers-reduced-motion`)

## Capabilities

### New Capabilities

- `scroll-animations`: Intersection Observer-based fade-in-up animations for section content
- `stat-counter`: Animated number count-up when stats section enters viewport
- `hud-effects`: CSS-based HUD visual effects (glow, scanlines, corner brackets)

### Modified Capabilities

- None (this is a visual polish/redesign, not a feature change)

## Impact

### Files Affected

- `styles.css` - Major updates:
  - New HUD color variables and glow effects
  - Updated card hover states with neon borders
  - Scanline overlay CSS
  - Corner bracket decorations
  - Typography enhancements (optional Orbitron)

- `index.html` - Structure changes:
  - Simplified video grid (6 max)
  - Enhanced hero badge markup
  - Expert card layout simplification
  - Replace emoji icons with SVG icons

- `script.js` - New functionality:
  - Scroll animation logic (Intersection Observer)
  - Stat counter animation
  - Reduced motion detection

### No Breaking Changes

- All existing content and functionality preserved
- Existing color scheme enhanced (not replaced)
- Mobile responsiveness maintained and improved
- Accessibility: `prefers-reduced-motion` respected, contrast ratios maintained

### Anti-Patterns to Avoid

- No emojis as UI icons (use SVG)
- Limit glow effects to 2-3 key elements per section
- No continuous animations on decorative elements
- Scanlines must not interfere with text readability
- Neon accents on dark backgrounds only (no neon-on-neon)
