# Interface Skills

Delete buttons with no undo. Forms that lose your work on refresh. Errors that say "Something went wrong" with no next step. Modals you can't escape.

Sound familiar?

These aren't bugs. They're gaps between "it works in the demo" and "it's ready for real users." After years of building design systems and shipping products, I kept seeing the same patterns slip through. So I turned them into skills.

## What This Is

Four skills that surface interaction problems before users find them:

| Skill | When to Use |
|-------|-------------|
| `/interface-plan` | Before building — asks the questions that prevent headaches later |
| `/interface-audit` | Reviewing existing code — explains the *why* behind each finding |
| `/interface-review` | PR review — terse output, no teaching |
| `/interface-teach` | Learning — deep explanations of the principles |

## Install

```bash
npx @anthropic-ai/claude-code skills add alantippins/interface-skills
```

Or clone locally:

```bash
git clone https://github.com/alantippins/interface-skills.git
npx @anthropic-ai/claude-code skills add ./interface-skills
```

## The Laws

What makes software feel solid, intentional, and trustworthy. Concrete questions you can check against any feature.

| Law | The Question |
|-----|--------------|
| **Reversibility** | Can users undo what they just did? |
| **Forgiveness** | Does the app protect users from their own mistakes? |
| **Persistence** | Does user work survive refresh, failure, or closing? |
| **Transparency** | Do users always know what's happening? |
| **Escape** | Can users always get out of any state? |
| **Consistency** | Does the same action work the same way everywhere? |
| **Craft** | Does the interface show intentional choices, not defaults? |
| **Recognition** | Can users see what they need, or must they remember? |

Each one maps to specific code and design patterns. The principle names the problem. The pattern tells you what to fix.

## How the Skills Work

### /interface-plan

Before you write code, surface the decisions that need to happen.

```
> /interface-plan "Add delete button to item cards"

A few questions before we build:

**Reversibility:**
- Should deleted items go to trash (recoverable) or permanent?
- Confirmation dialog, undo toast, or both?

**Transparency:**
- What feedback after deletion? Toast? Animation?
```

The goal isn't to slow you down. It's to make the decisions explicit *before* you're in the code and making assumptions.

### /interface-audit

Teaching-first review. Every finding explains the principle behind it, so you learn as you fix.

```
> /interface-audit src/components/

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
🔴 BLOCKER: Delete without safeguard

📍 src/components/ItemCard.tsx:42

⚖️  PRINCIPLE: Law of Reversibility
    Every action should be undoable or recoverable.

    Users will make mistakes. When deletion is permanent
    and instant, that one wrong click causes real harm.

🔧 FIX:
    Quick:  Add confirmation dialog
    Better: Undo toast (delay deletion 5s)
    Best:   Soft delete to trash
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

The tiered fixes let you pick based on how much you want to invest. Sometimes a quick fix is fine. Sometimes you need the full solution.

### /interface-review

Terse output for PR review. When you already know the principles and just need the findings.

```markdown
## UX Review

⚠️ **Reversibility** — `src/components/ItemCard.tsx:42`
   Delete without undo. Add confirmation or soft delete.

⚠️ **Forgiveness** — `src/components/Form.tsx:15`
   Button not disabled during async. Double-submit possible.

✓ **Escape** — Modal has close button and ESC handler
```

### /interface-teach

Deep explanations when you want to understand a principle, not just fix a violation.

```
> /interface-teach Law of Reversibility

# Law of Reversibility

Every action should be undoable or recoverable.

Users make mistakes. They click wrong, delete accidentally, submit early.
When actions are irreversible, users develop anxiety. They hesitate.
They double-check obsessively. Every interaction carries risk.

When actions are reversible, users gain confidence. They explore freely...
```

## What These Skills Catch

The same gaps I keep seeing:

- **Delete without recovery** — No confirmation, undo, or trash
- **State that doesn't persist** — Form data lost on refresh
- **Silent async failures** — No try/catch, no user feedback
- **Double-submit possible** — Buttons not disabled during loading
- **No escape from modals** — Missing close button, ESC handler
- **Placeholder handlers** — Buttons that `console.log` instead of acting

See [heuristics/ai-antipatterns.md](./heuristics/ai-antipatterns.md) for the full list with code examples.

## Try It

Install the skills, run `/interface-audit` on something you're building, and see what surfaces.

If something's missing or doesn't match your workflow, let me know. These are patterns I've refined from my own work — I'm curious what breaks in yours.

## License

MIT
