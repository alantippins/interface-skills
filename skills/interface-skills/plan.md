# Plan Mode

Question-driven spec refinement. Use **before** building to surface interaction and craft concerns early.

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

## Question Framework

For each feature, work through these categories.

### Intent Questions (ask first)

Before any implementation questions, establish intent:

- **Who is this human?** Not "users." The actual person. Where are they when they open this? What's on their mind?
- **What must they accomplish?** Not "use the feature." The verb. What action, what outcome?
- **What should this feel like?** Say it in words that mean something. "Clean and modern" means nothing. Warm like a notebook? Cold like a terminal? Dense like a trading floor? Calm like a reading app?

If you can't answer these with specifics, ask the user. Don't guess.

### Craft Questions (decisions to make early)

These decisions shape everything downstream. Make them explicit:

- **Depth strategy:** Borders-only, subtle shadows, layered shadows, or surface color shifts? Pick ONE.
- **Typography:** What typeface fits the feel? Don't default — select.
- **Color temperature:** Warm, cool, neutral? What colors exist in this product's world?
- **Information density:** Spacious or dense? What serves the user's task?

### Where Defaults Hide

Defaults sneak into these areas. Name them before they win:

| Area | The Trap | Ask Instead |
|------|----------|-------------|
| Typography | "Pick something readable" | What typeface fits this product's personality? |
| Navigation | "Build sidebar, add links" | How should users think about this space? |
| Data display | "Show the number" | What does this number mean? What will they do with it? |
| Token names | "Implementation detail" | Do these names evoke the product or a template? |

---

## Interaction Safeguard Questions

Work through each principle. Reference [references/interaction.md](references/interaction.md) for details.

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

### Consistency Questions
- Does this action work the same way elsewhere in the app?
- Are we following platform conventions (iOS/Android/web)?
- Will users expect this to behave like similar features they've used?

### Recognition Questions
- Can users see their options, or must they remember commands?
- Should we show recent items, suggestions, or search?
- How do users find this feature if they forget where it is?

---

## Output Format

Return a refined spec that includes:

```markdown
## Feature: [Name]

### Intent
- **Who:** [The actual person using this]
- **Task:** [What they must accomplish]
- **Feel:** [How it should feel — specific, not generic]

### Craft Decisions
- **Depth:** [borders-only / subtle shadows / layered / surface shifts]
- **Typography:** [Selected typeface and why]
- **Density:** [spacious / balanced / dense]

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

**Consistency:**
- [How this matches existing patterns]

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
