# Claude Code — Healthcare Training Center Build Prompt

Paste this entire message as your first prompt in Claude Code.

---

## Your mission

You are building a production React app from a high-fidelity design handoff. The designs were created in Claude Design and exported as a complete bundle. Your job is to implement them pixel-faithfully.

## Step 1 — Read before you write anything

1. Read `healthcare-training-center/README.md` in full
2. Read `healthcare-training-center/project/Healthcare Training Center - Learner App.html` top to bottom — do not skim
3. Read every file it imports:
   - `healthcare-training-center/project/app/rooms.jsx`
   - `healthcare-training-center/project/app/components.jsx`
   - `healthcare-training-center/project/app/screens.jsx`
   - `healthcare-training-center/project/app/store.jsx`
   - `healthcare-training-center/project/app/lessons.jsx`
   - `healthcare-training-center/project/app/kit.css`
   - `healthcare-training-center/project/assets/colors_and_type.css`

Do not write a single line of code until you have read all of these.

## Step 2 — Confirm the stack with me

After reading, tell me:
- What stack you recommend (React + Vite, Next.js, etc.)
- How you plan to handle the design token system (`colors_and_type.css`)
- How you plan to handle routing (Lobby → Room → Lesson → Quiz)
- How you plan to handle the room accent recolor system
- What you plan to do with the isometric assets in `assets/iso/`

Wait for my confirmation before proceeding.

## Step 3 — Build

Once I confirm, implement the full app. The scope is:

1. **Lobby (Storefront)** — hero illustration with 5 clickable room hotspots, pop-out card + 3D tile, list-view toggle, support spaces strip
2. **Room screen** — accent-colored banner, course card grid, aside panel, back navigation
3. **Lesson screen** — left module rail, center content (video placeholder, prose blocks, key callouts, patient voice quotes), right notes panel
4. **Knowledge Check (Quiz)** — radio card questions, scoring (≥70% pass), per-question feedback, Mark Complete flow
5. **Chrome** — TopNav (recolors to room accent), mobile BottomNav (≤720px), floating Help Desk button
6. **Transitions** — room entry fade/slide (~150ms), pop-out card/tile animations (350ms, cubic-bezier(0.16,1,0.3,1), fill-mode: forwards), progress spring animations
7. **Persistence** — localStorage for progress, lobby mode, and per-course notes (with a note that production should replace progress/notes with API calls)
8. **Accessibility** — WCAG 2.1 AA, real button elements for hotspots/cards, Escape closes popout, quiz uses radio semantics, prefers-reduced-motion respected

## Key design constraints — do not deviate

- **Fonts:** Montserrat ExtraBold/Bold/SemiBold (headings + wordmark), Inter (body/UI)
- **Colors:** Navy `#1E3A6E`, Teal `#2B8FA9`, Surface `#F4F6F9`, Cream `#FAF7F2`
- **5 room accents:** CS `#3B7DD8`, HIPAA `#2BA89A`, Compliance `#2EAA6E`, Records `#7B5EA7`, Finance `#D4A017`
- **Spacing:** strict 8px grid
- **Shadows:** soft navy-tinted only — never black box-shadows
- **Icons:** Phosphor icon font from `assets/phosphor/` (swap to npm package in production)
- **Tweaks panel:** do NOT include in production build — prototype tool only
- **Animation fill-mode: forwards** is required on pop-out card/tile or they snap back to opacity:0

## Assets location

All assets are already in the bundle:
- `healthcare-training-center/project/assets/iso/` — lobby hero + 5 store tiles
- `healthcare-training-center/project/assets/phosphor/` — icon font
- `healthcare-training-center/project/assets/colors_and_type.css` — all design tokens

Copy these into the new project's public/assets folder.

## What not to do

- Do not copy-paste the Babel/in-browser React setup into production
- Do not use the Tweaks panel component
- Do not use black shadows
- Do not use the default browser focus outline — use `--shadow-focus` (teal ring)
- Do not skip `animation-fill-mode: forwards` on animated elements
- Do not skip `prefers-reduced-motion` gates on decorative animations

---

Start by reading the files listed in Step 1, then give me your stack recommendation.
