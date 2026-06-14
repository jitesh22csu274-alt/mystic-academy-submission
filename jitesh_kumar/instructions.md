# instruction.md
# Mystic Academy: The Lost Relic

**Type:** Developer Instruction Manual  
**Audience:** Freelance Developers / AI Coding Agents  
**Version:** 2.1  

---

## Project Summary

A short browser-based fantasy adventure game. Players arrive at a small magical academy, discover the Celestial Relic is missing, explore 3–4 connected locations, solve 2–3 puzzles, use one spell mechanic, and reach a closing scene that resolves the mystery. Total playtime: 15–25 minutes.

---

## What to Build

- Landing page with a Start Game button
- Character creation: name input + avatar selection (3–4 options)
- 3–4 connected academy locations with point-and-click or keyboard navigation
- Dialogue system with speaker name, portrait, and manual text advance
- 2–3 quests with a visible quest tracker that updates in real time
- 2–3 puzzles (rune matching, object interaction, or clue finding)
- One spell mechanic — learned mid-game, used once to unlock something or advance the story
- Story arc: introduction → investigation → short ending scene with genuine resolution
- Auto-save with local storage; Continue option on return
- Responsive UI for desktop and mobile
- Placeholder fantasy assets from free/licensed sources
- Source code, setup docs, and a working web build

## What NOT to Build

Multiplayer, combat, enemy AI, inventory system, achievements, XP/leveling, skill trees, advanced spells, custom artwork, voice acting, backend, cloud saves, leaderboards, monetization, app store deployment.

---

## Design Rules

1. Every location must contain at least one interactive object, one story detail, and one clue
2. UI must feel like part of the magical world — no generic flat-design components
3. The spell cast must have a visual effect and audio cue — it must feel magical
4. Every click must produce visible feedback — no silent interactions
5. Navigation must always be clear — players should never feel lost in a 3–4 room game
6. All dialogue must be purposeful — no filler text, no lorem ipsum anywhere in the build

---

## Locations

Pick 3–4 from the following. Each must connect logically to the next.

| Location | Purpose |
|---|---|
| Academy Entrance / Courtyard | Arrival point; first NPC; mystery introduced |
| Library | Clues in readable objects; one puzzle; librarian NPC |
| Spell Classroom | Spell mechanic introduced; professor NPC |
| Corridor / Hidden Passage | Transitional space; spell used to unlock path |
| Inner Chamber / Vault | Final location; ending scene plays here |

---

## Systems

**Navigation** — Animated transition between locations (fade, 500–700ms). Current location always labeled. All previously visited locations remain accessible.

**Dialogue** — Speaker name + portrait. Manual advance. No walls of text. Max 2 choices where branching is needed.

**Quests** — 2–3 quests (1 main, 1–2 side). Each has a name, short description, and 1–3 objectives. Quest tracker visible at all times. Completion triggers an on-screen notification.

**Puzzles** — 2–3 puzzles. Solutions consistent between sessions (no randomization). All clues exist within the game. Failed attempts show feedback, never lock the player out.

**Spell** — Exactly one spell. Learned through a story event. Triggers a particle/glow visual effect and a cast + resolution audio pair. Used at one specific story moment.

**Save** — Auto-save after quest updates, puzzles solved, locations visited, and ending reached. On reload, offer Continue or New Game. Handle missing/corrupt data gracefully.

---

## Technical Stack

| Item | Choice |
|---|---|
| Framework | React 18+ |
| Build | Next.js 14+ App Router (or Vite + React if simpler) |
| Language | TypeScript — strict mode on |
| Styling | Tailwind CSS |
| Animation | Framer Motion |
| State | Zustand |
| Storage | localStorage via custom hook with error handling |

**Folder structure (abbreviated):**

```
/src
  /app             # Routes and pages
  /components
    /ui            # Reusable primitives
    /game          # Scene, navigation, dialogue
    /puzzles       # Puzzle overlays
    /hud           # Quest tracker, spell button, location label
  /systems         # Quest, dialogue, puzzle, spell, save logic
  /data            # All game content as JSON (quests, dialogue, locations, puzzles)
  /stores          # Zustand stores
  /types           # TypeScript interfaces
  /hooks           # Custom hooks
/public/assets     # Audio, images, fonts
```

**Data-driven content is required.** All dialogue, quest definitions, location data, and puzzle configs must live in `/data` JSON files — never hardcoded in components.

---

## Visual Direction

- **Palette:** Deep indigo, midnight blue, gold, aged brass, arcane violet, warm parchment
- **Headings:** Cinzel or similar medieval serif
- **Body text:** Clean readable serif or sans-serif, 16px min desktop / 14px min mobile
- **Assets:** Illustrated/painted backgrounds, consistent portrait style, no stock photography
- **No mixing of flat-design UI with illustrated fantasy elements**

---

## Performance Targets

| Metric | Target |
|---|---|
| Lighthouse Performance | 85+ |
| Lighthouse Accessibility | 90+ |
| First Contentful Paint | < 1.5s |
| Largest Contentful Paint | < 2.5s |
| Time to Interactive | < 3s |

Test on mobile (mid-range Android, 4G) — not just desktop.

---

## Code Standards

- ESLint + Prettier — zero warnings on commit
- No `console.log` in production builds
- No `ts-ignore` — resolve all strict mode errors
- All exported components and functions have JSDoc comments
- No hardcoded game content in component files
- `README.md` must include setup, dev workflow, and env variable docs

---

## Deliverables

- Source code in a Git repo with clean commit history
- `README.md` — setup and local dev instructions
- `DATA_SCHEMA.md` — JSON data file schemas with field descriptions
- `LICENSES.md` — all third-party asset attributions
- `DEPLOYMENT.md` — deploy steps for Vercel or Netlify
- Tested production build

---

## Things to Avoid

- Adding features not listed under "What to Build"
- Hardcoded dialogue, quest names, or puzzle data inside component code
- Silent interactions — every click must produce a response
- Shrinking the desktop layout for mobile instead of redesigning it
- Generic RPG asset packs that don't match the visual direction
- Mixing icon packs or art styles
- An ending scene that says "To be continued" or stops without resolution

---

## Done When

- Complete flow works: landing → character creation → exploration → quests → puzzles → spell → ending
- Save and restore works across a full browser reload
- No placeholder text in the shipped build
- Runs without errors in Chrome, Firefox, Safari, and Edge
- Fully playable on mobile without horizontal scroll
- Lighthouse Performance 85+, Accessibility 90+
- A player can finish the full experience in 15–25 minutes without guidance

