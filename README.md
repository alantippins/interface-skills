# Interface Skills

Delete buttons with no undo. Forms that lose your work on refresh. Errors that say "Something went wrong" with no next step. Modals you can't escape.

Sound familiar?

These aren't bugs. They're gaps between "it works in the demo" and "it's ready for real users." After years of building design systems and shipping products, I kept seeing the same patterns slip through. So I turned them into skills.

## What This Is

Four skills that surface interaction problems before users find them:

| Skill | When to Use | Output |
|-------|-------------|--------|
| `/interface-plan` | Before building | Questions that prevent headaches later |
| `/interface-audit` | Deep codebase review | Verbose findings with explanations + tiered fixes |
| `/interface-review` | PR review | One-line comments with file:line references |
| `/interface-teach` | Learning a principle | Full lesson with examples |

### Audit vs Review — Which One?

Both catch the same issues. The difference is **teaching vs shipping**.

| | **Audit** | **Review** |
|---|---|---|
| **When** | Onboarding a codebase, teaching a team, first deep dive | Mid-PR, you know the principles, need the checklist |
| **Output** | Multi-paragraph findings explaining *why* | One-line flags with file:line |
| **Fixes** | Tiered (quick/better/best) | Single suggestion |
| **Tone** | "Here's the principle and why it matters" | "Fix this" |

Use **audit** when you want to learn or teach. Use **review** when verbose = ignored.

## Install

```bash
# Interactive — choose which skills and agents
npx skills add alantippins/interface-skills

# Claude Code only
npx skills add alantippins/interface-skills -a claude-code

# Multiple specific agents
npx skills add alantippins/interface-skills -a claude-code -a cursor -a windsurf
```

Works with Claude Code, Cursor, Windsurf, and [40+ other agents](https://github.com/vercel-labs/skills).

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
