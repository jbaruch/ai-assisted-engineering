# Design Document

## Overview

This design document outlines the technical approach for modernizing the AI-Assisted Engineering website while maintaining its existing dark tech aesthetic. The redesign focuses on critical fixes (background consistency, video grid optimization), enhanced user interactions (hover states, animations), and improved visual hierarchy through better typography and spacing.

The design maintains the existing vanilla JavaScript architecture with zero framework dependencies, ensuring fast loading times and broad browser compatibility. All enhancements will be implemented through CSS improvements and minimal JavaScript additions for animations.

## Architecture

### Design System Foundation

The redesign builds upon the existing CSS custom properties system, extending it with additional variables for consistent spacing, typography, and interaction states. The architecture maintains the current file structure:

- `styles.css` - Enhanced with new design system variables and component styles
- `script.js` - Extended with intersection observer for scroll animations
- `site-config.js` - Unchanged, maintaining content separation
- `index.html` - Minimal structural changes for new elements

### Color System Enhancement

The existing color palette will be preserved and extended:

```css
:root {
  /* Existing colors (preserved) */
  --color-primary: #667eea;
  --color-bg-base: #0a0a0a;
  --color-bg-elevated: #111111;
  --color-bg-deep: #1a1a2e;
  
  /* New interaction states */
  --color-primary-hover: rgba(102, 126, 234, 0.9);
  --color-primary-glow: rgba(102, 126, 234, 0.3);
  --color-primary-tint: rgba(102, 126, 234, 0.1);
  
  /* Enhanced borders */
  --color-border-subtle: rgba(255, 255, 255, 0.1);
  --color-border-visible: rgba(255, 255, 255, 0.3);
  --color-border-hover: rgba(102, 126, 234, 0.5);
}
```

### Typography Scale

A systematic typography scale will replace the current inconsistent sizing:

```css
:root {
  /* Typography scale */
  --font-size-h1: 4rem;      /* 64px */
  --font-size-h2: 2.5rem;    /* 40px */
  --font-size-h3: 1.5rem;    /* 24px */
  --font-size-h4: 1.125rem;  /* 18px */
  --font-size-body-large: 1.125rem;  /* 18px */
  --font-size-body: 1rem;    /* 16px */
  
  /* Line heights */
  --line-height-tight: 1.1;
  --line-height-normal: 1.2;
  --line-height-relaxed: 1.6;
  
  /* Font weights */
  --font-weight-bold: 700;
  --font-weight-semibold: 600;
  --font-weight-medium: 500;
}
```

### Spacing System

Consistent spacing will be implemented through a systematic scale:

```css
:root {
  /* Spacing scale */
  --space-section: 120px;    /* Section padding */
  --space-section-header: 64px;  /* Section header margin */
  --space-card-padding: 32px;    /* Card internal padding */
  --space-grid-gap: 32px;        /* Grid gaps */
  --space-element-gap: 24px;     /* Element spacing */
}
```

## Components and Interfaces

### Enhanced Card Component System

All cards (video, event, expert, feature) will share a common base class with consistent hover behaviors:

```css
.card-base {
  background: var(--color-bg-elevated);
  border: 1px solid var(--color-border-subtle);
  border-radius: 16px;
  transition: transform 0.3s ease, border-color 0.3s ease, box-shadow 0.3s ease;
}

.card-base:hover {
  transform: translateY(-4px);
  border-color: var(--color-border-hover);
  box-shadow: 0 20px 40px rgba(0, 0, 0, 0.3);
}
```

### Video Grid Component

The video grid will be restructured to show maximum 6 videos with improved card styling:

```css
.video-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: var(--space-grid-gap);
}

.video-card {
  @extend .card-base;
  overflow: hidden;
}

.video-thumbnail {
  aspect-ratio: 16/9;
  position: relative;
  overflow: hidden;
}

.video-play-button {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 56px;
  height: 56px;
  background: rgba(102, 126, 234, 0.9);
  border-radius: 50%;
  transition: transform 0.2s ease, background 0.2s ease;
}

.video-card:hover .video-play-button {
  transform: translate(-50%, -50%) scale(1.1);
  background: var(--color-primary);
}
```

### Hero Section Enhancement

The hero section will receive visual depth through gradient backgrounds and enhanced CTAs:

```css
.hero {
  background: radial-gradient(
    ellipse 80% 50% at 50% -20%, 
    rgba(102, 126, 234, 0.15), 
    transparent
  ), var(--color-bg-base);
  padding: 160px 0 120px;
}

.hero-badge {
  display: inline-flex;
  align-items: center;
  gap: 8px;
  padding: 8px 16px;
  background: var(--color-primary-tint);
  border: 1px solid rgba(102, 126, 234, 0.3);
  border-radius: 100px;
  font-size: 0.875rem;
  color: var(--color-primary);
  margin-bottom: 24px;
}

.btn-primary:hover {
  transform: scale(1.05);
  box-shadow: 0 6px 30px rgba(102, 126, 234, 0.5);
}
```

### Expert Card Redesign

Expert cards will be simplified for better scannability:

```css
.expert-card {
  @extend .card-base;
  padding: var(--space-card-padding);
  display: flex;
  gap: 24px;
  align-items: flex-start;
}

.expert-photo {
  width: 80px;
  height: 80px;
  border-radius: 50%;
  overflow: hidden;
  flex-shrink: 0;
  background: linear-gradient(135deg, #667eea, #764ba2);
}

.expert-bio {
  font-size: 0.875rem;
  color: var(--color-text-secondary);
  line-height: 1.5;
  /* Limit to 2 lines */
  display: -webkit-box;
  -webkit-line-clamp: 2;
  -webkit-box-orient: vertical;
  overflow: hidden;
}
```

## Data Models

### Animation State Management

The design includes scroll-triggered animations managed through intersection observers:

```javascript
// Animation state interface
interface AnimationState {
  element: HTMLElement;
  threshold: number;
  hasAnimated: boolean;
  animationClass: string;
}

// Statistics animation data
interface StatAnimation {
  element: string;
  target: number;
  suffix: string;
  duration: number;
}
```

### Responsive Breakpoint System

The design system defines consistent breakpoints:

```css
:root {
  --breakpoint-mobile: 480px;
  --breakpoint-tablet: 768px;
  --breakpoint-desktop: 1024px;
  --breakpoint-wide: 1200px;
}
```

## Correctness Properties

*A property is a characteristic or behavior that should hold true across all valid executions of a system—essentially, a formal statement about what the system should do. Properties serve as the bridge between human-readable specifications and machine-verifiable correctness guarantees.*

### Property Reflection

After analyzing all acceptance criteria, several properties can be consolidated to eliminate redundancy:

- Typography properties (6.1-6.5) can be combined into a single comprehensive typography consistency property
- Hover state properties (4.1-4.4) can be unified into one comprehensive card hover behavior property  
- Background consistency properties (1.1, 1.3) overlap and can be combined
- Mobile responsiveness properties (11.1-11.5) can be consolidated into fewer comprehensive properties

### Core Properties

**Property 1: Dark Theme Consistency**
*For any* section element on the website, the computed background-color should be one of the approved dark theme colors (#0a0a0a, #111111, or #1a1a2e)
**Validates: Requirements 1.1, 1.3**

**Property 2: Card Hover Behavior Uniformity**
*For any* card element (video, event, expert, feature), hovering should apply translateY(-4px) transform, border-color change to rgba(102, 126, 234, 0.5), and box-shadow of 0 20px 40px rgba(0, 0, 0, 0.3)
**Validates: Requirements 4.1, 4.2, 4.3, 4.4**

**Property 3: Typography Scale Consistency**
*For any* heading element (h1-h4), the computed font-size and font-weight should match the design system specifications (h1: 4rem/700, h2: 2.5rem/600, h3: 1.5rem/600, h4: 1.125rem/500)
**Validates: Requirements 6.1, 6.2, 6.3, 6.4, 6.5**

**Property 4: Responsive Grid Adaptation**
*For any* grid layout, the number of columns should adapt based on viewport width (3 columns ≥1024px, 2 columns 768-1023px, 1 column <768px)
**Validates: Requirements 2.3, 11.1**

**Property 5: Section Spacing Uniformity**
*For any* major section element, the padding-top and padding-bottom should be 120px, and section headers should have 64px margin-bottom
**Validates: Requirements 3.1, 3.2**

**Property 6: Expert Bio Length Constraint**
*For any* expert bio text element, the text content length should not exceed 100 characters
**Validates: Requirements 7.1**

**Property 7: Animation Timing Consistency**
*For any* count-up animation, the animation duration should complete within 2000ms and trigger only once per page load
**Validates: Requirements 10.3, 10.4**

**Property 8: Mobile Touch Accessibility**
*For any* interactive element at mobile viewport (≤768px), the computed width and height should be at least 44px for touch accessibility
**Validates: Requirements 11.3**

**Property 9: Performance Constraint Compliance**
*For any* CSS file additions, the total file size should remain under 50KB to maintain loading performance
**Validates: Requirements 12.5**

**Property 10: Color Contrast Accessibility**
*For any* text element, the color contrast ratio between text color and background color should meet or exceed WCAG AA standards (4.5:1 for normal text, 3:1 for large text)
**Validates: Requirements 12.4**

## Error Handling

### CSS Fallbacks

The design includes robust fallbacks for browser compatibility:

```css
/* Gradient fallbacks */
.gradient-text {
  color: #667eea; /* Fallback for browsers without gradient support */
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

/* Transform fallbacks */
.card-base:hover {
  /* Fallback for browsers without transform support */
  margin-top: -4px;
  transform: translateY(-4px);
}

/* Grid fallbacks */
.video-grid {
  /* Flexbox fallback for older browsers */
  display: flex;
  flex-wrap: wrap;
  gap: 32px;
  
  /* Modern grid for supported browsers */
  display: grid;
  grid-template-columns: repeat(3, 1fr);
}
```

### JavaScript Error Handling

Animation scripts include error handling for missing elements:

```javascript
// Safe element querying with error handling
function safeQuerySelector(selector) {
  try {
    return document.querySelector(selector);
  } catch (error) {
    console.warn(`Element not found: ${selector}`);
    return null;
  }
}

// Intersection Observer with feature detection
function initScrollAnimations() {
  if (!('IntersectionObserver' in window)) {
    // Fallback: show all elements immediately
    document.querySelectorAll('.animate-on-scroll').forEach(el => {
      el.classList.add('visible');
    });
    return;
  }
  
  // Modern intersection observer implementation
  const observer = new IntersectionObserver(handleIntersection, {
    threshold: 0.1,
    rootMargin: '0px 0px -50px 0px'
  });
  
  document.querySelectorAll('.animate-on-scroll').forEach(el => {
    observer.observe(el);
  });
}
```

### Performance Error Prevention

The design prevents common performance issues:

- **Layout Thrashing**: All animations use `transform` and `opacity` properties only
- **Memory Leaks**: Event listeners are properly cleaned up
- **Infinite Loops**: Animation counters have maximum iteration limits
- **Resource Loading**: Images include loading="lazy" and proper alt attributes

## Testing Strategy

### Dual Testing Approach

The redesign will be validated through both unit tests and property-based tests to ensure comprehensive coverage:

**Unit Tests** will verify:
- Specific examples and edge cases (mobile breakpoints, specific color values)
- Integration points between CSS and JavaScript
- Error conditions (missing elements, unsupported browsers)
- Accessibility features (focus states, ARIA attributes)

**Property-Based Tests** will verify:
- Universal properties across all card types and sections
- Responsive behavior across viewport ranges
- Animation consistency across different elements
- Color contrast compliance across all text/background combinations

### Property-Based Testing Configuration

Each correctness property will be implemented as a property-based test using a JavaScript testing framework (Jest with fast-check for property testing):

- **Minimum 100 iterations** per property test due to randomization
- **Test tagging format**: `Feature: site-redesign, Property {number}: {property_text}`
- **Viewport testing**: Properties will test across randomized viewport sizes
- **Element generation**: Tests will generate random DOM structures to verify universal behavior

### Testing Implementation Strategy

**CSS Testing Approach**:
```javascript
// Example property test structure
test('Feature: site-redesign, Property 1: Dark Theme Consistency', () => {
  fc.assert(fc.property(
    fc.array(fc.record({
      tagName: fc.constantFrom('section', 'div', 'article'),
      className: fc.constantFrom('hero', 'videos', 'events', 'about')
    })),
    (sections) => {
      // Generate DOM elements
      const container = createTestContainer(sections);
      
      // Apply CSS
      applyStylesheet(container);
      
      // Verify all sections have dark backgrounds
      const sectionElements = container.querySelectorAll('section, .hero, .videos, .events, .about');
      return Array.from(sectionElements).every(el => {
        const bgColor = getComputedStyle(el).backgroundColor;
        return isDarkColor(bgColor);
      });
    }
  ));
});
```

**Responsive Testing Approach**:
```javascript
test('Feature: site-redesign, Property 4: Responsive Grid Adaptation', () => {
  fc.assert(fc.property(
    fc.integer(320, 1920), // Random viewport widths
    (viewportWidth) => {
      // Set viewport
      setViewportWidth(viewportWidth);
      
      // Query grid elements
      const grids = document.querySelectorAll('.video-grid, .features-grid');
      
      // Verify column count matches breakpoint
      return Array.from(grids).every(grid => {
        const columnCount = getGridColumnCount(grid);
        if (viewportWidth >= 1024) return columnCount === 3;
        if (viewportWidth >= 768) return columnCount === 2;
        return columnCount === 1;
      });
    }
  ));
});
```

### Manual Testing Checklist

Beyond automated tests, manual verification will include:

- **Cross-browser testing**: Chrome, Firefox, Safari, Edge
- **Device testing**: iPhone, Android, tablet, desktop
- **Accessibility testing**: Screen reader compatibility, keyboard navigation
- **Performance testing**: Lighthouse scores, loading times
- **Visual regression testing**: Screenshot comparisons before/after changes

The testing strategy ensures that all visual improvements maintain the site's performance, accessibility, and cross-browser compatibility while delivering the enhanced user experience outlined in the requirements.