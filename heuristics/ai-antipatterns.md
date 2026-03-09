# AI Design Anti-Patterns

Common UX issues in AI-generated interfaces. These are the patterns that get missed when building fast with AI assistance — described by what users experience, not implementation details.

---

## The Core Problem

AI generates interfaces that work in the happy path demo. It doesn't design for:
- What happens when things go wrong
- What happens when users make mistakes
- What happens when the network fails
- What happens when users leave and come back

These anti-patterns are training signal gaps, not AI limitations. As you spot them, you're filling in what the training data missed.

---

## Anti-Pattern: State That Doesn't Survive Refresh

**What users experience:** "I spent 20 minutes filling out this form, refreshed the page, and everything is gone." Or: "My cart was full yesterday, now it's empty."

**Why this happens:** AI defaults to temporary in-memory state. It doesn't think about persistence unless explicitly asked.

**What to check:**
- Does form data survive browser refresh?
- Do draft states persist when navigating away and back?
- Is important data saved to backend or localStorage?

**Principle violated:** Law of Persistence

---

## Anti-Pattern: Silent Failures

**What users experience:** "I clicked submit and nothing happened." Or: "The page froze and I don't know if it worked." Sometimes the action succeeded, sometimes it failed — users can't tell.

**Why this happens:** AI generates the success path but forgets error handling. When something breaks, the UI just stops.

**What to check:**
- Does every action provide visible feedback (success or failure)?
- Are error messages specific and actionable?
- Does the UI indicate when something is loading vs broken?

**Principle violated:** Law of Transparency

---

## Anti-Pattern: Buttons That Do Nothing

**What users experience:** "I clicked Save and nothing happened." Or: "This button looks active but doesn't work." Users think the app is broken.

**Why this happens:** AI generates placeholder handlers that log to console instead of doing real work. The UI looks complete but isn't.

**What to check:**
- Does every interactive element have a real action?
- Are unimplemented features visibly disabled or hidden?
- Do buttons provide feedback when clicked?

**Principle violated:** Law of Transparency

---

## Anti-Pattern: Double-Action Risk

**What users experience:** "I clicked once but it processed twice." "I got charged twice because nothing showed it was processing."

**Why this happens:** AI forgets to disable buttons during async operations. Users click again because they got no feedback.

**What to check:**
- Are buttons disabled while their action processes?
- Is there visual feedback (spinner, loading state) during async operations?
- Can users trigger duplicate submissions?

**Principle violated:** Law of Forgiveness

---

## Anti-Pattern: Destructive Actions Without Safeguards

**What users experience:** "I accidentally deleted everything and there's no undo." "One wrong click and my work is gone forever."

**Why this happens:** AI implements delete as a direct action without confirmation, undo, or soft delete. The happy path doesn't consider mistakes.

**What to check:**
- Do destructive actions have confirmation dialogs or undo options?
- Is there a way to recover from accidental deletion?
- Are dangerous buttons visually distinct from safe ones?

**Principle violated:** Law of Reversibility

---

## Anti-Pattern: Fake Success

**What users experience:** "The UI said it saved but when I came back, my changes were gone." The interface showed success, but the action actually failed.

**Why this happens:** AI implements optimistic UI updates without rollback on failure. Shows success immediately, never corrects when the backend rejects it.

**What to check:**
- When actions fail, does the UI revert to the actual state?
- Does success feedback only appear after server confirmation?
- Are users warned when their local state differs from server state?

**Principle violated:** Law of Transparency

---

## Anti-Pattern: Missing UI States

**What users experience:** Crash on first load. Error when the list is empty. Blank screen while data loads. The app breaks on any edge case.

**Why this happens:** AI codes for the "data exists" case. Loading, empty, and error states are afterthoughts that don't get implemented.

**What to check:**
- Is there a loading state while data fetches?
- Is there an empty state when no data exists?
- Is there an error state when fetching fails?
- Do all states guide users on what to do next?

**Principle violated:** Law of Forgiveness

---

## Anti-Pattern: Trapped States

**What users experience:** "I can't close this popup." "There's no way to go back." "I'm stuck in this wizard and can't exit."

**Why this happens:** AI forgets escape routes. Creates modals without close buttons, flows without back options, dialogs that trap focus.

**What to check:**
- Can every modal be dismissed (X button, ESC key, backdrop click)?
- Do multi-step flows have back/cancel options?
- Does browser back button work as expected?
- Can onboarding be skipped?

**Principle violated:** Law of Escape

---

## Anti-Pattern: Unprotected Destructive APIs

**What users experience:** "Someone deleted my account." Or worse, they never know — their data is simply gone.

**Why this happens:** AI generates working endpoints without auth checks or ownership verification. Anyone can call any action.

**What to check:**
- Do destructive actions verify the user is authorized?
- Is ownership checked before modifying data?
- Are API endpoints protected from unauthorized access?

**Principle violated:** Law of Forgiveness

---

## Quick Audit Checklist

When reviewing AI-generated interfaces, watch for these behaviors:

- [ ] State lost on page refresh
- [ ] No feedback when actions fail
- [ ] Buttons that appear active but do nothing
- [ ] No loading or processing indicators
- [ ] Delete actions without confirmation or undo
- [ ] Success shown before server confirmation
- [ ] No empty state when lists have no items
- [ ] No error state when data fails to load
- [ ] Modals with no way to close them
- [ ] Destructive actions anyone can trigger

---

## Why AI Generates These Patterns

1. **Training data bias:** Most code examples are minimal demos, not production interfaces
2. **Context window limits:** Error handling is "extra" that gets trimmed
3. **Happy path prompts:** "Build a todo app" doesn't mention error handling
4. **Speed optimization:** Shorter = faster generation = better benchmarks

The skill of building robust software is knowing what the demo version left out.
