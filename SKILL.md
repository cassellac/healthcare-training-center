# Healthcare Training Center — Brand Design Skill

**Version 1.0 | Last Updated: June 4, 2026**

This skill provides instant reference for brand design decisions, component specs, color codes, typography, spacing, and usage guidelines for the Healthcare Training Center project.

---

## Quick Reference

### Core Colors
- **Primary Navy:** `#1E3A6E` — headers, nav, authority
- **Secondary Teal:** `#2B8FA9` — interactive, links, highlights
- **Room Colors:** CS `#3B7DD8` | HIPAA `#2BA89A` | Compliance `#2EAA6E` | Records `#7B5EA7` | Finance `#D4A017`
- **Semantic:** Success `#28A745` | Warning `#FFC107` | Error `#DC3545` | Info `#17A2B8`
- **Neutrals:** Surface `#F4F6F9` | Border `#D0D8E8` | Text `#475569`

### Typography
- **Headings:** Montserrat (ExtraBold 800 / Bold 700 / SemiBold 600)
- **Body:** Inter (Regular 400 / Medium 500 / SemiBold 600)
- **Display:** 48px ExtraBold | H1: 36px Bold | H2: 28px Bold | H3: 22px SemiBold | Body: 16px Regular

### Spacing Grid
Base: **8px** → 4 | 8 | 12 | 16 | 24 | 32 | 48 | 64 | 96px

### Buttons
| Variant | BG | Text | Border | Usage |
|---------|----|----|--------|-------|
| Primary | Navy | White | None | Main CTAs |
| Secondary | Teal | White | None | Secondary actions |
| Outline | Transparent | Navy | 2px Navy | Tertiary |
| Room-Accent | [Room Color] | White | None | In-room CTAs |
| Danger | Error Red | White | None | Destructive |

### Radius & Shadows
- **Radius:** 4px (badges) | 8px (buttons, cards) | 16px (room cards) | 24px (hero) | 9999px (pills)
- **Shadows:** sm `0 1px 3px rgba(0,0,0,0.08)` | md `0 4px 12px rgba(0,0,0,0.10)` | lg `0 8px 24px rgba(0,0,0,0.14)`

---

## Brand Voice Quick Rules

**Personality:** Trustworthy, Warm, Empowering, Clear

**Do:**
- Speak to learners as "you" / org as "we"
- Use Title Case for headers, sentence case for body
- Apply the rule of three: "Enter. Learn. Lead."
- Tie everything back to patient outcomes
- Use "→" arrow on CTAs, "✓" on completion badges

**Don't:**
- Use emoji for iconography (use Phosphor icons instead)
- Make copy cold or clinical
- Use jargon without context
- Sacrifice accessibility for aesthetics

---

## The Five Rooms

| # | Room | Color | Icon | Coverage |
|---|------|-------|------|----------|
| 1 | Customer Service | `#3B7DD8` | ph-users | Communication, empathy, de-escalation |
| 2 | HIPAA & Privacy | `#2BA89A` | ph-shield-check | PHI, privacy rule, breach prevention |
| 3 | Compliance | `#2EAA6E` | ph-clipboard-text | Laws, fraud/waste/abuse, ethics |
| 4 | Medical Records | `#7B5EA7` | ph-folder-open | EHR, documentation, retention |
| 5 | Finance | `#D4A017` | ph-currency-dollar | Revenue cycle, billing, collections |

**When entering a room:** Page recolors to room accent, nav accent changes, buttons use room color, progress bars use room color.

---

## Icon Library

**All icons from Phosphor Icons (MIT, free).**

### Room Icons
- Customer Service: `ph-users` (alt: `ph-chat-circle`)
- HIPAA: `ph-shield-check` (alt: `ph-lock`)
- Compliance: `ph-clipboard-text` (alt: `ph-check-circle`)
- Records: `ph-folder-open` (alt: `ph-archive`)
- Finance: `ph-currency-dollar` (alt: `ph-coins`)

### UI Icons
Progress `ph-chart-bar` | Certificate `ph-certificate` | Video `ph-video-camera` | Books `ph-books` | Archive `ph-archive` | Headset `ph-headset` | Medal `ph-medal` | Bell `ph-bell` | Home `ph-house` | User `ph-user` | Gear `ph-gear` | Sign Out `ph-sign-out`

### State Icons
Complete `ph-check-circle` (green) | Warning `ph-warning-circle` (yellow) | Error `ph-x-circle` (red) | Locked `ph-lock` (gray)

**Sizing:** 16px (micro) | 20px (small) | 24px (default) | 32px (large) | 48–64px (xlarge, use fill/duotone)

---

## Common Components

### Room Entry Card (Lobby)
- Full-color header (40% height) with white icon
- Room number badge (top-left pill, UPPERCASE)
- Room name (h3, navy, Montserrat Bold)
- Description (14px gray)
- Progress bar (if started)
- "Enter Room →" CTA (room color, solid)
- Hover: scale(1.02) + shadow-md + brighten
- States: Default | Hover | In Progress | Completed (green badge) | Locked (grayed, lock icon)

### Course Card (Inside Room)
- Thumbnail or subject image (top)
- Title (h4, navy)
- Duration + difficulty badge (12px caps)
- Progress ring (if started, room color)
- "Start" / "Continue" / "Review" button (room color)

### Progress Bar
- Track: `--color-border`
- Fill: room accent or success green
- Height: 6px, full radius
- Label: "18 of 24 courses"

### Form Input
- Height: 44px (touch target)
- Border: 1px `--color-border`, 8px radius
- Focus: `--shadow-focus` (teal ring)
- Label above field (never inside)

### Buttons
- Large: 48px height | Default: 40px | Small: 32px
- Hover: color darkens one step, shadow deepens
- Focus: visible teal ring
- Never aggressive shrink on press

---

## Layout & Spacing Rules

- **Content max-width:** 1280px, centered
- **Section breaks:** 48–96px vertical padding
- **Card padding:** 24px (--space-5) default
- **Mobile-first:** Design from 375px up
- **Sticky elements:** Help desk widget bottom-right (fixed), nav top
- **Gutters:** 8px base grid, 16–24px component padding

---

## Motion Guidelines

| Motion | Duration | Easing | Usage |
|--------|----------|--------|-------|
| Fast | 100ms | ease-out | Button hover, icon states |
| Base | 200ms | ease-in-out | Panel open/close, tabs |
| Slow | 350ms | ease-in-out | Page transitions, modals |
| Spring | 400ms | spring(1, 0.5) | Progress fill, badge unlock |

**Always respect `prefers-reduced-motion`.** Disable all transitions when set.

---

## Accessibility (WCAG 2.1 AA Minimum)

- **Color contrast:** 4.5:1 text, 3:1 large/UI
- **Touch targets:** 44x44px minimum
- **Focus states:** Visible focus ring (teal, `--shadow-focus`)
- **Form labels:** Always above input, never placeholder-only
- **Alt text:** Descriptive for all images
- **Keyboard nav:** Fully supported throughout
- **Videos:** Must include captions (HIPAA training content)
- **Screen readers:** ARIA roles on all dynamic components

---

## Design Tokens (CSS Variables)

```css
/* Colors */
--color-navy: #1E3A6E;
--color-teal: #2B8FA9;
--color-surface: #F4F6F9;
--color-border: #D0D8E8;
--color-room-cs: #3B7DD8;
--color-room-hipaa: #2BA89A;
--color-room-compliance: #2EAA6E;
--color-room-records: #7B5EA7;
--color-room-finance: #D4A017;
--color-success: #28A745;

/* Typography */
--text-display: 48px, 800 weight, Montserrat;
--text-h1: 36px, 700 weight, Montserrat;
--text-h2: 28px, 700 weight, Montserrat;
--text-h3: 22px, 600 weight, Montserrat;
--text-body: 16px, 400 weight, Inter;

/* Spacing */
--space-4: 16px;
--space-5: 24px;
--space-7: 48px;
--space-9: 96px;

/* Elevation */
--shadow-md: 0 4px 12px rgba(0,0,0,0.10);
--shadow-focus: 0 0 0 3px rgba(43,143,169,0.35);

/* Radius */
--radius-md: 8px;
--radius-lg: 16px;
--radius-full: 9999px;

/* Motion */
--motion-base: 200ms ease-in-out;
```

---

## Common Design Decisions

### "Should I use this color?"
✓ Navy for authority, headers, primary nav
✓ Teal for interactive states, secondary actions, highlights
✓ Room color when user is inside that room (progress bars, buttons, accents)
✗ Don't mix room colors on the same page (unless showing them as options)
✗ Don't invent new colors — stick to the palette

### "How do I show a room-specific action?"
Use the room's accent color for the button/CTA. If user is inside Room 3 (Compliance, green), buttons in that context should be green. Progress bars should be green. Highlights should be green. Color = room identity.

### "What weight of Montserrat should I use?"
- ExtraBold (800): Hero display text (48px+)
- Bold (700): Page titles (h1, h2), room names (h3 in cards)
- SemiBold (600): Section headers (h3, h4), labels, UI text
- Never Regular weight — use Inter for body copy

### "How much whitespace is enough?"
Generous. Section breaks should be 48–96px. Card padding 24px. The brand feels spacious and breathing.

### "Can I add a background texture?"
No. The brand is clean and flat. Solid fills only. Subtle room-color tints (5% opacity) are the only exception inside room pages.

### "Do I need to design for mobile?"
Yes. Mobile-first approach. Design for 375px, then expand. Healthcare workers access training between shifts — mobile is critical.

### "What happens when a learner completes a course?"
Progress bar fills to 100% (animate with spring motion). Checkmark badge appears (green, `ph-check-circle`). CTA changes from "Start" → "Review". On the room card, a completion badge appears top-right.

---

## File References

- **Brand Guide:** `BRAND-GUIDE.html` — Full visual guide with all colors, typography, components
- **Email Template:** `TEMPLATES-email.html` — Ready-to-use email design
- **Social Templates:** `TEMPLATES-social.html` — LinkedIn, Instagram, Twitter post templates
- **Presentation:** `TEMPLATES-presentation.html` — Slide deck + document header templates
- **Icon Library:** `ICON-LIBRARY.json` — Complete icon reference with usage rules
- **Spec Document:** `design-system-spec.md` — Authoritative v1.0 design specification

---

## How to Use This Skill

**When making design decisions:**
- Check the color palette first (is this color approved?)
- Verify typography (is this the right font/size/weight?)
- Check spacing rules (8px grid — does this align?)
- Confirm icon choice (is this a Phosphor icon?)

**When building components:**
- Use the design tokens (CSS variables)
- Respect the button styles and sizes
- Ensure touch targets are 44x44px minimum
- Always include focus states (teal ring)
- Test color contrast (4.5:1 for text)

**When creating marketing materials:**
- Use the template files (email, social, presentation)
- Match the voice and tone (warm authority, rule of three)
- Apply the room color if highlighting a specific room
- Use Phosphor icons exclusively
- Keep layouts clean and spacious

**When onboarding designers/developers:**
- Start with `BRAND-GUIDE.html`
- Share `ICON-LIBRARY.json` for icon lookups
- Reference `design-system-spec.md` for technical details
- Use templates as examples

---

## Contact & Updates

**Project Owner:** Healthcare Training Center
**Last Reviewed:** June 4, 2026
**Next Review:** Q3 2026

For questions or brand updates, reference the `design-system-spec.md` or return to the full brand guide.

---

*Created by Claude Code | Healthcare Training Center Design System v1.0*
