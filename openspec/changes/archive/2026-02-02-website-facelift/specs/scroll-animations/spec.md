## ADDED Requirements

### Requirement: Sections animate on scroll into view

The system SHALL animate section content when it enters the viewport using a fade-in-up effect.

#### Scenario: Section enters viewport
- **WHEN** a section with class `animate-on-scroll` scrolls into view (threshold 10%)
- **THEN** the section receives class `visible` which triggers CSS animation

#### Scenario: Animation applies fade-in-up effect
- **WHEN** an element receives the `visible` class
- **THEN** it transitions from `opacity: 0; transform: translateY(20px)` to `opacity: 1; transform: translateY(0)` over 600ms

#### Scenario: Animation triggers only once
- **WHEN** a section has already animated into view
- **THEN** scrolling away and back does not re-trigger the animation

### Requirement: Reduced motion preference is respected

The system SHALL disable scroll animations when the user has `prefers-reduced-motion: reduce` enabled.

#### Scenario: User has reduced motion enabled
- **WHEN** the media query `prefers-reduced-motion: reduce` matches
- **THEN** all animation durations are reduced to 0.01ms
- **THEN** elements are visible immediately without animation

#### Scenario: Reduced motion check on page load
- **WHEN** the page loads
- **THEN** the scroll animation observer checks for reduced motion preference before initializing

### Requirement: Staggered animation for card grids

The system SHALL apply staggered animation delays to cards within a grid.

#### Scenario: Cards animate with stagger
- **WHEN** a grid container enters viewport
- **THEN** each card animates with an incremental delay (e.g., 0ms, 100ms, 200ms)
- **THEN** maximum stagger delay is 500ms to prevent slow reveals

#### Scenario: Mobile stagger is reduced
- **WHEN** viewport width is below 768px
- **THEN** stagger delay is halved (50ms increments) for faster reveal
