---
name: interface-skills
description: "Interface quality toolkit. Plan before building, review interfaces. Based on the Laws of Interface Quality."
argument-hint: "[plan | review] [--teach]"
---

# Interface Skills

By Alan Tippins

| Mode | When to Use | Invoke |
|------|-------------|--------|
| [Plan](plan.md) | Before building — surface concerns early | `/interface-skills plan` |
| [Review](review.md) | Check interface quality | `/interface-skills review` |

## Input

Review accepts:
- **Code** — analyze what the interface will be
- **Screenshot** — analyze what the interface is
- **Both** — comprehensive analysis

## Modifiers

- `--teach` — Add principle explanations to findings

## Routing

1. **plan** → Load [plan.md](plan.md)
2. **review** → Load [review.md](review.md)
3. **Screenshot pasted** → Load [review.md](review.md)
4. **Ambiguous** → Ask which mode

## Foundation

All modes reference shared principles in `references/`:
- [references/interaction.md](references/interaction.md) — Laws of Interface Quality
- [references/checklists.md](references/checklists.md) — States, accessibility, hierarchy, layout, motion, mobile

---

## Quick Reference

### The Laws of Interface Quality

1. **Reversibility** — Every action should be undoable or recoverable
2. **Forgiveness** — Software should assume human error and prevent harm
3. **Persistence** — User work should survive navigation, refresh, failure, and closing
4. **Transparency** — System state should be visible and understandable at all times
5. **Escape** — Users should always have a way out of any state
6. **Consistency** — The same action should work the same way everywhere
7. **Craft** — The interface should show intentional design choices, not defaults
8. **Recognition** — Show users what they need — don't make them remember

### Severity

- 🔴 **Blocker** — Data loss, no escape, crashes, accessibility blockers
- 🟡 **Warning** — Missing safeguards with workarounds, craft issues
- 🟢 **Suggestion** — Polish opportunities, minor consistency issues
