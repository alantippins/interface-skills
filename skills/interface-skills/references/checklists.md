# Interface Checklists

Consolidated quality checks. Single source of truth for visual, technical, and accessibility standards.

Severity: 🔴 Blocker | 🟡 Warning | 🟢 Suggestion

---

## States

The #1 gap in vibe-coded work. If it fetches data or takes action, it needs states.

### Data States
- 🔴 **Loading state exists** — Structural skeletons, not spinners in empty space
- 🔴 **Empty state exists** — Not blank; one clear action to fix it
- 🔴 **Error state exists** — Displayed adjacent to triggering action, not just console
- 🟡 **Success feedback** — User knows the action worked

### Interaction States
- 🔴 **All five states defined** — default, hover, active, focus, disabled
- 🟡 **Hover doesn't shift layout** — No size/position changes on hover
- 🟡 **Disabled has explanation** — Why can't I click this?
- 🟢 **Focus visible without mouse** — Tab through the UI, focus always apparent

---

## Accessibility

### Critical
- 🔴 **Accessible names** — All controls labeled; icon buttons have `aria-label`
- 🔴 **Keyboard accessible** — Every interactive element reachable via Tab
- 🔴 **No div/span buttons** — Use `<button>` or accessible primitives
- 🔴 **Focus trapped in modals** — Can't Tab outside open dialogs
- 🔴 **Escape closes dialogs** — Standard expectation
- 🔴 **Focus restored on close** — Returns to trigger element

### High Priority
- 🟡 **Semantic HTML** — Proper heading levels, lists, landmarks
- 🟡 **Form errors linked** — `aria-describedby` connects error to input
- 🟡 **Required fields announced** — Screen readers know what's required
- 🟡 **Color contrast 4.5:1** — Normal text minimum; 3:1 for large text

### Medium Priority
- 🟡 **Live regions for errors** — `aria-live` for critical errors
- 🟡 **Loading announced** — `aria-busy` on loading containers
- 🟢 **Alt text accurate** — Describes content, not "image of..."
- 🟢 **Decorative images hidden** — `aria-hidden` or empty alt

---

## Hierarchy & Typography

### Typography
- 🟡 **Four text levels max** — primary, secondary, tertiary, muted
- 🟡 **Headings use `text-balance`** — Prevents orphans
- 🟡 **Body uses `text-pretty`** — Better line breaks
- 🟡 **Data uses `tabular-nums`** — Numbers align in columns
- 🟢 **Line length 65-75 chars** — Optimal readability
- 🟢 **Line height 1.5-1.75** — Body text breathes

### Text Hierarchy

Build four levels, not two:

| Level | Role | Example Use |
|-------|------|-------------|
| Primary | Default text | Body copy, main content |
| Secondary | Supporting text | Descriptions, help text |
| Tertiary | Metadata | Timestamps, counts, labels |
| Muted | Disabled/placeholder | Inactive states, hints |

- 🟡 **Four text levels defined** — Not just "text" and "gray text"
- 🟡 **Levels used consistently** — Same level = same meaning throughout
- 🟡 **Hierarchy visible without color** — Weight and size create hierarchy, not just color

### Visual Hierarchy
- 🟡 **Single accent color per view** — One thing is primary
- 🟡 **Gray for structure, color for meaning** — Status, action, emphasis only
- 🟡 **Squint test passes** — Blur vision; hierarchy still perceivable
- 🟢 **Headlines have presence** — Weight + tight tracking

### Layering & Depth

**Pick ONE depth strategy and commit:**

| Strategy | Feel | When to Use |
|----------|------|-------------|
| Borders-only | Clean, technical | Dense tools, data-heavy interfaces |
| Subtle shadows | Soft lift | Approachable products |
| Layered shadows | Premium, dimensional | Cards that need presence |
| Surface color shifts | Background tints | Hierarchy without shadows |

**Anti-pattern:** Mixing approaches. Don't use borders AND dramatic shadows.

- 🟡 **Single depth strategy** — ONE approach throughout, not mixed
- 🟡 **Subtle elevation shifts** — Lightness changes of a few percentage points, not dramatic jumps
- 🟡 **Sidebars same bg as canvas** — Subtle border separation, not different colors
- 🟡 **Inputs darker than surroundings** — Inset feel signals "type here"
- 🟢 **Dropdowns above parent surface** — One level up in elevation

---

## Layout & Spacing

### Spacing
- 🟡 **Consistent base unit** — 4px or 8px scale throughout
- 🟡 **Spacing test passes** — Inconsistent spacing = no system
- 🟡 **Symmetrical padding default** — Asymmetry only when content requires
- 🟢 **Use `size-*` for squares** — Not `w-*` + `h-*`

### Structure
- 🔴 **`h-dvh` not `h-screen`** — Accounts for mobile browser chrome
- 🔴 **`safe-area-inset` on fixed elements** — Respects notches/home indicators
- 🟡 **Fixed z-index scale** — Documented layers, not arbitrary numbers
- 🟡 **No layout shift on load** — Content stable as assets load
- 🟢 **Sidebars same bg as canvas** — Subtle border separation, not color

---

## Motion & Animation

### Constraints
- 🔴 **`prefers-reduced-motion` respected** — Check and disable/reduce
- 🔴 **Compositor props only** — `transform`, `opacity`; never animate layout
- 🟡 **Max 200ms for feedback** — Interaction responses feel instant
- 🟡 **150-300ms for transitions** — UI state changes
- 🟡 **Looping animations pause off-screen** — Performance + respect

### Anti-patterns
- 🔴 **No animated layout props** — `width`, `height`, `top`, `left`, margins
- 🟡 **No animation unless requested** — Don't add decoration
- 🟢 **Large surfaces don't animate** — Full-screen, large images excluded

---

## Mobile

Touch targets and mobile-specific patterns. Applies when viewport < 768px or touch device.

- 🔴 **44x44px minimum touch targets** — Buttons, links, interactive elements
- 🔴 **Thumb zone awareness** — Primary actions reachable one-handed
- 🟡 **No hover-only interactions** — Everything works on tap
- 🟡 **Inputs don't zoom on focus** — Font size ≥ 16px
- 🟢 **Bottom sheet over modal on mobile** — Easier to reach/dismiss

---

## Red Flags

Patterns that signal amateur work. Presence of these = immediate 🟡 or 🔴.

### Visual
- 🟡 Harsh borders demanding attention
- 🟡 Dramatic surface lightness jumps
- 🟡 Pure white cards on colored backgrounds
- 🟡 Decorative gradients (unless intentional brand)
- 🟡 Multiple hues across surfaces (keep hue, shift lightness)
- 🟡 Large radius on small elements
- 🟡 Glow effects as primary affordances
- 🟡 Different colors for sidebar vs canvas
- 🟢 Emoji instead of consistent icon set

### Structural
- 🔴 Missing interaction states
- 🔴 Missing data states (loading/empty/error)
- 🟡 Mixed depth strategies (borders AND shadows)
- 🟡 Dramatic drop shadows
- 🟡 Inconsistent spacing
- 🟡 Multiple accent colors competing
- 🟡 Only two text hierarchy levels

### Craft
- 🟡 Hardcoded hex colors instead of tokens
- 🟡 Default fonts never changed
- 🟡 Arbitrary spacing values with no scale
- 🟡 Missing polish — no hover, focus, or transition states
- 🟢 Token names that could belong to any project

---

## AI Anti-Patterns

Common UX issues in AI-generated interfaces.

### The Core Problem

AI generates interfaces that work in the happy path demo. It doesn't design for:
- What happens when things go wrong
- What happens when users make mistakes
- What happens when the network fails
- What happens when users leave and come back

### Detection Checklist

| Anti-Pattern | What Users Experience | Principle Violated |
|--------------|----------------------|-------------------|
| State doesn't survive refresh | "I refreshed and everything is gone" | Persistence |
| Silent failures | "I clicked submit and nothing happened" | Transparency |
| Buttons that do nothing | "This button looks active but doesn't work" | Transparency |
| Double-action risk | "I got charged twice" | Forgiveness |
| Permanent actions without safeguards | "I accidentally removed everything" | Reversibility |
| Fake success | "It said it saved but my changes are gone" | Transparency |
| Missing UI states | Crash on first load, blank on empty | Forgiveness |
| Trapped states | "I can't close this popup" | Escape |

Quick checks:
- [ ] State lost on page refresh
- [ ] No feedback when actions fail
- [ ] Buttons that appear active but do nothing
- [ ] No loading or processing indicators
- [ ] Delete actions without confirmation or undo
- [ ] Success shown before server confirmation
- [ ] No empty state when lists have no items
- [ ] No error state when data fails to load
- [ ] Modals with no way to close them

---

## Quality Tests

Manual tests for craft. Run these during review.

### Swap Test
> Would the design feel different if you replaced the typeface or layout with standard alternatives?

If no → you defaulted. 🟡

### Squint Test
> Blur your vision. Is hierarchy still perceivable without harsh jumps?

If no → hierarchy relies on color alone. 🟡

### Signature Test
> Can you identify 5 specific elements unique to this product's interface?

If no → generic. 🟢 (not broken, but no craft)

### Spacing Test
> Is spacing consistent throughout? Same gaps for same relationships?

If no → clearest sign of no design system. 🟡

### Token Test
> Do CSS variable names reflect this product's world or generic templates?

If generic → copy-paste without intention. 🟢
