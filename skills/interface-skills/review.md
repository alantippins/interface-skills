# Review Mode

Interface quality review. Works on code, screenshots, or both.

---

## When to Use

- Checking interface quality (any input)
- PR review
- Screenshot feedback
- "What's wrong with this?"

---

## Input Types

**Code:** Read files, mentally render the interface from the code.

**Screenshot:** View image, critique what you see directly.

**Both:** Cross-reference — "code does X but visually Y"

---

## Detect Review Type

### Single Screen (Steps 0-6)
- One screenshot
- Single component or page
- No navigation/routing involved

### Flow Review (Steps 0-7)
Triggers when ANY of these are present:
- Multiple screenshots provided
- Figma URL with multiple frames
- User mentions "flow", "sequence", "steps", "journey", "wizard", "onboarding"
- Code includes router, navigation, or multi-step state

**When flow detected:** Add Step 7 (Flow Coherence) to the critique. Evaluate transitions, state continuity, progress indicators, and exit paths.

---

## Process

Load and follow [critique.md](critique.md) for the review methodology.

**For specific checks, reference:**
- [checklists.md](references/checklists.md) — States, accessibility, hierarchy, layout, motion, mobile, red flags
- [interaction.md](references/interaction.md) — The 8 Laws of Interface Quality

---

## Modifiers

`--teach` — Add principle explanations to each finding. See critique.md output format.

---

## Quick Reference

### Severity

- 🔴 **Blocker** — Data loss, no escape, accessibility blockers
- ⚠️ **Warning** — Missing safeguards, craft issues
- 🟢 **Polish** — Minor improvements

### The Laws

| Law | What to Look For |
|-----|------------------|
| Reversibility | Delete has safeguard |
| Forgiveness | Submit disabled during async |
| Persistence | State survives refresh |
| Transparency | Actions confirm, errors explain |
| Escape | Modals closeable, flows have back |
| Consistency | Same action = same result |
| Recognition | Options visible, not memorized |

### Flow-Specific (Step 7)

| Check | What to Look For |
|-------|------------------|
| Transition logic | Screens connect naturally |
| State continuity | Data persists across steps |
| Progress clarity | User knows where they are |
| Exit paths | Can abandon at any point |
| Error recovery | Can resume after failure |
