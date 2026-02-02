## ADDED Requirements

### Requirement: Cards have glowing border on hover

The system SHALL apply a neon glow border effect to cards on hover.

#### Scenario: Card hover state
- **WHEN** user hovers over a card (video, event, expert, feature)
- **THEN** the card border transitions to `--hud-cyan` or `--color-primary` with glow
- **THEN** transition duration is 300ms ease

#### Scenario: Card lift on hover
- **WHEN** user hovers over a card
- **THEN** the card translates up by 4px (`translateY(-4px)`)
- **THEN** box-shadow increases for depth effect

### Requirement: Hero section has scanline overlay

The system SHALL display a subtle scanline overlay on the hero section background.

#### Scenario: Scanlines render correctly
- **WHEN** the hero section loads
- **THEN** a repeating horizontal line pattern is visible
- **THEN** scanline opacity is between 0.03 and 0.05 (very subtle)

#### Scenario: Scanlines do not affect text
- **WHEN** text content is displayed over the hero
- **THEN** scanlines are rendered behind text (z-index management)
- **THEN** text remains fully readable

#### Scenario: Scanlines respect reduced motion
- **WHEN** `prefers-reduced-motion: reduce` is enabled
- **THEN** any scanline animation (if present) is disabled

### Requirement: Status indicators have pulse animation

The system SHALL apply a pulse animation to status indicators (e.g., "Connected" dot in code block).

#### Scenario: Status dot pulses
- **WHEN** a status indicator with class `status-active` is displayed
- **THEN** it pulses between opacity 1.0 and 0.5 over 2 seconds
- **THEN** animation loops infinitely

#### Scenario: Pulse respects reduced motion
- **WHEN** `prefers-reduced-motion: reduce` is enabled
- **THEN** pulse animation is disabled
- **THEN** status indicator displays at full opacity

### Requirement: CTA buttons have glow on hover

The system SHALL apply a neon glow effect to primary CTA buttons on hover.

#### Scenario: Primary button hover
- **WHEN** user hovers over a `.btn-primary` button
- **THEN** box-shadow includes glow effect (`0 6px 30px rgba(102, 126, 234, 0.5)`)
- **THEN** button scales to 1.05

#### Scenario: Secondary button hover
- **WHEN** user hovers over a `.btn-secondary` button
- **THEN** background transitions to semi-transparent white
- **THEN** border brightens

### Requirement: Feature icons have HUD container styling

The system SHALL display feature icons in HUD-styled containers with subtle glow background.

#### Scenario: Feature icon container
- **WHEN** a feature card is displayed
- **THEN** the icon container has background `rgba(102, 126, 234, 0.15)`
- **THEN** the container has rounded corners (12-15px)

#### Scenario: Feature card hover
- **WHEN** user hovers over a feature card
- **THEN** icon container glow intensifies slightly

### Requirement: Emoji icons are replaced with SVG

The system SHALL use SVG icons from Lucide icon set instead of emoji characters.

#### Scenario: Feature section icons
- **WHEN** the feature/about section displays
- **THEN** icons are inline SVG elements (not emoji characters)
- **THEN** SVG icons inherit color from CSS (`currentColor`)

#### Scenario: SVG icon sizing
- **WHEN** an SVG icon is displayed
- **THEN** it uses consistent sizing (24x24 viewBox, w-6 h-6)
- **THEN** stroke width is consistent (2px)
