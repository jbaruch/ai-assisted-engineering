## ADDED Requirements

### Requirement: Stats animate with count-up effect

The system SHALL animate numeric statistics from 0 to their target value when the stats section enters the viewport.

#### Scenario: Stats section enters viewport
- **WHEN** the stats section (`.why-ai-stats`) scrolls into view
- **THEN** each stat number animates from 0 to its target value over 2 seconds

#### Scenario: Count-up animation easing
- **WHEN** a stat number is animating
- **THEN** the animation uses ease-out timing (fast start, slow finish)
- **THEN** numbers are rounded to integers during animation

#### Scenario: Stat with suffix
- **WHEN** a stat has a suffix (e.g., "73%", "40%", "2025")
- **THEN** the suffix is preserved during and after animation
- **THEN** only the numeric portion animates

### Requirement: Count-up triggers only once

The system SHALL trigger the count-up animation only on the first viewport entry.

#### Scenario: Re-scrolling to stats section
- **WHEN** user scrolls away from stats section and returns
- **THEN** stats remain at their final values
- **THEN** animation does not replay

### Requirement: Count-up respects reduced motion

The system SHALL skip count-up animation when reduced motion is preferred.

#### Scenario: Reduced motion enabled
- **WHEN** the media query `prefers-reduced-motion: reduce` matches
- **THEN** stat numbers display their final values immediately
- **THEN** no count-up animation occurs

### Requirement: Stats are readable before animation

The system SHALL display stat values even if JavaScript fails.

#### Scenario: JavaScript disabled or failed
- **WHEN** JavaScript does not execute
- **THEN** stat values are visible in the HTML (not injected)
- **THEN** users can still read the statistics
