# Interface Principles — Quick Reference

One set of principles. Covers both visual craft and interaction safety.

---

## Visual Principles

*How interfaces should look and feel.* See [visual.md](./visual.md) for details.

### States
| Principle | Check |
|-----------|-------|
| Loading | Structural skeletons, not empty spinners |
| Empty | Clear action to populate |
| Error | Displayed adjacent to trigger |
| Interaction | Default, hover, active, focus, disabled |

### Accessibility
| Principle | Check |
|-----------|-------|
| Names | All controls labeled (aria-label for icons) |
| Keyboard | Tab reaches everything |
| Focus | Trapped in modals, restored on close |
| Contrast | 4.5:1 for text |

### Hierarchy
| Principle | Check |
|-----------|-------|
| Typography | 4 levels max, text-balance/pretty |
| Color | Single accent per view, gray for structure |
| Depth | One strategy (borders OR shadows OR elevation) |

### Layout
| Principle | Check |
|-----------|-------|
| Spacing | Consistent 4/8px scale |
| Mobile | h-dvh, safe-area-inset |
| Z-index | Documented scale |

### Motion
| Principle | Check |
|-----------|-------|
| Reduced motion | prefers-reduced-motion respected |
| Properties | Only transform/opacity |
| Duration | 200ms feedback, 150-300ms transitions |

---

## Interaction Principles

*How interfaces should behave.* See [interaction.md](./interaction.md) for details.

### The Laws

| Law | Core Question |
|-----|---------------|
| **Reversibility** | Can users recover from mistakes? |
| **Forgiveness** | Does the app prevent harm from errors? |
| **Persistence** | Does user work survive failure? |
| **Transparency** | Do users always know what's happening? |
| **Escape** | Can users always get out? |
| **Consistency** | Does the same action work the same way everywhere? |
| **Craft** | Does the interface show intentional choices? |
| **Recognition** | Can users see what they need, not remember it? |

### Quick Checks

| Law | Look For |
|-----|----------|
| Reversibility | Delete → confirmation/undo/trash |
| Forgiveness | Submit button → disabled during async |
| Persistence | Form state → survives refresh |
| Transparency | Async operations → try/catch + feedback |
| Escape | Modal → X + ESC + backdrop close |
| Consistency | Same gesture → same result everywhere |
| Craft | Design tokens → not hardcoded values |
| Recognition | Recent items visible → no memorization required |

---

## Severity Guide

| Level | When to Use |
|-------|-------------|
| 🔴 Blocker | Data loss, broken UX, accessibility failure, no escape |
| 🟡 Warning | Missing safeguard with workaround, inconsistent pattern |
| 🟢 Suggestion | Polish opportunity, not causing harm |

---

## Red Flags

Patterns that signal amateur work:

**Structural (🔴)**
- Missing loading/empty/error states
- Missing interaction states (hover, focus, disabled)

**Visual (🟡)**
- Mixed depth strategies
- Inconsistent spacing
- Multiple competing accent colors
- Harsh borders, dramatic shadows

**Behavioral (🔴)**
- Delete without confirmation
- No error handling on async
- State only in React state
- Modals without escape

**Craft (🟡)**
- Hardcoded colors/spacing instead of tokens
- Default fonts never changed
- Missing polish (hover, focus, transitions)

**Consistency (🟡)**
- Same action behaves differently in different places
- Platform conventions ignored
- Mixed terminology for same concepts

---

## For Each Skill

| Skill | Use This Reference For |
|------|------------------------|
| `/interface-plan` | Questions that surface principle violations early |
| `/interface-audit` | Teaching-first findings with full explanations |
| `/interface-review` | Terse PR comments with file:line references |
| `/interface-teach` | Deep explanations of individual principles |
