---
name: interface-skills
description: "Interface quality toolkit. Plan before building, review PRs, audit codebases, critique screenshots. Based on the Laws of Interface Quality."
argument-hint: "[plan | review | audit | critique] [--teach]"
---

# Interface Skills

By Alan Tippins

| Mode | When to Use | Invoke |
|------|-------------|--------|
| [Plan](plan.md) | Before building — surface concerns early | `/interface-skills plan` |
| [Review](review.md) | PR review — terse, actionable | `/interface-skills review` |
| [Audit](audit.md) | Full codebase check | `/interface-skills audit` |
| [Critique](critique.md) | Screenshot/UI analysis | `/interface-skills critique` |

## Modifiers

- `--teach` — Add principle explanations to findings. Works with review and audit.
  - `/interface-skills review --teach` — PR review with learning
  - `/interface-skills audit --teach` — Verbose teaching mode

## Routing

1. **plan** → Load [plan.md](plan.md)
2. **review** → Load [review.md](review.md) (check for --teach flag)
3. **audit** → Load [audit.md](audit.md) (check for --teach flag)
4. **critique** or screenshot pasted → Load [critique.md](critique.md)
5. **Ambiguous** → Ask which mode

## Foundation

All modes reference shared principles in `references/`:
- [references/interaction.md](references/interaction.md) — Laws of Interface Quality
- [references/visual.md](references/visual.md) — Visual & Technical Principles
- [references/heuristics.md](references/heuristics.md) — Universal UX Heuristics

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
