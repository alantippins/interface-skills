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

## Principles Reference

Before auditing, load these principles:

**Interaction (Five Laws):** See `principles/interaction.md`
- Reversibility, Forgiveness, Persistence, Transparency, Escape

**Visual:** See `principles/visual.md`
- States, Accessibility, Hierarchy, Layout, Motion

**AI Anti-patterns:** See `heuristics/ai-antipatterns.md`
- Common issues in AI-generated code

---

## Phase 1: Understand the App

Before checking anything, understand what users can DO:

- **Data types:** What entities exist? (users, posts, tasks, items)
- **Actions:** What can users do? (CRUD per entity)
- **Flows:** What multi-step processes exist? (onboarding, checkout, wizard)

This determines what to check.

---

## Phase 2: Auto-Detection

Scan code for pattern violations. Use grep/search for:

**Reversibility:**
- `onClick={() => delete` without confirmation/undo nearby
- Bulk operations without extra confirmation

**Forgiveness:**
- Submit buttons without `disabled={isLoading}`
- `.catch(() => setFormData({}))` — clears form on error

**Persistence:**
- `useState` without localStorage/API persistence
- No `onbeforeunload` for forms

**Transparency:**
- `await fetch` without try/catch
- `console.log` in onClick handlers
- No toast/feedback after async

**Escape:**
- `<Modal` without `onClose` prop
- Multi-step without back/cancel

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

For each finding, use this teaching format:

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
🔴 BLOCKER: [Brief description]

📍 [file:line]
   [code snippet]

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

⚖️  PRINCIPLE: [Law name]
    [Core idea in one sentence]

    [2-3 sentences explaining WHY this matters. What users feel.
    What happens when this is violated. Make it memorable.]

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

🔧 FIX (pick one):

    Quick:  [Minimal fix]
            → [One-liner description]

    Better: [More robust fix]
            → [One-liner description]

    Best:   [Ideal implementation]
            → [One-liner description]

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

---

## Phase 5: Summary

End with:

### What's Working
Note things done well. Reinforces good patterns.

### Priority Order
Rank findings:
1. 🔴 Blockers — Data loss, no escape, crashes
2. 🟡 Warnings — Missing safeguards with workarounds
3. 🟢 Suggestions — Polish opportunities

### Ship Checklist Reference
Point to manual tests they should run before shipping.

---

## Example Finding

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
🔴 BLOCKER: Delete without safeguard

📍 src/components/ItemCard.tsx:42
   <Button onClick={() => deleteItem(id)}>Delete</Button>

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

⚖️  PRINCIPLE: Law of Reversibility
    Every action should be undoable or recoverable.

    Users will make mistakes. They'll accidentally delete the wrong
    thing, misclick, or change their mind. When deletion is permanent
    and instant, that one wrong click causes real harm. Users learn
    to be anxious around your app instead of confident.

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

🔧 FIX (pick one):

    Quick:  Add confirmation dialog
            → window.confirm("Delete this item?")

    Better: Add undo toast
            → Show toast with undo link, delay actual deletion 5s

    Best:   Implement soft delete
            → Move to trash, auto-purge after 30 days

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

---

## Key Principles

1. **Teach, don't just flag** — Every finding is a learning moment
2. **Name the law** — Users remember "Reversibility" better than "add confirmation"
3. **Explain the user impact** — Not what's wrong technically, but how it feels
4. **Offer choices** — Quick/better/best lets them decide investment level
5. **Note what works** — Balance critique with recognition
