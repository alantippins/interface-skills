# Interface Skills

Surface interface quality concerns. Works on anything.

---

## Process

Load and follow [critique.md](critique.md) for the full methodology.

**References:**

- [checklists.md](references/checklists.md) — Visual coherence, states, accessibility, hierarchy, layout, motion, mobile, red flags
- [interaction.md](references/interaction.md) — Principles of Interface Quality

---

## Input Detection

| Input                                | Output                        |
| ------------------------------------ | ----------------------------- |
| Code                                 | Critique the implementation   |
| Screenshot                           | Critique the visual           |
| Code + Screenshot                    | Cross-reference both          |
| Spec / Plan / Feature description    | Surface unaddressed questions |
| Multiple screens or "flow" mentioned | Add flow coherence lens       |

---

## Modifiers

`--teach` — Add principle explanations to each finding.

---

## Quick Reference

### Severity

- 🔴 **Blocker** — Data loss, no escape, accessibility blockers
- 🟡 **Warning** — Missing safeguards, craft issues
- 🟢 **Suggestion** — Polish opportunities

### Composition

| Check | What to Look For |
|-------|------------------|
| Color strategy | Count colors; do they reinforce or fragment? |
| Type stack | Clear levels, one hero size |
| Depth approach | ONE strategy (borders OR shadows), not mixed |
| Entry point | One focal point, not everything competing |
| Density | Matches context and user frequency |
| Sequence | Clear visual path through the interface |

### The Principles

| Principle     | What to Look For                  |
| ------------- | --------------------------------- |
| Reversibility | Delete has safeguard              |
| Forgiveness   | Submit disabled during async      |
| Persistence   | State survives refresh            |
| Transparency  | Actions confirm, errors explain   |
| Escape        | Modals closeable, flows have back |
| Consistency   | Same action = same result         |
| Recognition   | Options visible, not memorized    |
