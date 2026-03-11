# Interface Skills

This skill helps you see and improve interface problems, and suggests what would take your interface to the next level.

```bash
npx skills add alantippins/interface-skills
```

---

## The Problem

Interfaces ship with problems that feel obvious in retrospect. The user deleted something and couldn't get it back. They filled out a form, navigated away, came back. Form fields are empty. They clicked a button and nothing happened. No feedback, no confirmation.

---

## How It Works

Give it anything. It adapts.

| Input            | Output                        |
| ---------------- | ----------------------------- |
| Code             | Critique the implementation   |
| Screenshot       | Critique the visual           |
| Spec or plan     | Surface unaddressed questions |
| Multiple screens | Add flow coherence            |

```
/interface-skills
```

No modes to remember. Just run it against whatever you're working on.

---

## The Principles

Principles to reference while looking at an interface.

**Reversibility.** Can users undo what they just did? Confident users are users who can recover from mistakes. When delete is permanent, users hesitate. When undo exists, they explore.

**Forgiveness.** Does the interface prevent errors before they happen? A disabled button during submission stops the double-click. A confirmation before delete catches the misclick. Forgiveness assumes humans make mistakes and designs around that fact.

**Persistence.** Does work survive? Refresh, navigation, network failure, closing the tab. Lost work is the deepest betrayal an interface can commit. Users remember the time they lost twenty minutes of writing forever.

**Transparency.** Do users know what's happening? Loading states, success confirmations, error explanations. Silent interfaces breed anxiety. When I click and nothing changes, did it work? Is it broken? Am I supposed to wait?

**Escape.** Can users get out? Close the modal, cancel the flow, go back. Trapped users become frustrated users. Every state should have an exit.

**Consistency.** Does the same action work the same way everywhere? When patterns shift without reason, users lose trust. They stop predicting what will happen next.

**Craft.** Are these intentional choices or unexamined defaults? The difference shows. Craft is visible in the details — the hover state that exists, the spacing that breathes, the animation that clarifies rather than decorates.

**Recognition.** Are options visible, or must users remember them? Humans are better at recognizing than recalling. Show them what they can do.

---

## The Lenses

Different ways of seeing the same interface. Not every lens applies to every screen. The skill uses judgement.

**Visual Composition.** Look at color, typography, depth, and weight as a composition, not a collection of items. Count the distinct colors. List the type sizes. Ask: is there one depth strategy or several competing? The squint test — does importance survive the blur?

**Interface Composition.** Where does the eye land first? Is there one clear entry point, or does everything compete for attention? Is the density appropriate for who's using this and how often? Are there dead ends — elements that exist but lead nowhere?

**Interaction.** This is where the principles live. Does the interface help the user do their job, or make them work around it? Can they tell what's clickable? Do they know what state they're in?

**Craft.** The technical quality users feel even when they can't name it. Interaction states (default, hover, active, focus, disabled). Data states (loading, empty, error). Accessibility. The polish that separates "it works" from "someone cared."

**Consistency.** Does the interface feel like one designer made it, or like it was assembled from different kits? Are similar actions handled the same way throughout? Do patterns shift without reason?

---

## Examples

### On Code

```
> /interface-skills src/components/Settings.tsx

## Context
Settings page for a B2B SaaS product. Users visit monthly, not daily.

## First Impressions
Dense. 40+ controls visible at once, but users only touch 2-3 per visit.
The density says "power tool" but the audience is casual visitors.

## Findings

### Visual Composition
**Color fragmentation** — Seven distinct grays across the page: card backgrounds,
borders, text, dividers. They're close enough to feel accidental rather than
systematic. Three grays would do the job.

### Interaction
**Transparency** — Save button gives no feedback. User clicks, nothing visible
happens. Did it work? Add loading state during async, success confirmation after.

**Persistence** — Form state doesn't survive navigation. User fills fields,
clicks a link in the sidebar to check something, comes back — fields empty.

## Top Opportunities
1. Add save feedback (loading → success)
2. Persist form state across navigation
3. Progressive disclosure — show common settings, hide advanced
```

### On a Plan

```
> /interface-skills [run against your Claude Code plan]

## Delete Button

### Questions

**Reversibility:**
- Should deleted items go to trash (recoverable) or permanent delete?
- Confirmation dialog, undo toast, or both?

**Transparency:**
- What feedback after deletion? Toast? Animation? Optimistic removal?

**Consistency:**
- How do other destructive actions work in this app? Match the pattern.

### Suggestions

If you want safe defaults: soft delete with 30-day recovery, confirmation
dialog for single items, undo toast for bulk operations.
```

Add `--teach` to include principle explanations with each finding.

---

## Severity

When technical issues appear:

- 🔴 **Blocker** — Data loss, no escape, accessibility blockers
- 🟡 **Warning** — Missing safeguards, craft issues with workarounds
- 🟢 **Suggestion** — Polish opportunities, minor consistency issues

---

## Foundation

The methodology lives in `critique.md`. Deep-dive references in `references/`:

- **interaction.md** — Principles of interface quality
- **checklists.md** — Technical checks (states, accessibility, mobile, red flags)

---

## Install

```bash
npx skills add alantippins/interface-skills
```

Works with Claude Code, Cursor, Windsurf, and [40+ other agents](https://github.com/vercel-labs/skills).

## License

MIT
