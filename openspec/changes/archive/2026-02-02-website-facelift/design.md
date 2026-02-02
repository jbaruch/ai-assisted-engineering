## Context

The AI-Assisted Engineering website is a static HTML/CSS/JS site promoting AI development tools and featuring video tutorials, expert profiles, and upcoming events. The current implementation uses:
- Vanilla HTML with semantic sections
- Custom CSS with CSS variables for theming
- Vanilla JavaScript for dynamic content loading and modal interactions
- Dark theme with purple/blue gradient accents (`--color-primary: #667eea`)

The site needs a visual refresh to achieve a premium "HUD / Sci-Fi FUI" aesthetic while maintaining all existing functionality and content.

## Goals / Non-Goals

**Goals:**
- Elevate visual polish with futuristic HUD aesthetic
- Improve UX through better spacing, typography hierarchy, and micro-interactions
- Add scroll-triggered animations for engagement
- Replace emoji icons with professional SVG icons
- Maintain accessibility (contrast ratios, reduced motion support)
- Keep all existing content and functionality intact

**Non-Goals:**
- No framework migration (stays vanilla HTML/CSS/JS)
- No new pages or routes
- No backend changes
- No content rewrites (only structural simplification)
- No mobile-first redesign (enhance existing responsive approach)

## Decisions

### Decision 1: Typography Approach

**Choice:** Hybrid typography - add Orbitron for display headlines, keep Inter for body text

**Rationale:**
- Orbitron provides futuristic aesthetic for key headlines without compromising readability
- Inter remains highly readable for body text and descriptions
- Minimizes font loading overhead (one additional font vs two)

**Alternatives Considered:**
- Full monospace (Share Tech Mono + Fira Code): Too aggressive, hurts readability
- Keep Inter only with glow effects: Doesn't achieve desired futuristic feel

### Decision 2: HUD Color Integration

**Choice:** Add HUD accent colors as supplementary variables, keep existing purple gradient as primary

**Rationale:**
- Existing `--color-primary: #667eea` works well and has brand recognition
- Cyan (`#00FFFF`) adds HUD accent without replacing primary
- Glow effects use existing primary color, cyan reserved for special elements

**Implementation:**
```css
:root {
  /* Existing - unchanged */
  --color-primary: #667eea;

  /* New HUD accents */
  --hud-cyan: #00FFFF;
  --hud-glow: 0 0 10px rgba(0, 255, 255, 0.3);
}
```

### Decision 3: Animation Strategy

**Choice:** CSS-first animations with JavaScript Intersection Observer for scroll triggers

**Rationale:**
- CSS animations are performant and respect `prefers-reduced-motion`
- Intersection Observer is lightweight and widely supported
- No animation library dependency needed

**Implementation Pattern:**
```javascript
// Single observer instance for all animated elements
const observer = new IntersectionObserver(callback, { threshold: 0.1 });
document.querySelectorAll('.animate-on-scroll').forEach(el => observer.observe(el));
```

### Decision 4: Icon Replacement Strategy

**Choice:** Use Lucide icons via inline SVG

**Rationale:**
- Lucide has consistent 24x24 viewBox and stroke-based design
- Inline SVG allows CSS color control and glow effects
- No icon font or sprite dependency

**Alternatives Considered:**
- Heroicons: Also good, but Lucide has better coverage for tech/data icons
- Icon fonts: Harder to apply glow effects, accessibility concerns

### Decision 5: Video Grid Limitation

**Choice:** Show 6 videos maximum with "View all" link to YouTube playlist

**Rationale:**
- Reduces visual overwhelm
- Maintains page performance
- External link keeps users in YouTube ecosystem for engagement

**Implementation:**
- Modify `script.js` to slice video array to first 6
- Add static "View all" link below grid

## Risks / Trade-offs

### Risk 1: Glow Effects on Low-End Devices
**Risk:** Box-shadow and text-shadow glow effects may cause jank on low-end mobile devices
**Mitigation:**
- Use `will-change: transform` sparingly
- Reduce glow intensity on mobile via media query
- Test on actual devices before release

### Risk 2: Orbitron Readability at Small Sizes
**Risk:** Orbitron font may be hard to read below 18px
**Mitigation:**
- Only use Orbitron for h1/h2 (≥24px)
- Fall back to Inter for h3/h4 and smaller

### Risk 3: Animation Performance
**Risk:** Too many scroll animations may cause stuttering
**Mitigation:**
- Limit to one animation per section (not per card)
- Use `transform` and `opacity` only (GPU-accelerated)
- Add `prefers-reduced-motion` check

### Risk 4: Scanline Effect Legibility
**Risk:** Scanlines may interfere with text readability
**Mitigation:**
- Apply scanlines only to hero background, not over text
- Use very low opacity (0.03-0.05)
- Make scanlines optional/removable

## Migration Plan

**Phase 1: CSS Foundation**
1. Add new CSS variables for HUD colors and glow effects
2. Update typography scale and spacing
3. Add Orbitron font import

**Phase 2: Component Styling**
1. Update card hover states with glow borders
2. Add scanline overlay to hero
3. Replace emoji icons with SVG

**Phase 3: JavaScript Enhancements**
1. Add scroll animation observer
2. Add stat counter animation
3. Limit video grid to 6 items

**Phase 4: Testing & Polish**
1. Cross-browser testing
2. Mobile responsiveness check
3. Accessibility audit (contrast, reduced motion)

**Rollback:** Since this is a static site, rollback is simply reverting the CSS/HTML/JS files via git.

## Open Questions

1. **Orbitron vs Space Grotesk:** Should we test Space Grotesk as an alternative futuristic font that's more readable?
2. **Scanline intensity:** What opacity level works best for the scanline effect without hurting readability?
3. **Video count:** Is 6 the right number, or should we show 3/6/9 based on viewport?
