# PRD: Dark Theme for Memory Game

## Overview
Add a toggleable Dark Theme to the Memory Game to improve usability in low-light conditions, match user OS preferences, and modernize the visual design.

## Goals
- Provide a visually consistent dark color scheme with minimal layout changes.
- Allow users to toggle between Light and Dark themes.
- Respect the OS-level `prefers-color-scheme` by default.
- Persist user choice across sessions using `localStorage`.
- Maintain accessibility (contrast, focus states, screen reader labels, keyboard navigation).

## Success Metrics
- Theme toggle used by at least 20% of returning users in first month (if telemetry available).
- No accessibility contrast violations per automated checks (WCAG AA for normal text).
- No regressions in core gameplay (matching logic, timer, moves).

## User Stories
- As a player, I can enable Dark Theme to reduce eye strain in low-light environments.
- As a returning player, my chosen theme persists across visits.
- As a keyboard user, I can toggle the theme and navigate with visible focus states.

## UX & Interaction
- Place a theme toggle button in the `.controls` area (a sun/moon icon). Tooltip: "Toggle theme".
- Default theme: follow `prefers-color-scheme`. If user explicitly toggles, save their preference.
- When toggled, apply theme immediately without reloading the page.

## Design & Visuals
- Implement colors using CSS custom properties (variables) in `:root` and a `.dark-theme` class.
- Light variables already exist (e.g., `--background-color`, `--card-back`, `--card-front`, `--text-color`). Add complementary dark values:
  - `--background-color`: #0f1720
  - `--card-back`: #1f2937
  - `--card-front`: #0b1220 (or a soft surface color)
  - `--text-color`: #e6eef8
  - `--muted-color`: #9aa6b2
  - `--success-color`: #16a34a
  - `--primary-color`: adjust to a visible accent in dark mode (e.g., #3b82f6)
- Ensure card front/back contrast is >= 4.5:1 for text/icons.

## Accessibility
- Ensure focus outlines use `--primary-color` with sufficient contrast.
- Provide `aria-pressed` and `aria-label` for toggle button (e.g., `aria-pressed="true"` when dark).
- Verify color contrast with automated tools (axe-core, Lighthouse) and manual checks.

## Technical Implementation
1. CSS
   - Refactor existing color constants to use CSS variables at top of `memory-game.html`.
   - Add a `.dark-theme` selector that overrides dark variables.
   - Example structure:
     ```css
     :root { --background-color: #f5f5f5; --text-color: #333; /* ... */ }
     .dark-theme { --background-color: #0f1720; --text-color: #e6eef8; /* ... */ }
     body { background-color: var(--background-color); color: var(--text-color); }
     ```
2. JavaScript
   - Add a theme toggle UI in the `.controls` area.
   - On load, determine theme by:
     - Checking `localStorage.getItem('theme')` for `'dark'|'light'`.
     - Otherwise, use `window.matchMedia('(prefers-color-scheme: dark)').matches`.
   - Apply theme by toggling `document.documentElement.classList` (add/remove `dark-theme`).
   - Persist changes to `localStorage` and set appropriate `aria-pressed` on the toggle.
   - Update any dynamic elements (e.g., modal background) if needed.
3. Persistence
   - Use `localStorage.setItem('theme', 'dark')` or `'light'`.
4. Testing
   - Unit test JS behavior (if test harness exists) or add simple runtime checks:
     - Theme persists across reloads.
     - Toggle updates `aria-pressed`.
   - Run automated a11y checks.

## Edge Cases & Risks
- If user has browser extensions that force colors, the theme may be overridden.
- Existing inline styles with hard-coded colors could cause visual regressions; prefer variable-based colors.
- Must ensure modal overlay contrast remains usable in dark mode.

## Rollout Plan
- Phase 1: Add PRD and implement CSS + toggle in a feature branch `feature/dark-theme`.
- Phase 2: Run accessibility and compatibility checks across browsers and screen sizes.
- Phase 3: Merge and monitor user feedback.

## Timeline (Estimates)
- PRD + small design review: 0.5 day
- Implementation (CSS + toggle + persistence): 1 day
- Accessibility & QA: 0.5 day
- Total: ~2 days

## Acceptance Criteria
- A working theme toggle appears in UI and persists selection.
- Dark theme respects `prefers-color-scheme` when no explicit selection exists.
- Visual contrast meets WCAG AA for text and controls.
- No changes to game mechanics or stored scores.

## Files to change
- `memory-game.html` — move color values to CSS variables, add `.dark-theme`, add toggle button, and add JS logic for persistence.

---

*Author: GitHub Copilot*  
*Date: 2026-06-27*
