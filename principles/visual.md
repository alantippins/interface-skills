# Visual & Technical Principles

Rules for interface quality. These apply to any project.

Severity: 🔴 Blocker | 🟡 Warning | 🟢 Suggestion

---

## States

The #1 gap in vibe-coded work. If it fetches data or takes action, it needs states.

### Data States

| Check | Severity | What to Look For |
|-------|----------|------------------|
| Loading state exists | 🔴 | Structural skeletons, not spinners in empty space |
| Empty state exists | 🔴 | Not blank; one clear action to fix it |
| Error state exists | 🔴 | Displayed adjacent to triggering action, not just console |
| Success feedback | 🟡 | User knows the action worked |

### Interaction States

| Check | Severity | What to Look For |
|-------|----------|------------------|
| All five states defined | 🔴 | default, hover, active, focus, disabled |
| Hover doesn't shift layout | 🟡 | No size/position changes on hover |
| Disabled has explanation | 🟡 | Why can't I click this? |
| Focus visible without mouse | 🟢 | Tab through the UI, focus always apparent |

---

## Accessibility

### Critical (🔴 Blockers)

| Check | What to Look For |
|-------|------------------|
| Accessible names | All controls labeled; icon buttons have `aria-label` |
| Keyboard accessible | Every interactive element reachable via Tab |
| No div/span buttons | Use `<button>` or accessible primitives |
| Focus trapped in modals | Can't Tab outside open dialogs |
| Escape closes dialogs | Standard expectation |
| Focus restored on close | Returns to trigger element |

### High Priority (🟡 Warnings)

| Check | What to Look For |
|-------|------------------|
| Semantic HTML | Proper heading levels, lists, landmarks |
| Form errors linked | `aria-describedby` connects error to input |
| Required fields announced | Screen readers know what's required |
| Color contrast 4.5:1 | Normal text minimum; 3:1 for large text |
| Live regions for errors | `aria-live` for critical errors |
| Loading announced | `aria-busy` on loading containers |

### Medium Priority (🟢 Suggestions)

| Check | What to Look For |
|-------|------------------|
| Alt text accurate | Describes content, not "image of..." |
| Decorative images hidden | `aria-hidden` or empty alt |

---

## Hierarchy & Layering

### Typography

| Check | Severity | What to Look For |
|-------|----------|------------------|
| Four text levels max | 🟡 | primary, secondary, tertiary, muted |
| Headings use `text-balance` | 🟡 | Prevents orphans |
| Body uses `text-pretty` | 🟡 | Better line breaks |
| Data uses `tabular-nums` | 🟡 | Numbers align in columns |
| Line length 65-75 chars | 🟢 | Optimal readability |
| Line height 1.5-1.75 | 🟢 | Body text breathes |

### Visual Hierarchy

| Check | Severity | What to Look For |
|-------|----------|------------------|
| Single accent color per view | 🟡 | One thing is primary |
| Gray for structure, color for meaning | 🟡 | Status, action, emphasis only |
| Squint test passes | 🟡 | Blur vision; hierarchy still perceivable |
| Headlines have presence | 🟢 | Weight + tight tracking |

### Layering

| Check | Severity | What to Look For |
|-------|----------|------------------|
| Subtle elevation shifts | 🟡 | Lightness changes, not color jumps |
| Inputs darker than surroundings | 🟡 | Signals interactivity |
| Single depth strategy | 🟡 | Borders OR shadows OR elevation; don't mix |
| Dropdowns above parent surface | 🟢 | One level up in elevation |

---

## Layout & Spacing

### Spacing

| Check | Severity | What to Look For |
|-------|----------|------------------|
| Consistent base unit | 🟡 | 4px or 8px scale throughout |
| Spacing test passes | 🟡 | Inconsistent spacing = no system |
| Symmetrical padding default | 🟡 | Asymmetry only when content requires |
| Use `size-*` for squares | 🟢 | Not `w-*` + `h-*` |

### Structure

| Check | Severity | What to Look For |
|-------|----------|------------------|
| `h-dvh` not `h-screen` | 🔴 | Accounts for mobile browser chrome |
| `safe-area-inset` on fixed elements | 🔴 | Respects notches/home indicators |
| Fixed z-index scale | 🟡 | Documented layers, not arbitrary numbers |
| No layout shift on load | 🟡 | Content stable as assets load |
| Sidebars same bg as canvas | 🟢 | Subtle border separation, not color |

---

## Motion & Animation

### Constraints

| Check | Severity | What to Look For |
|-------|----------|------------------|
| `prefers-reduced-motion` respected | 🔴 | Check and disable/reduce |
| Compositor props only | 🔴 | `transform`, `opacity`; never animate layout |
| Max 200ms for feedback | 🟡 | Interaction responses feel instant |
| 150-300ms for transitions | 🟡 | UI state changes |
| Looping animations pause off-screen | 🟡 | Performance + respect |

### Anti-patterns

| Check | Severity | What to Look For |
|-------|----------|------------------|
| No animated layout props | 🔴 | `width`, `height`, `top`, `left`, margins |
| No animation unless requested | 🟡 | Don't add decoration |
| Large surfaces don't animate | 🟢 | Full-screen, large images excluded |

---

## Mobile

Touch targets and mobile-specific patterns. Applies when viewport < 768px or touch device.

| Check | Severity | What to Look For |
|-------|----------|------------------|
| 44x44px minimum touch targets | 🔴 | Buttons, links, interactive elements |
| Thumb zone awareness | 🔴 | Primary actions reachable one-handed |
| No hover-only interactions | 🟡 | Everything works on tap |
| Inputs don't zoom on focus | 🟡 | Font size ≥ 16px |
| Bottom sheet over modal on mobile | 🟢 | Easier to reach/dismiss |

---

## Red Flags

Patterns that signal amateur work. Presence of these = immediate warning or blocker.

### Visual (🟡 Warnings)

- Harsh borders demanding attention
- Dramatic surface lightness jumps
- Pure white cards on colored backgrounds
- Decorative gradients (unless intentional brand)
- Multiple hues across surfaces (keep hue, shift lightness)
- Large radius on small elements
- Glow effects as primary affordances
- Emoji instead of consistent icon set (🟢)

### Structural

- Missing interaction states (🔴)
- Missing data states (loading/empty/error) (🔴)
- Mixed depth strategies (🟡)
- Dramatic drop shadows (🟡)
- Inconsistent spacing (🟡)
- Multiple accent colors competing (🟡)

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
