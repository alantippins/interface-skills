# Audit Mode

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
5. **Summarize** — What's working, priority order

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

### Standard Format (no --teach)

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
🔴 BLOCKER: [Brief description]

📍 [file:line]
   [code snippet]

⚖️  PRINCIPLE: [Law name]

🔧 FIX (pick one):

    Quick:  [Minimal fix]
    Better: [More robust fix]
    Best:   [Ideal implementation]

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

### With --teach Flag

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
🔴 BLOCKER: [Brief description]

📍 [file:line]
   [code snippet]

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

⚖️  PRINCIPLE: [Law name]
    [Core idea in one sentence]

    [2-3 sentences explaining WHY this matters. What users feel.
    The psychology behind the principle. What happens when it's
    violated vs. done well.]

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

## What to Check

Reference these for full details:
- [references/interaction.md](references/interaction.md) — Laws of Interface Quality
- [references/visual.md](references/visual.md) — Visual & Technical Principles
- [references/heuristics.md](references/heuristics.md) — Universal UX Heuristics

### Interaction Checks

| Law | Severity | What to Look For |
|-----|----------|------------------|
| Reversibility | 🔴 | Delete has safeguard, bulk actions protected |
| Forgiveness | 🔴 | Submit disabled during async, forms preserve on error |
| Persistence | 🔴 | Long forms have draft, state survives refresh |
| Transparency | 🔴 | Actions confirm completion, errors explain what to do |
| Escape | 🔴 | Modals closeable, flows have back/cancel |
| Consistency | 🟡 | Platform conventions, same action = same result |
| Craft | 🟡 | Typography intentional, tokens used, depth consistent |
| Recognition | 🟡 | Options discoverable, recent items visible |

### Visual Checks

| Category | Severity | What to Look For |
|----------|----------|------------------|
| Data States | 🔴 | Loading, empty, error states exist |
| Interaction States | 🔴 | All five states (default, hover, active, focus, disabled) |
| Accessibility | 🔴 | aria-labels, keyboard nav, no div buttons |
| Layout | 🔴 | h-dvh not h-screen, safe-area-inset |
| Motion | 🔴 | prefers-reduced-motion, compositor props only |
| Mobile | 🔴 | 44px touch targets, thumb zone |
| Typography | 🟡 | Four text levels, text-balance, tabular-nums |
| Hierarchy | 🟡 | Single accent, gray for structure |
| Depth | 🟡 | ONE strategy (borders OR shadows) |
| Spacing | 🟡 | Consistent 4px/8px scale |

### AI Anti-Pattern Checks

| Pattern | What Users Experience |
|---------|----------------------|
| State doesn't survive refresh | "I refreshed and everything is gone" |
| Silent failures | "I clicked submit and nothing happened" |
| Buttons that do nothing | "This button looks active but doesn't work" |
| Double-action risk | "I got charged twice" |
| Permanent actions without safeguards | "I accidentally removed everything" |
| Fake success | "It said it saved but my changes are gone" |
| Missing UI states | Crash on first load, blank on empty |
| Trapped states | "I can't close this popup" |

---

## Quality Tests

Run these during review:

### Swap Test
> Replace typeface and colors with generic alternatives. Feels different?
> If no → you defaulted.

### Squint Test
> Blur vision. Is hierarchy still perceivable?
> If no → relies on color alone.

### Spacing Test
> Same gaps for same relationships?
> If no → no design system.

### Token Test
> CSS variable names reflect product or templates?
> If generic → no intention.

---

## Key Principles

1. **Teach, don't just flag** — Every finding is a learning moment (especially with --teach)
2. **Name the law** — Users remember "Reversibility" better than "add confirmation"
3. **Explain the user impact** — Not what's wrong technically, but how it feels
4. **Offer choices** — Quick/better/best lets them decide investment level
5. **Note what works** — Balance critique with recognition
