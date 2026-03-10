# Review Mode

Terse PR comments. Actionable findings for code review, not teaching.

---

## When to Use

- Reviewing a PR
- CI/automated checks
- When brevity matters

---

## Output Format

```markdown
## UX Review

### Interaction

⚠️ **Reversibility** — `src/components/ItemCard.tsx:42`
   Delete without undo. Add confirmation or soft delete.

⚠️ **Persistence** — `src/components/Form.tsx:15`
   Form state in useState only. Lost on refresh.

✓ **Transparency** — Error states show actionable messages
✓ **Escape** — Modal has close button and ESC handler

### Visual

⚠️ **States** — `src/components/UserList.tsx:23`
   No empty state. Show guidance when list is empty.

⚠️ **Accessibility** — `src/components/IconButton.tsx:5`
   Missing aria-label on icon-only button.

✓ **Motion** — prefers-reduced-motion respected

### Craft

⚠️ **Tokens** — `src/components/Card.tsx:12`
   Hardcoded colors (#3b82f6). Use design tokens.

✓ **Polish** — Hover and focus states present
```

---

## Format Rules

1. **Category header** — Group by principle type (Interaction / Visual / Craft)
2. **Status icon** — ⚠️ for issues, ✓ for passing
3. **Principle name in bold** — One word identifier
4. **File:line** — Clickable location reference
5. **One line problem + fix** — Minimal explanation

---

## Severity Markers

Use for serious issues only:

```markdown
🔴 **Blocker: Accessibility** — `src/Button.tsx:12`
   div with onClick. Use <button> for keyboard access.
```

Most issues are just ⚠️ warnings.

---

## What to Check

### Interaction (from references/interaction.md)

| Check | Pass/Fail Criteria |
|-------|-------------------|
| Reversibility | Delete handlers have confirmation/undo/trash |
| Forgiveness | Async buttons disabled during loading |
| Persistence | Important state survives refresh |
| Transparency | try/catch on async, errors explain next steps |
| Escape | Modals closeable, flows have back/cancel |
| Consistency | Same action = same behavior everywhere |
| Recognition | Options visible, not hidden behind memorization |

### Visual (from references/visual.md)

| Check | Pass/Fail Criteria |
|-------|-------------------|
| States | Loading, empty, error states present |
| Accessibility | aria-labels, keyboard nav, focus management |
| Hierarchy | Consistent typography, single accent |
| Layout | Consistent spacing, proper mobile handling |
| Motion | reduced-motion respected, compositor props only |

### Craft (from references/visual.md)

| Check | Pass/Fail Criteria |
|-------|-------------------|
| Tokens | Colors/spacing use tokens, not hardcoded values |
| Depth | ONE strategy (borders OR shadows), not mixed |
| Text hierarchy | Four levels defined, used consistently |
| Polish | Hover, focus, transition states present |

---

## Quick Reference Tables

### Interaction Principles

| Principle | What to Look For |
|-----------|------------------|
| Reversibility | Delete has safeguard (confirmation, undo, soft delete) |
| Forgiveness | Submit disabled during async, forms preserve on error |
| Persistence | Long forms have draft, state survives refresh |
| Transparency | Actions confirm completion, errors explain what to do |
| Escape | Modals have X/ESC/backdrop, flows have back/cancel |
| Consistency | Platform conventions, same action = same result |
| Recognition | Recent items visible, options discoverable |

### Visual Principles

**Data States (🔴):**
- Loading state exists
- Empty state exists
- Error state exists

**Interaction States (🔴):**
- All five states defined (default, hover, active, focus, disabled)

**Accessibility (🔴):**
- Accessible names (icon buttons have aria-label)
- Keyboard accessible (Tab reaches everything)
- No div/span buttons
- Focus trapped in modals, ESC closes, focus restored

**Layout (🔴):**
- `h-dvh` not `h-screen`
- `safe-area-inset` on fixed elements

**Motion (🔴):**
- `prefers-reduced-motion` respected
- Compositor props only (transform, opacity)

**Mobile (🔴):**
- 44x44px minimum touch targets
- Thumb zone awareness

---

## --teach Modifier

When invoked with `--teach`, add a "Why this matters" section after each finding:

```markdown
⚠️ **Reversibility** — `src/components/ItemCard.tsx:42`
   Delete without undo. Add confirmation or soft delete.

   **Why this matters:** Users will make mistakes. When actions are
   irreversible, users develop anxiety. Every interaction carries risk.
   Undo or soft delete turns mistakes into minor inconveniences.
```

Without `--teach`, keep findings terse. Reviewers can look up principles if curious.

---

## What NOT to Include

- Long explanations (save for audit mode)
- Principle rationales (unless --teach)
- Multiple fix options (just state what's needed)
- Teaching content (this is for experienced reviewers)

---

## Example: Full Review

```markdown
## UX Review: PR #142 — Add item deletion

### Interaction

⚠️ **Reversibility** — `src/components/ItemCard.tsx:42`
   Delete without safeguard. Add confirmation dialog.

⚠️ **Reversibility** — `src/api/items.ts:28`
   Hard delete. Consider soft delete to trash.

✓ **Forgiveness** — Delete button styled distinctly from primary actions
✓ **Transparency** — Toast shown after deletion

### Visual

⚠️ **States** — `src/components/ItemList.tsx:15`
   No empty state after last item deleted.

✓ **Accessibility** — Delete button has aria-label
✓ **Motion** — No animations added

---

**Summary:** 3 issues (2 interaction, 1 visual). Main concern is delete without recovery path.
```

---

## Integration Note

This format is designed for:
- PR comments (GitHub, GitLab)
- CI output
- Slack summaries

Keep it scannable. Link to full docs if user wants to learn more.
