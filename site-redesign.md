# AI-Assisted Engineering Website Redesign Requirements

## Project Overview

Modernize and polish the existing https://ai-assisted.engineering/ website to improve visual appeal, user experience, and professional feel while maintaining the existing dark tech aesthetic and content structure.

---

## Current Site Analysis

### What's Working Well (Keep)
- Gradient text on "Engineering" heading
- Code block mockup in hero
- Stats section visual hierarchy
- Overall dark color scheme
- Content structure and messaging

### Issues to Fix
1. **Video grid is too dense** — 12+ thumbnails overwhelming users
2. **Tutorials section uses white background** — breaks dark theme flow
3. **Section spacing is cramped** — needs more breathing room
4. **Expert cards are text-heavy** — hard to scan
5. **"Master the Tools" section** — left/right columns feel disconnected
6. **Upcoming Events feels sparse** — only 2 cards with empty space
7. **Lack of micro-interactions** — static, no hover states
8. **Typography hierarchy** — headings feel similar in weight

---

## Design System (Existing Colors — Do Not Change)

```css
:root {
  /* Primary */
  --color-primary: #667eea;
  --color-primary-hover: rgba(102, 126, 234, 0.9);
  --color-primary-glow: rgba(102, 126, 234, 0.3);
  --color-primary-tint: rgba(102, 126, 234, 0.1);
  
  /* Backgrounds */
  --color-bg-base: #0a0a0a;
  --color-bg-elevated: #111111;
  --color-bg-deep: #1a1a2e;
  
  /* Text */
  --color-text-primary: #ffffff;
  --color-text-secondary: #b3b3b3;
  --color-text-muted: #999999;
  
  /* Borders */
  --color-border-subtle: rgba(255, 255, 255, 0.1);
  --color-border-visible: rgba(255, 255, 255, 0.3);
}
```

---

## Global Improvements

### 1. Section Spacing
```css
/* BEFORE: ~60-80px padding */
/* AFTER: 120px padding for breathing room */

section {
  padding: 120px 0;
}

/* Section headers */
.section-header {
  margin-bottom: 64px; /* Was ~32-40px */
}
```

### 2. Typography Scale
```css
h1 {
  font-size: 4rem;      /* 64px */
  font-weight: 700;
  line-height: 1.1;
}

h2 {
  font-size: 2.5rem;    /* 40px */
  font-weight: 600;
  line-height: 1.2;
}

h3 {
  font-size: 1.5rem;    /* 24px */
  font-weight: 600;
}

h4 {
  font-size: 1.125rem;  /* 18px */
  font-weight: 500;
}

/* Body text */
.body-large {
  font-size: 1.125rem;  /* 18px */
  line-height: 1.7;
}

.body-regular {
  font-size: 1rem;      /* 16px */
  line-height: 1.6;
}
```

### 3. Card Hover States (Global)
```css
.card {
  transition: transform 0.3s ease, border-color 0.3s ease, box-shadow 0.3s ease;
}

.card:hover {
  transform: translateY(-4px);
  border-color: rgba(102, 126, 234, 0.5);
  box-shadow: 0 20px 40px rgba(0, 0, 0, 0.3);
}
```

### 4. Background Consistency
**Remove all white/light backgrounds.** Every section should use:
- `--color-bg-base` (#0a0a0a) — primary sections
- `--color-bg-deep` (#1a1a2e) — alternating sections
- `--color-bg-elevated` (#111111) — cards and elevated elements

### 5. Subtle Grid Pattern (Optional Depth)
```css
.section-with-pattern {
  background-image: 
    linear-gradient(rgba(102, 126, 234, 0.03) 1px, transparent 1px),
    linear-gradient(90deg, rgba(102, 126, 234, 0.03) 1px, transparent 1px);
  background-size: 50px 50px;
}
```

### 6. Section Dividers
Instead of hard edges, use gradient transitions:
```css
.section-divider {
  height: 1px;
  background: linear-gradient(
    90deg, 
    transparent 0%, 
    rgba(102, 126, 234, 0.3) 50%, 
    transparent 100%
  );
  max-width: 600px;
  margin: 0 auto;
}
```

---

## Section-Specific Improvements

---

### HERO SECTION

#### Current Issues
- Text could be larger and bolder
- CTAs are small
- Code block is nice but could have more polish
- Missing visual interest (orbs, gradients)

#### Requirements

**Background Enhancement:**
```css
.hero {
  position: relative;
  padding: 160px 0 120px;
  background: radial-gradient(
    ellipse 80% 50% at 50% -20%, 
    rgba(102, 126, 234, 0.15), 
    transparent
  );
}
```

**Add Pill Badge Above Headline:**
```html
<div class="hero-badge">
  <span class="badge-icon">✨</span>
  Transform your development workflow
</div>
```
```css
.hero-badge {
  display: inline-flex;
  align-items: center;
  gap: 8px;
  padding: 8px 16px;
  background: rgba(102, 126, 234, 0.15);
  border: 1px solid rgba(102, 126, 234, 0.3);
  border-radius: 100px;
  font-size: 0.875rem;
  color: var(--color-primary);
  margin-bottom: 24px;
}
```

**Headline Styling:**
```css
.hero h1 {
  font-size: 4rem;
  font-weight: 700;
  line-height: 1.1;
}

.hero h1 .gradient-text {
  background: linear-gradient(135deg, #667eea 0%, #764ba2 50%, #a855f7 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

@media (max-width: 768px) {
  .hero h1 {
    font-size: 2.5rem;
  }
}
```

**CTA Buttons:**
```css
.btn-primary {
  padding: 16px 32px;
  font-size: 1rem;
  font-weight: 600;
  background: var(--color-primary);
  color: white;
  border-radius: 12px;
  box-shadow: 0 4px 20px rgba(102, 126, 234, 0.4);
  transition: transform 0.2s ease, box-shadow 0.2s ease;
}

.btn-primary:hover {
  transform: scale(1.05);
  box-shadow: 0 6px 30px rgba(102, 126, 234, 0.5);
}

.btn-secondary {
  padding: 16px 32px;
  font-size: 1rem;
  font-weight: 600;
  background: transparent;
  color: white;
  border: 1px solid var(--color-border-visible);
  border-radius: 12px;
  transition: background 0.2s ease;
}

.btn-secondary:hover {
  background: rgba(255, 255, 255, 0.1);
}
```

**Code Block Enhancement:**
```css
.code-block {
  background: var(--color-bg-deep);
  border: 1px solid var(--color-border-subtle);
  border-radius: 16px;
  padding: 24px;
  box-shadow: 0 25px 50px rgba(0, 0, 0, 0.5);
}

/* Add status indicator */
.code-status {
  display: flex;
  align-items: center;
  gap: 8px;
  margin-top: 16px;
  font-size: 0.875rem;
  color: var(--color-text-muted);
}

.code-status .dot {
  width: 8px;
  height: 8px;
  background: #22c55e;
  border-radius: 50%;
  animation: pulse 2s infinite;
}

@keyframes pulse {
  0%, 100% { opacity: 1; }
  50% { opacity: 0.5; }
}
```

---

### STATS SECTION

#### Current Issues
- Cards are flat
- Numbers are static
- Could use more visual impact

#### Requirements

**Card Styling:**
```css
.stat-card {
  background: rgba(102, 126, 234, 0.08);
  border: 1px solid rgba(102, 126, 234, 0.2);
  border-radius: 16px;
  padding: 40px 32px;
  text-align: center;
  transition: border-color 0.3s ease, box-shadow 0.3s ease;
}

.stat-card:hover {
  border-color: rgba(102, 126, 234, 0.4);
  box-shadow: 0 0 40px rgba(102, 126, 234, 0.15);
}
```

**Gradient Numbers:**
```css
.stat-number {
  font-size: 3.5rem;
  font-weight: 700;
  background: linear-gradient(135deg, #667eea 0%, #a855f7 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}
```

**Animated Count-Up (JavaScript):**
```javascript
// Trigger when section enters viewport
const animateStats = () => {
  const stats = [
    { element: '.stat-1', target: 73, suffix: '%' },
    { element: '.stat-2', target: 40, suffix: '%' },
    { element: '.stat-3', target: 2025, suffix: '' }
  ];
  
  stats.forEach(stat => {
    const el = document.querySelector(stat.element);
    let current = 0;
    const increment = stat.target / 60;
    const timer = setInterval(() => {
      current += increment;
      if (current >= stat.target) {
        current = stat.target;
        clearInterval(timer);
      }
      el.textContent = Math.round(current) + stat.suffix;
    }, 30);
  });
};

// Use Intersection Observer to trigger
const observer = new IntersectionObserver((entries) => {
  entries.forEach(entry => {
    if (entry.isIntersecting) {
      animateStats();
      observer.unobserve(entry.target);
    }
  });
}, { threshold: 0.5 });

observer.observe(document.querySelector('.stats-section'));
```

---

### TUTORIALS SECTION (Featured Videos)

#### Current Issues
- **WHITE BACKGROUND** — breaks dark theme (CRITICAL FIX)
- 12+ videos overwhelming the grid
- Cards are too small and cramped

#### Requirements

**CRITICAL: Change Background to Dark**
```css
.tutorials-section {
  background: var(--color-bg-base); /* #0a0a0a */
  padding: 120px 0;
}
```

**Reduce Grid to 6 Videos Max:**
```html
<div class="tutorials-section">
  <div class="section-header">
    <h2>Featured Tutorials</h2>
    <p>Master AI-powered development with comprehensive guides</p>
  </div>
  
  <!-- Optional: Category tabs -->
  <div class="tutorial-tabs">
    <button class="tab active">All</button>
    <button class="tab">Getting Started</button>
    <button class="tab">Advanced</button>
    <button class="tab">Tools</button>
  </div>
  
  <div class="video-grid">
    <!-- Show only 6 videos -->
    <div class="video-card">...</div>
    <div class="video-card">...</div>
    <div class="video-card">...</div>
    <div class="video-card">...</div>
    <div class="video-card">...</div>
    <div class="video-card">...</div>
  </div>
  
  <div class="tutorials-footer">
    <a href="/tutorials" class="view-all-link">
      View all 50+ tutorials
      <svg><!-- arrow icon --></svg>
    </a>
  </div>
</div>
```

**Video Grid Layout:**
```css
.video-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 32px;
}

@media (max-width: 1024px) {
  .video-grid {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media (max-width: 640px) {
  .video-grid {
    grid-template-columns: 1fr;
  }
}
```

**Video Card Styling:**
```css
.video-card {
  background: var(--color-bg-elevated);
  border: 1px solid var(--color-border-subtle);
  border-radius: 16px;
  overflow: hidden;
  transition: transform 0.3s ease, border-color 0.3s ease, box-shadow 0.3s ease;
}

.video-card:hover {
  transform: translateY(-4px);
  border-color: rgba(102, 126, 234, 0.5);
  box-shadow: 0 20px 40px rgba(0, 0, 0, 0.4);
}

.video-thumbnail {
  position: relative;
  aspect-ratio: 16/9;
  overflow: hidden;
}

.video-thumbnail img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform 0.3s ease;
}

.video-card:hover .video-thumbnail img {
  transform: scale(1.05);
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
  display: flex;
  align-items: center;
  justify-content: center;
  transition: transform 0.2s ease, background 0.2s ease;
}

.video-card:hover .video-play-button {
  transform: translate(-50%, -50%) scale(1.1);
  background: var(--color-primary);
}

.video-info {
  padding: 20px;
}

.video-title {
  font-size: 1rem;
  font-weight: 600;
  color: var(--color-text-primary);
  line-height: 1.4;
  margin-bottom: 8px;
  /* Limit to 2 lines */
  display: -webkit-box;
  -webkit-line-clamp: 2;
  -webkit-box-orient: vertical;
  overflow: hidden;
}

.video-meta {
  font-size: 0.875rem;
  color: var(--color-text-muted);
}
```

**Optional Category Tabs:**
```css
.tutorial-tabs {
  display: flex;
  gap: 8px;
  margin-bottom: 48px;
  justify-content: center;
}

.tab {
  padding: 10px 20px;
  background: transparent;
  border: 1px solid var(--color-border-subtle);
  border-radius: 100px;
  color: var(--color-text-secondary);
  font-size: 0.875rem;
  cursor: pointer;
  transition: all 0.2s ease;
}

.tab:hover {
  border-color: var(--color-border-visible);
  color: var(--color-text-primary);
}

.tab.active {
  background: var(--color-primary);
  border-color: var(--color-primary);
  color: white;
}
```

**"View All" Link:**
```css
.tutorials-footer {
  text-align: center;
  margin-top: 48px;
}

.view-all-link {
  display: inline-flex;
  align-items: center;
  gap: 8px;
  color: var(--color-primary);
  font-weight: 500;
  transition: gap 0.2s ease;
}

.view-all-link:hover {
  gap: 12px;
}
```

---

### UPCOMING EVENTS SECTION

#### Current Issues
- Only 2 cards with lots of empty space
- Cards feel minimal/sparse

#### Requirements

**Layout Options:**

Option A: If you only have 2 events, center them:
```css
.events-grid {
  display: flex;
  justify-content: center;
  gap: 32px;
  max-width: 800px;
  margin: 0 auto;
}

.event-card {
  flex: 1;
  max-width: 360px;
}
```

Option B: Add visual elements to fill space:
```html
<div class="events-section">
  <div class="events-layout">
    <div class="events-info">
      <h2>Upcoming Events</h2>
      <p>Join me at conferences and meetups around the world</p>
      <a href="/events" class="btn-secondary">See all events</a>
    </div>
    <div class="events-grid">
      <div class="event-card">...</div>
      <div class="event-card">...</div>
    </div>
  </div>
</div>
```

**Event Card Styling:**
```css
.event-card {
  background: var(--color-bg-elevated);
  border: 1px solid var(--color-border-subtle);
  border-radius: 16px;
  padding: 32px;
  transition: all 0.3s ease;
}

.event-card:hover {
  transform: translateY(-4px);
  border-color: rgba(102, 126, 234, 0.4);
}

.event-date {
  display: inline-flex;
  flex-direction: column;
  align-items: center;
  background: rgba(102, 126, 234, 0.15);
  border-radius: 12px;
  padding: 12px 16px;
  margin-bottom: 20px;
}

.event-date .month {
  font-size: 0.75rem;
  font-weight: 600;
  color: var(--color-primary);
  text-transform: uppercase;
}

.event-date .day {
  font-size: 1.5rem;
  font-weight: 700;
  color: var(--color-text-primary);
}

.event-name {
  font-size: 1.25rem;
  font-weight: 600;
  color: var(--color-text-primary);
  margin-bottom: 8px;
}

.event-location {
  font-size: 0.875rem;
  color: var(--color-text-muted);
  display: flex;
  align-items: center;
  gap: 6px;
}
```

---

### MEET THE EXPERTS SECTION

#### Current Issues
- Cards are too text-heavy (long bios)
- Small profile photos
- No interactive elements

#### Requirements

**Simplified Expert Card:**
```html
<div class="expert-card">
  <div class="expert-photo">
    <img src="viktor.jpg" alt="Viktor Gamov" />
  </div>
  <div class="expert-info">
    <h4 class="expert-name">Viktor Gamov</h4>
    <p class="expert-role">Principal Developer Advocate</p>
    <p class="expert-bio">
      <!-- MAX 2 lines / ~100 characters -->
      Java Champion & streaming expert helping developers master AI-assisted engineering.
    </p>
    <div class="expert-links">
      <a href="#" class="social-link"><svg><!-- LinkedIn --></svg></a>
      <a href="#" class="social-link"><svg><!-- Twitter --></svg></a>
      <a href="#" class="social-link"><svg><!-- YouTube --></svg></a>
    </div>
    <a href="#" class="expert-cta">Watch their talks →</a>
  </div>
</div>
```

**Expert Card Styling:**
```css
.expert-card {
  background: var(--color-bg-elevated);
  border: 1px solid var(--color-border-subtle);
  border-radius: 16px;
  padding: 32px;
  display: flex;
  gap: 24px;
  align-items: flex-start;
  transition: all 0.3s ease;
}

.expert-card:hover {
  border-color: var(--color-primary);
  transform: translateY(-4px);
}

.expert-photo {
  width: 80px;
  height: 80px;
  border-radius: 50%;
  overflow: hidden;
  flex-shrink: 0;
  background: linear-gradient(135deg, #667eea, #764ba2);
}

.expert-photo img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.expert-name {
  font-size: 1.25rem;
  font-weight: 600;
  color: var(--color-text-primary);
  margin-bottom: 4px;
}

.expert-role {
  font-size: 0.875rem;
  color: var(--color-primary);
  margin-bottom: 12px;
}

.expert-bio {
  font-size: 0.875rem;
  color: var(--color-text-secondary);
  line-height: 1.5;
  margin-bottom: 16px;
  /* Limit to 2 lines */
  display: -webkit-box;
  -webkit-line-clamp: 2;
  -webkit-box-orient: vertical;
  overflow: hidden;
}

.expert-links {
  display: flex;
  gap: 8px;
  margin-bottom: 16px;
}

.social-link {
  width: 36px;
  height: 36px;
  display: flex;
  align-items: center;
  justify-content: center;
  background: var(--color-bg-base);
  border-radius: 8px;
  color: var(--color-text-secondary);
  transition: all 0.2s ease;
}

.social-link:hover {
  background: var(--color-primary-tint);
  color: var(--color-primary);
}

.expert-cta {
  font-size: 0.875rem;
  font-weight: 500;
  color: var(--color-primary);
  transition: gap 0.2s ease;
  display: inline-flex;
  align-items: center;
  gap: 4px;
}

.expert-cta:hover {
  gap: 8px;
}
```

---

### MASTER THE TOOLS SECTION

#### Current Issues
- Left column (icon list) and right column (stats) feel disconnected
- Two different visual styles that don't relate

#### Requirements

**Option A: Unified Feature Grid**
Replace the two-column layout with a consistent 3-column feature grid:

```html
<div class="features-section">
  <div class="section-header">
    <h2>Master the Tools That Matter</h2>
    <p>From beginner-friendly introductions to advanced techniques</p>
  </div>
  
  <div class="features-grid">
    <div class="feature-card">
      <div class="feature-icon">🚀</div>
      <h4>Accelerate Development</h4>
      <p>Cut development time in half with intelligent code suggestions.</p>
    </div>
    <div class="feature-card">
      <div class="feature-icon">🧠</div>
      <h4>Intelligent Problem Solving</h4>
      <p>Get instant solutions to complex coding challenges.</p>
    </div>
    <div class="feature-card">
      <div class="feature-icon">📚</div>
      <h4>Learn While You Code</h4>
      <p>Discover new patterns through AI recommendations.</p>
    </div>
    <!-- ... more cards -->
  </div>
  
  <!-- Stats as a separate row below -->
  <div class="features-stats">
    <div class="mini-stat">
      <span class="mini-stat-number">10x</span>
      <span class="mini-stat-label">Faster Development</span>
    </div>
    <div class="mini-stat">
      <span class="mini-stat-number">90%</span>
      <span class="mini-stat-label">Fewer Bugs</span>
    </div>
    <div class="mini-stat">
      <span class="mini-stat-number">50+</span>
      <span class="mini-stat-label">AI Tools Covered</span>
    </div>
  </div>
</div>
```

**Feature Card Styling:**
```css
.features-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 32px;
  margin-bottom: 64px;
}

@media (max-width: 1024px) {
  .features-grid {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media (max-width: 640px) {
  .features-grid {
    grid-template-columns: 1fr;
  }
}

.feature-card {
  background: var(--color-bg-elevated);
  border: 1px solid var(--color-border-subtle);
  border-radius: 16px;
  padding: 32px;
  transition: all 0.3s ease;
}

.feature-card:hover {
  border-color: rgba(102, 126, 234, 0.4);
  box-shadow: 0 0 30px rgba(102, 126, 234, 0.1);
  transform: translateY(-4px);
}

.feature-icon {
  width: 56px;
  height: 56px;
  display: flex;
  align-items: center;
  justify-content: center;
  background: rgba(102, 126, 234, 0.15);
  border-radius: 12px;
  font-size: 1.5rem;
  margin-bottom: 20px;
}

.feature-card h4 {
  font-size: 1.125rem;
  font-weight: 600;
  color: var(--color-text-primary);
  margin-bottom: 12px;
}

.feature-card p {
  font-size: 0.9375rem;
  color: var(--color-text-secondary);
  line-height: 1.6;
}
```

**Mini Stats Row:**
```css
.features-stats {
  display: flex;
  justify-content: center;
  gap: 64px;
  padding-top: 48px;
  border-top: 1px solid var(--color-border-subtle);
}

.mini-stat {
  text-align: center;
}

.mini-stat-number {
  display: block;
  font-size: 2.5rem;
  font-weight: 700;
  background: linear-gradient(135deg, #667eea 0%, #a855f7 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

.mini-stat-label {
  font-size: 0.875rem;
  color: var(--color-text-muted);
}
```

---

## Scroll Animations (Optional Enhancement)

Add subtle fade-in-up animations as sections enter viewport:

```css
.animate-on-scroll {
  opacity: 0;
  transform: translateY(20px);
  transition: opacity 0.6s ease, transform 0.6s ease;
}

.animate-on-scroll.visible {
  opacity: 1;
  transform: translateY(0);
}
```

```javascript
const animateOnScroll = () => {
  const elements = document.querySelectorAll('.animate-on-scroll');
  
  const observer = new IntersectionObserver((entries) => {
    entries.forEach(entry => {
      if (entry.isIntersecting) {
        entry.target.classList.add('visible');
      }
    });
  }, { threshold: 0.1 });
  
  elements.forEach(el => observer.observe(el));
};

document.addEventListener('DOMContentLoaded', animateOnScroll);
```

---

## Implementation Checklist

### Critical (Do First)
- [ ] Change tutorials section background from white to dark (#0a0a0a)
- [ ] Reduce video grid from 12+ to 6 max
- [ ] Increase section padding to 120px
- [ ] Add card hover states globally

### High Priority
- [ ] Enhance hero with larger text, pill badge, gradient orb
- [ ] Add gradient numbers to stats section
- [ ] Simplify expert cards (shorter bio, larger photo, social links)
- [ ] Restructure "Master the Tools" section

### Nice to Have
- [ ] Animated stat count-up on scroll
- [ ] Scroll-triggered fade-in animations
- [ ] Category tabs for tutorials
- [ ] Subtle grid pattern backgrounds
- [ ] Code block status indicator

---

## File Structure

```
/styles
├── variables.css      # CSS custom properties
├── global.css         # Base styles, typography
├── components.css     # Cards, buttons, forms
├── sections/
│   ├── hero.css
│   ├── stats.css
│   ├── tutorials.css
│   ├── events.css
│   ├── experts.css
│   └── features.css
└── animations.css     # Scroll animations, hover effects

/scripts
├── animations.js      # Scroll-triggered animations
└── stats-counter.js   # Animated number count-up
```

---

## Testing Checklist

- [ ] All sections have dark backgrounds (no white)
- [ ] Hover states work on all cards
- [ ] Typography hierarchy is clear (h1 > h2 > h3 > h4)
- [ ] Section spacing feels spacious
- [ ] Mobile responsive (test at 375px, 768px, 1024px)
- [ ] Video grid shows max 6 items with "View all" link
- [ ] Expert cards are scannable (short bios)
- [ ] Stats animate on scroll (if implemented)
- [ ] No horizontal scroll on mobile
- [ ] All links/buttons have hover states