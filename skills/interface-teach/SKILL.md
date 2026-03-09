---
name: interface-teach
description: Learn the Five Laws of interaction safety with examples and explanations.
---

# Interface Teach

Deep educational explanations. For learning UX principles, not reviewing code.

---

## When to Use

- User wants to understand a principle
- Learning UX concepts
- Building intuition, not fixing code

---

## How It Works

User asks about a principle → Full lesson with examples, counter-examples, and related concepts.

---

## Principles Reference

The Five Laws of Interaction Safety:

1. **Reversibility** — Every action should be undoable or recoverable
2. **Forgiveness** — Software should assume human error and prevent harm
3. **Persistence** — User work should survive navigation, refresh, failure, and closing
4. **Transparency** — System state should be visible and understandable at all times
5. **Escape** — Users should always have a way out of any state

See `principles/interaction.md` for full details.

---

## Input Formats

```
/interface-teach Law of Reversibility
/interface-teach "Why do users need undo?"
/interface-teach forgiveness
/interface-teach "What makes good error handling?"
```

---

## Output Format

```markdown
# [Principle Name]

## The Core Idea
[One memorable sentence]

---

## Why This Matters

[2-3 paragraphs explaining:]
- The user psychology behind this
- What happens when it's violated
- What happens when it's done well

---

## Examples

### ✗ Violation
[Concrete example of doing it wrong]
- What the user experiences
- Why it fails

### ✓ Good Implementation
[Concrete example of doing it right]
- What the user experiences
- Why it works

---

## Detection

**What to look for in code:**
- [Pattern 1]
- [Pattern 2]

**What to look for in the UI:**
- [Manual check 1]
- [Manual check 2]

---

## Related Principles

- [Related Law 1] — [How they connect]
- [Related Law 2] — [How they connect]

---

## Quick Reference

| Severity | When |
|----------|------|
| 🔴 | [Blocker criteria] |
| 🟡 | [Warning criteria] |
| 🟢 | [Suggestion criteria] |

---

## Further Reading

- [Link or reference 1]
- [Link or reference 2]
```

---

## Example: Law of Reversibility

```markdown
# Law of Reversibility

## The Core Idea
Every action should be undoable or recoverable.

---

## Why This Matters

Users make mistakes. They click the wrong button, delete the wrong item,
submit before they're ready. This is not user error—it's human nature.
The question isn't whether mistakes happen, but what happens when they do.

When actions are irreversible, users develop anxiety. They hesitate before
clicking. They double-check obsessively. They lose trust in your app. Every
interaction carries risk, and risk creates friction.

When actions are reversible, users gain confidence. They explore freely.
They try things without fear. The cognitive load of "what if I mess up?"
disappears. Your app becomes a safe space to work, not a minefield.

---

## Examples

### ✗ Violation: Gmail circa 2004
Click delete → Email gone forever.
Users had to fish through trash. Accidental deletions caused panic.
The cost of a mistake was permanent loss.

### ✓ Good Implementation: Gmail today
Click delete → Email moves to trash → Toast: "Message deleted. [Undo]"
Users can immediately undo. Trash auto-purges after 30 days.
Accidents become minor inconveniences, not disasters.

### ✗ Violation: Form without confirmation
Click submit on wrong form → Data sent, no take-backs.
User realizes mistake immediately, but it's too late.
Anxiety on every submit button going forward.

### ✓ Good Implementation: Slack message editing
Send message → Can edit for hours → Can delete anytime.
Typos, wrong channels, regrettable messages—all fixable.
Users send freely without proofreading anxiety.

---

## Detection

**What to look for in code:**
- `onClick={() => delete(id)}` without confirmation/undo nearby
- Hard delete API calls (`DELETE /items/:id`) without soft delete option
- State changes with no history/undo mechanism
- Bulk operations without extra confirmation

**What to look for in the UI:**
- Delete buttons with no confirmation dialog
- No "undo" option after destructive actions
- No trash/archive as alternative to permanent delete
- Actions that immediately modify server state

---

## Related Principles

- **Law of Forgiveness** — Prevent mistakes from happening; Reversibility handles them after
- **Law of Transparency** — Users need to see what was undone and what state they're in
- **Peak-End Rule** — A recoverable mistake feels okay; an unrecoverable one ruins the experience

---

## Quick Reference

| Severity | When |
|----------|------|
| 🔴 Blocker | Delete with no safeguard at all |
| 🟡 Warning | Confirmation only (no undo or trash) |
| 🟢 Good | Undo toast, soft delete, or version history |

---

## Further Reading

- Laws of UX: https://lawsofux.com/
- Gmail's undo feature case study
- "Don't Make Me Think" by Steve Krug (Chapter on user mistakes)
```

---

## Key Principles for Teaching

1. **Start with the memorable version** — One sentence they'll remember
2. **Explain the psychology** — Why users feel this way
3. **Concrete examples** — Real products, real scenarios
4. **Both sides** — What bad looks like AND what good looks like
5. **Connect to other principles** — Build a mental model
6. **Make it actionable** — What to look for in their own work
