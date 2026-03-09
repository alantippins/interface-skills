---
name: interface-audit
description: Teach-first review of existing code. Explains principles, not just findings.
---

# Interface Audit

Teaching-first codebase review. Verbose explanations that help users learn the principles, not just fix the code.

---

## When to Use

- Reviewing an existing codebase
- Learning what's wrong and why
- When you have time for deeper analysis

---

## How It Works

1. **Understand the app** — What entities exist? What actions can users take?
2. **Scan for violations** — Auto-detect patterns that break principles
3. **Walk through systematically** — Check each feature against each principle
4. **Output teaching findings** — Principle + explanation + tiered fixes

---

## Interaction Principles

What makes software feel solid, intentional, and trustworthy.

Severity: 🔴 Blocker | 🟡 Warning | 🟢 Suggestion

### Law of Reversibility

**Every action should be undoable or recoverable.**

Users will make mistakes. They delete the wrong thing, edit when they meant to view, submit before they're ready. When actions are reversible, users explore freely. When they're not, users hesitate.

**What violation feels like:** "I just deleted that and there's no way to get it back." Heart-pounding panic followed by resignation.

| Check | What to Look For |
|-------|------------------|
| Delete has safeguard | Confirmation, undo toast, or soft delete (trash) |
| Bulk actions protected | "Delete all" / "Remove selected" has extra confirmation |
| State changes reversible | History/undo mechanism for important changes |
| Archive over delete | Soft delete when permanent removal isn't required |

| Situation | Severity |
|-----------|----------|
| No safeguard at all | 🔴 Blocker |
| Confirmation dialog only (no undo) | 🟡 Warning |
| Undo toast or soft delete | ✅ Good |

### Law of Forgiveness

**Software should assume human error and prevent harm.**

Users aren't careful. They double-click, fat-finger, paste wrong values, forget to save. Robust software anticipates this and prevents damage rather than punishing mistakes.

**What violation feels like:** "I clicked twice and it charged me twice." "The form rejected my input but won't tell me why."

| Check | What to Look For |
|-------|------------------|
| Submit disabled during async | Button disabled while processing |
| Destructive actions distinct | Delete styled differently than Submit |
| Input parsing permissive | Accept variations, normalize internally |
| Forms preserve on error | Don't clear data after API failure |

### Law of Persistence

**User work should survive navigation, refresh, failure, and closing.**

Lost work is the deepest betrayal. Users invest time and attention. When the app loses their work—whether through a bug, a refresh, or accidental navigation—they lose trust permanently.

**What violation feels like:** "I spent 20 minutes on that form and it's gone." "I refreshed and everything reset."

| Check | What to Look For |
|-------|------------------|
| Long forms have draft state | localStorage/sessionStorage/autosave |
| State survives refresh | Not just React state |
| Failed submissions preserve input | Don't clear form on API error |
| Unsaved changes warning | `onbeforeunload` or router guards |

### Law of Transparency

**System state should be visible and understandable at all times.**

Users shouldn't have to guess what happened, what's happening, or what will happen. Invisible state creates anxiety and mistrust. Clear feedback builds confidence.

**What violation feels like:** "Did it save?" "Is this loading or broken?" "What does this error mean?"

| Check | What to Look For |
|-------|------------------|
| Actions confirm completion | Toast/feedback after async operations |
| Errors explain what to do | Not just "Error" — what happened and next steps |
| Pending states visible | Loading indicators, disabled states |
| Sync status shown | "Saved" / "Saving..." / "Offline" |

### Law of Escape

**Users should always have a way out of any state.**

Trapped users become angry users. Whether it's a modal, a wizard, or a process they started accidentally—there should always be an exit. Forced completions breed resentment.

**What violation feels like:** "I can't close this dialog." "There's no back button." "How do I cancel?"

| Check | What to Look For |
|-------|------------------|
| Modals have escape routes | X button, ESC handler, backdrop click |
| Multi-step flows have back/cancel | Not just "Next" and "Submit" |
| Browser back works | Proper history management |
| Onboarding skippable | Skip option available |

### Law of Consistency

**The same action should work the same way everywhere.**

Users build mental models. When a swipe deletes in one place and archives in another, the model breaks. When your app works differently than every other app on the platform, users stumble. Consistency lets users transfer what they've learned.

**What violation feels like:** "Wait, why didn't that work?" "This button did something different last time." "This doesn't feel like an iPhone app."

| Check | What to Look For |
|-------|------------------|
| Platform conventions | iOS patterns on iOS, Android on Android, web standards on web |
| Internal consistency | Same gesture/action = same result everywhere in the app |
| Icon meanings | Trash means delete everywhere, not archive in one place |
| Terminology | Same words for same concepts throughout |

| Situation | Severity |
|-----------|----------|
| Conflicts with platform conventions | 🔴 Blocker |
| Same action behaves differently within app | 🟡 Warning |
| Minor terminology inconsistencies | 🟢 Suggestion |

### Law of Craft

**The interface should show intentional design choices, not unexamined defaults.**

Generic interfaces feel cheap. Users notice when something was designed vs. assembled from defaults. Craft isn't about being flashy — it's about every choice being deliberate.

**What violation feels like:** "This looks like a template." "This could be any app." "It works but feels unfinished."

**Where Defaults Hide:**

| Area | The Trap | Reality |
|------|----------|---------|
| Typography | "Pick something readable, move on" | Typography IS your design. The weight of a headline, the personality of a label — these shape feel before anyone reads a word. |
| Navigation | "Build the sidebar, get to real work" | Navigation IS your product. Where you are, where you can go, what matters most. |
| Data display | "You have numbers, show numbers" | A number on screen is not design. What does it mean? What will they do with it? |
| Token names | "Implementation detail" | Your CSS variables are design decisions. `--ink` and `--parchment` evoke a world. `--gray-700` evokes a template. |

| Check | What to Look For |
|-------|------------------|
| Typography intentional | Fonts selected for purpose, not defaulted |
| Color coherent | Defined palette with tokens, not random hex values |
| Spacing systematic | Consistent scale (4px/8px), not arbitrary numbers |
| Depth strategy consistent | ONE approach: borders-only, subtle shadows, layered, or surface shifts |
| Details finished | Hover states, focus rings, transitions polished |

### Law of Recognition

**Show users what they need — don't make them remember.**

Memory is unreliable. When users have to remember commands, navigate without landmarks, or recall what they did last time, friction builds. Recognition is easy. Recall is hard.

**What violation feels like:** "Where was that setting?" "What did I name that thing?" "How do I do that again?"

| Check | What to Look For |
|-------|------------------|
| Recent items visible | Show what they worked on last |
| Options discoverable | Common actions visible, not buried in menus |
| Context preserved | Return to where they left off |
| Search over navigation | Let users find instead of browse for large sets |

### Related Laws (from Laws of UX)

- **Jakob's Law** — Users expect your app to work like others they've used
- **Fitts's Law** — Small, far targets are hard to hit (44px minimum touch targets)
- **Hick's Law** — More choices = slower decisions (one clear primary CTA per view)
- **Postel's Law** — Be liberal in what you accept, conservative in what you produce
- **Peak-End Rule** — Experiences are judged by peak and end moments
- **Doherty Threshold** — Response under 400ms keeps users in flow
- **Tesler's Law** — Complexity can't be eliminated, only moved
- **Zeigarnik Effect** — Incomplete tasks nag at the mind (draft saves, progress indicators)

---

## Visual Principles

### States

The #1 gap in vibe-coded work. If it fetches data or takes action, it needs states.

**Data States:**

| Check | Severity | What to Look For |
|-------|----------|------------------|
| Loading state exists | 🔴 | Structural skeletons, not spinners in empty space |
| Empty state exists | 🔴 | Not blank; one clear action to fix it |
| Error state exists | 🔴 | Displayed adjacent to triggering action, not just console |
| Success feedback | 🟡 | User knows the action worked |

**Interaction States:**

| Check | Severity | What to Look For |
|-------|----------|------------------|
| All five states defined | 🔴 | default, hover, active, focus, disabled |
| Hover doesn't shift layout | 🟡 | No size/position changes on hover |
| Disabled has explanation | 🟡 | Why can't I click this? |
| Focus visible without mouse | 🟢 | Tab through the UI, focus always apparent |

### Accessibility

**Critical (🔴 Blockers):**
- Accessible names — All controls labeled; icon buttons have `aria-label`
- Keyboard accessible — Every interactive element reachable via Tab
- No div/span buttons — Use `<button>` or accessible primitives
- Focus trapped in modals — Can't Tab outside open dialogs
- Escape closes dialogs — Standard expectation
- Focus restored on close — Returns to trigger element

**High Priority (🟡 Warnings):**
- Semantic HTML — Proper heading levels, lists, landmarks
- Form errors linked — `aria-describedby` connects error to input
- Color contrast 4.5:1 — Normal text minimum; 3:1 for large text
- Live regions for errors — `aria-live` for critical errors

### Hierarchy & Layering

**Layering & Depth — Pick ONE strategy:**

| Strategy | Feel | When to Use |
|----------|------|-------------|
| Borders-only | Clean, technical | Dense tools, data-heavy interfaces |
| Subtle shadows | Soft lift | Approachable products |
| Layered shadows | Premium, dimensional | Cards that need presence |
| Surface color shifts | Background tints | Hierarchy without shadows |

**Anti-pattern:** Mixing approaches. Don't use borders AND dramatic shadows.

**Text Hierarchy — Build four levels:**

| Level | Role | Example Use |
|-------|------|-------------|
| Primary | Default text | Body copy, main content |
| Secondary | Supporting text | Descriptions, help text |
| Tertiary | Metadata | Timestamps, counts, labels |
| Muted | Disabled/placeholder | Inactive states, hints |

### Layout & Spacing

| Check | Severity | What to Look For |
|-------|----------|------------------|
| `h-dvh` not `h-screen` | 🔴 | Accounts for mobile browser chrome |
| `safe-area-inset` on fixed elements | 🔴 | Respects notches/home indicators |
| Consistent base unit | 🟡 | 4px or 8px scale throughout |
| No layout shift on load | 🟡 | Content stable as assets load |

### Motion & Animation

| Check | Severity | What to Look For |
|-------|----------|------------------|
| `prefers-reduced-motion` respected | 🔴 | Check and disable/reduce |
| Compositor props only | 🔴 | `transform`, `opacity`; never animate layout |
| Max 200ms for feedback | 🟡 | Interaction responses feel instant |
| No animated layout props | 🔴 | `width`, `height`, `top`, `left`, margins |

### Mobile

| Check | Severity | What to Look For |
|-------|----------|------------------|
| 44x44px minimum touch targets | 🔴 | Buttons, links, interactive elements |
| Thumb zone awareness | 🔴 | Primary actions reachable one-handed |
| No hover-only interactions | 🟡 | Everything works on tap |
| Inputs don't zoom on focus | 🟡 | Font size ≥ 16px |

### Red Flags

**Visual (🟡):** Harsh borders, dramatic surface lightness jumps, pure white cards on colored backgrounds, mixed depth strategies

**Structural (🔴/🟡):** Missing interaction states (🔴), missing data states (🔴), inconsistent spacing (🟡), multiple accent colors competing (🟡)

**Craft (🟡):** Hardcoded hex colors instead of tokens, default fonts never changed, arbitrary spacing values

### Quality Tests

- **Swap Test:** Replace typeface/colors with generic alternatives. Feels different? If no → defaulted
- **Squint Test:** Blur vision. Hierarchy still perceivable? If no → relies on color alone
- **Spacing Test:** Same gaps for same relationships? If no → no design system
- **Token Test:** CSS variable names reflect product or templates? If generic → no intention

---

## AI Anti-Patterns

Common UX issues in AI-generated interfaces.

### The Core Problem

AI generates interfaces that work in the happy path demo. It doesn't design for:
- What happens when things go wrong
- What happens when users make mistakes
- What happens when the network fails
- What happens when users leave and come back

### Anti-Pattern Checklist

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
| Unguarded critical endpoints | "My data was modified without my action" | Forgiveness |

### Quick Audit Checklist

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

## Phase 1: Understand the App

Before checking anything, understand what users can DO:

- **Data types:** What entities exist? (users, posts, tasks, items)
- **Actions:** What can users do? (CRUD per entity)
- **Flows:** What multi-step processes exist? (onboarding, checkout, wizard)

---

## Phase 2: Auto-Detection

Scan code for pattern violations:

**Reversibility:** `onClick={() => remove` without confirmation/undo nearby
**Forgiveness:** Submit buttons without `disabled={isLoading}`
**Persistence:** `useState` without localStorage/API persistence
**Transparency:** `await fetch` without try/catch, no toast after async
**Escape:** `<Modal` without `onClose` prop
**Craft:** Hardcoded hex colors, system fonts, arbitrary spacing values

---

## Phase 3: Systematic Walk-Through

For each feature/entity, check against each principle:

```
📦 Feature: [Entity or Flow name]

⚖️  Law of Reversibility
    [✓] Can undo delete (soft delete implemented)
    [!] Edit has no undo/history

⚖️  Law of Persistence
    [?] State survive refresh? → Check storage usage
    [✓] Data persisted to database
```

---

## Phase 4: Output Findings

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
🔴 BLOCKER: [Brief description]

📍 [file:line]
   [code snippet]

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

⚖️  PRINCIPLE: [Law name]
    [Core idea in one sentence]

    [2-3 sentences explaining WHY this matters. What users feel.]

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

🔧 FIX (pick one):

    Quick:  [Minimal fix]
    Better: [More robust fix]
    Best:   [Ideal implementation]

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

---

## Phase 5: Summary

### What's Working
Note things done well. Reinforces good patterns.

### Priority Order
1. 🔴 Blockers — Data loss, no escape, crashes
2. 🟡 Warnings — Missing safeguards with workarounds
3. 🟢 Suggestions — Polish opportunities

---

## Key Principles

1. **Teach, don't just flag** — Every finding is a learning moment
2. **Name the law** — Users remember "Reversibility" better than "add confirmation"
3. **Explain the user impact** — Not what's wrong technically, but how it feels
4. **Offer choices** — Quick/better/best lets them decide investment level
5. **Note what works** — Balance critique with recognition
