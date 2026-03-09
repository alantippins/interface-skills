---
name: interface-plan
description: Surface interaction concerns before you build. Asks the questions that prevent undo headaches later.
---

# Interface Plan

Question-driven spec refinement. Use **before** building to surface interaction concerns early.

---

## When to Use

- Starting a new feature
- Refining a user story
- Before writing any code

---

## How It Works

1. User describes what they want to build
2. You ask questions that surface principle violations before they're coded
3. Output: refined spec with interaction concerns addressed

---

## Principles Reference

Before asking questions, understand the Five Laws of Interaction Safety:

1. **Reversibility** — Every action should be undoable or recoverable
2. **Forgiveness** — Software should assume human error and prevent harm
3. **Persistence** — User work should survive navigation, refresh, failure, and closing
4. **Transparency** — System state should be visible and understandable at all times
5. **Escape** — Users should always have a way out of any state

See `principles/interaction.md` for full details.

---

## Question Framework

For each feature, work through these categories:

### Reversibility Questions
- Will users need to recover deleted items? How long should recovery be available?
- Are there bulk operations? What happens if they select the wrong items?
- Can changes be undone? History, version control, undo button?

### Forgiveness Questions
- What happens if users double-click submit?
- Can they put bad data in and recover gracefully?
- Are destructive actions distinguishable from safe ones?

### Persistence Questions
- If they refresh mid-form, what happens?
- If the API fails, is their input preserved?
- Should there be a draft/autosave?

### Transparency Questions
- How will they know it worked?
- What does the loading state look like?
- If it fails, what do they see? What can they do?

### Escape Questions
- Can they cancel at any point?
- If there's a modal, how do they close it?
- For multi-step flows, can they go back?

---

## Output Format

Return a refined spec that includes:

```markdown
## Feature: [Name]

### User Intent
[What they want to accomplish]

### Happy Path
[Normal flow]

### Interaction Safeguards

**Reversibility:**
- [How delete/changes are recoverable]

**Forgiveness:**
- [How double-submit is prevented]
- [How errors preserve input]

**Persistence:**
- [What survives refresh/failure]

**Transparency:**
- [Loading, success, error feedback]

**Escape:**
- [How users can exit any state]

### Questions Still Open
- [Anything that needs user decision]
```

---

## Example

**User says:** "I want to add a delete button to each item in my list."

**Plan mode response:**

> A few questions before we build this:
>
> **Reversibility:**
> - Should deleted items go to trash (recoverable) or be permanently removed?
> - If permanent, do you want a confirmation dialog, undo toast, or both?
>
> **Forgiveness:**
> - Should the delete button be visually distinct from other actions (red, icon only, positioned separately)?
>
> **Transparency:**
> - What feedback should users see after deleting? Toast notification? List animation?
>
> **Bulk operations:**
> - Will you eventually support multi-select delete? If so, we should design for it now.

After user answers:

```markdown
## Feature: Delete Items

### Happy Path
Click delete → confirmation dialog → item removed → toast confirmation

### Interaction Safeguards

**Reversibility:**
- Soft delete to trash (recoverable 30 days)
- Confirmation dialog: "Delete [item name]? [Cancel] [Delete]"
- Undo toast for 5 seconds after deletion

**Forgiveness:**
- Delete button: outline style, smaller than primary actions
- Positioned right side, away from edit/view buttons

**Persistence:**
- N/A (list is server state)

**Transparency:**
- Loading: button shows spinner during API call
- Success: toast "Item deleted" with undo link
- Error: toast "Couldn't delete. Try again." + item stays in list

**Escape:**
- Confirmation dialog has Cancel button and closes on ESC/backdrop
```

---

## Key Principles

1. **Ask, don't assume** — Surface decisions before coding
2. **Name the principle** — "For reversibility..." helps users learn
3. **Offer good defaults** — Suggest the safest approach as default
4. **Keep it conversational** — This is planning, not auditing
