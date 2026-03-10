# Interface Skills

One skill, four modes. Surface interaction problems before users find them.

```bash
npx skills add alantippins/interface-skills
```

Works with Claude Code, Cursor, Windsurf, and [40+ other agents](https://github.com/vercel-labs/skills).

## Modes

| Mode | When to Use | Invoke |
|------|-------------|--------|
| **plan** | Before building | `/interface-skills plan` |
| **review** | PR review | `/interface-skills review` |
| **audit** | Deep codebase check | `/interface-skills audit` |
| **critique** | Screenshot/UI analysis | `/interface-skills critique` |

Add `--teach` to review or audit for verbose explanations:
```
/interface-skills review --teach
/interface-skills audit --teach
```

## The Laws

What makes software feel solid, intentional, and trustworthy.

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

## Examples

### Plan Mode

Before you write code, surface the decisions that need to happen.

```
> /interface-skills plan "Add delete button to item cards"

A few questions before we build:

**Reversibility:**
- Should deleted items go to trash (recoverable) or permanent?
- Confirmation dialog, undo toast, or both?

**Transparency:**
- What feedback after deletion? Toast? Animation?
```

### Review Mode

Quick output for PR review. Terse, actionable.

```markdown
## UX Review

⚠️ **Reversibility** — `src/components/ItemCard.tsx:42`
   Delete without undo. Add confirmation or soft delete.

⚠️ **Forgiveness** — `src/components/Form.tsx:15`
   Button not disabled during async. Double-submit possible.

✓ **Escape** — Modal has close button and ESC handler
```

### Audit Mode

Teaching-first review. Every finding explains the principle behind it.

```
> /interface-skills audit src/components/

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
🔴 BLOCKER: Delete without safeguard

📍 src/components/ItemCard.tsx:42

⚖️  PRINCIPLE: Law of Reversibility

🔧 FIX:
    Quick:  Add confirmation dialog
    Better: Undo toast (delay deletion 5s)
    Best:   Soft delete to trash
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

With `--teach`, adds full principle explanations to each finding.

### Critique Mode

Visual analysis for screenshots and UI mockups.

```
> /interface-skills critique [paste screenshot]

## Visual Critique

### First Impression
Clean structure with clear sections. Toggle states are ambiguous.

### Opportunities

🔴 **Critical:**
- Toggle states indistinguishable — Add clear on/off colors

🟡 **Important:**
- Sidebar darker than content — Use same bg with border

### Top 3 Actions
1. Fix toggle states
2. Add save feedback
3. Balance sidebar weight
```

## Try It

Install, run `/interface-skills audit` on something you're building, see what surfaces.

## License

MIT
