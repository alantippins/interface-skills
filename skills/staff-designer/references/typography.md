# Typography

Typography is the foundation of interface design. It carries the majority of information. When it's wrong, the whole interface reads as wrong regardless of execution quality elsewhere — it's the highest-leverage fix available.

---

## The Four Jobs

Typography has four jobs. Every finding traces back to one.

**Hierarchy.** Can you identify four distinct levels — primary, secondary, tertiary, muted — without relying on color? Count the distinct sizes. Count the distinct weights. If everything lands at one or two levels, there's no scale. If there are six levels that look nearly identical, there's no hierarchy either.

**Rhythm.** Does the type scale have internal logic? Steps should have a mathematical relationship — a ratio or a defined set — not arbitrary jumps. Line-height should be consistent within context: tighter for headings, more open for body, tightest for labels. Spacing between text blocks should feel like it comes from the same system as the type itself.

Rhythm scores the spacing *inside type groups* — heading → description, label → value, paragraph → paragraph. Spacing between components, cards, or sections is layout, not typography. Flag it if it affects the read, but don't score Rhythm down for it.

**Measure.** Line length determines readability. 65–75 characters is the target for body copy. Shorter feels cramped. Longer forces the eye to track across too much ground. Headings can run shorter. Labels can run longer. The issue is when body copy runs wall-to-wall with no constraint.

**Signal.** Does weight, size, and color reinforce what's semantically important — or contradict it? A bold label competing with a bolder value reads as noise. A large decorative heading visually outranking a smaller primary action inverts the priority. Signal is about whether the visual language matches the semantic hierarchy.

---

## Orient

Before assessing typography, establish the context. This sets the bar — a data tool tolerates tighter measure and smaller type than a content app.

**Verify user-visibility first.** Before anything enters the audit, confirm every screen and component you're about to review is actually reachable by a user in the current build. Feature-flagged, route-gated, permission-gated, or unreleased code does not score and does not appear in findings. If it's worth mentioning at all, it belongs in Code Flags — not in the scored critique.

**Interface type:**

| Context | Base | Density | Scale approach | Measure | Key signal concern |
|---------|------|---------|----------------|---------|-------------------|
| Data-dense tool | 13–14px | Tight | Custom increments (12/14/16/20) | Low — fragments | Weight distinguishes interactive vs. static |
| Onboarding / task flow | 14–16px | Moderate | Custom (14/16/20/28) | Low — short copy | Size + color guide step and progress |
| App / product | 15–16px | Moderate | Modular 1.25–1.333 | Moderate | Hierarchy carries navigation and state |
| Content / reading | 16–18px | Open | Modular 1.25–1.333 | High — 65–75ch | Measure and line-height are primary |
| Marketing / landing | 16px base + display | Open | Modular 1.333–1.5 | Moderate | Display size creates emotional impact |

**Primary reading task** — scan, read, fill in, decide. Determines where measure and hierarchy matter most.

**Font fit** — Find the actual typeface first: check `tailwind.config`, `globals.css`, or the font import. Never guess or assume a framework default. Then evaluate on three axes:

- **Neutral ↔ Expressive** — Neutral types (Inter, DM Sans, Geist) recede behind content. Expressive types (Fraunces, Editorial New, Canela) carry personality. A data tool usually wants neutral. A consumer product may want expressive.
- **Geometric ↔ Humanist** — Geometric (Futura, Circular, DM Sans) feels precise and modern. Humanist (Inter, Gill Sans, Myriad) feels approachable and legible. Humanist generally reads better at small sizes.
- **Formal ↔ Friendly** — Weight contrast, aperture, x-height all signal register. High contrast = formal. Open aperture + large x-height = friendly.

If the font choice is wrong, name it first. A mismatched typeface is the highest-leverage fix — it colors every other decision.

**Pairing** — If multiple families are used: is the role clear? Serif for editorial, mono for code, sans for UI is the reliable pattern. Two sans-serifs rarely add enough to justify the complexity.

---

## Count

Before judging, count:
- How many distinct font sizes are used?
- How many distinct weights?
- How many distinct text colors?

State the counts. "6 sizes, 2 weights, 4 colors" gives you the raw material for the critique. Counts prevent vague claims.

---

## Audit

**Form the visual impression first.** Whether the input is a screenshot or code, establish what the screen looks like before reading implementation details. For code: mentally render it. What does the hierarchy look like? Does rhythm hold? Where does the eye go?

Run each of the four jobs. For each finding: what you see, why it matters, what it could be instead. Write findings as a designer, not a code reviewer.

**Screenshot input** — visual hierarchy only. Does the squint test pass? (Blur your vision — can you still identify 4 levels?) Is the measure constrained? Does weight track importance?

**Code input** — mentally render first, then read code for implementation flags only. Keep flags separate from findings. A raw `<p>` that renders identically to a `<Text>` component is a code flag, not a hierarchy failure. Token violations with no visible difference are code flags, not signal failures. If the user can't see it, it's not a finding.
