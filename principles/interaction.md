# The Five Laws of Interaction Safety

What should happen when users make mistakes, things fail, or context changes.

Severity: 🔴 Blocker | 🟡 Warning | 🟢 Suggestion

---

## Law of Reversibility

**Every action should be undoable or recoverable.**

Users will make mistakes. They delete the wrong thing, edit when they meant to view, submit before they're ready. When actions are reversible, users explore freely. When they're not, users hesitate.

**What violation feels like:** "I just deleted that and there's no way to get it back." Heart-pounding panic followed by resignation.

### What to Check

| Check | What to Look For |
|-------|------------------|
| Delete has safeguard | Confirmation, undo toast, or soft delete (trash) |
| Bulk actions protected | "Delete all" / "Remove selected" has extra confirmation |
| State changes reversible | History/undo mechanism for important changes |
| Archive over delete | Soft delete when permanent removal isn't required |

### Detection Patterns

```javascript
// 🔴 Dangerous - no safeguard
onClick={() => deleteItem(id)}
onClick={() => removeUser(userId)}

// ✅ Better - has protection
onClick={() => setShowDeleteConfirm(true)}
onClick={() => handleDeleteWithUndo(id)}
```

### Severity

| Situation | Severity |
|-----------|----------|
| No safeguard at all | 🔴 Blocker |
| Confirmation dialog only (no undo) | 🟡 Warning |
| Undo toast or soft delete | ✅ Good |

---

## Law of Forgiveness

**Software should assume human error and prevent harm.**

Users aren't careful. They double-click, fat-finger, paste wrong values, forget to save. Robust software anticipates this and prevents damage rather than punishing mistakes.

**What violation feels like:** "I clicked twice and it charged me twice." "The form rejected my input but won't tell me why."

### What to Check

| Check | What to Look For |
|-------|------------------|
| Submit disabled during async | Button disabled while processing |
| Destructive actions distinct | Delete styled differently than Submit |
| Input parsing permissive | Accept variations, normalize internally |
| Forms preserve on error | Don't clear data after API failure |

### Detection Patterns

```javascript
// 🔴 Dangerous - double-submit possible
<button onClick={submitForm}>Submit</button>

// ✅ Better - disabled during processing
<button onClick={submitForm} disabled={isLoading}>Submit</button>

// 🔴 Dangerous - clears form on error
.catch(() => setFormData({}))

// ✅ Better - preserves input
.catch((err) => setError(err.message))
```

---

## Law of Persistence

**User work should survive navigation, refresh, failure, and closing.**

Lost work is the deepest betrayal. Users invest time and attention. When the app loses their work—whether through a bug, a refresh, or accidental navigation—they lose trust permanently.

**What violation feels like:** "I spent 20 minutes on that form and it's gone." "I refreshed and everything reset."

### What to Check

| Check | What to Look For |
|-------|------------------|
| Long forms have draft state | localStorage/sessionStorage/autosave |
| State survives refresh | Not just React state |
| Failed submissions preserve input | Don't clear form on API error |
| Unsaved changes warning | `onbeforeunload` or router guards |

### Detection Patterns

```javascript
// 🟡 Risky - state lost on refresh
const [formData, setFormData] = useState({});

// ✅ Better - persisted
const [formData, setFormData] = useLocalStorage('draft', {});
```

---

## Law of Transparency

**System state should be visible and understandable at all times.**

Users shouldn't have to guess what happened, what's happening, or what will happen. Invisible state creates anxiety and mistrust. Clear feedback builds confidence.

**What violation feels like:** "Did it save?" "Is this loading or broken?" "What does this error mean?"

### What to Check

| Check | What to Look For |
|-------|------------------|
| Actions confirm completion | Toast/feedback after async operations |
| Errors explain what to do | Not just "Error" — what happened and next steps |
| Pending states visible | Loading indicators, disabled states |
| Sync status shown | "Saved" / "Saving..." / "Offline" |

### Detection Patterns

```javascript
// 🔴 Dangerous - silent failure
.catch(console.log)
.catch(() => {})

// 🔴 Dangerous - no feedback
await saveData(data);
// ...nothing visible happens

// ✅ Better
await saveData(data);
toast.success('Changes saved');
```

---

## Law of Escape

**Users should always have a way out of any state.**

Trapped users become angry users. Whether it's a modal, a wizard, or a process they started accidentally—there should always be an exit. Forced completions breed resentment.

**What violation feels like:** "I can't close this dialog." "There's no back button." "How do I cancel?"

### What to Check

| Check | What to Look For |
|-------|------------------|
| Modals have escape routes | X button, ESC handler, backdrop click |
| Multi-step flows have back/cancel | Not just "Next" and "Submit" |
| Browser back works | Proper history management |
| Onboarding skippable | Skip option available |

### Detection Patterns

```javascript
// 🔴 Missing escape
<Modal>
  <form onSubmit={submit}>
    <button type="submit">Submit</button>
    // No close button, no onClose prop
  </form>
</Modal>

// ✅ Better
<Modal onClose={handleClose} closeOnEsc closeOnOverlayClick>
  <button type="button" onClick={handleClose}>Cancel</button>
  <button type="submit">Submit</button>
</Modal>
```

---

## Related Laws (from Laws of UX)

These principles inform the five core laws above.

### Jakob's Law
Users expect your app to work like others they've used.
- Standard icons for standard actions (pencil for edit, trash for delete)
- Conventional keyboard shortcuts (ESC closes, Enter submits)
- Platform-native gestures

### Fitts's Law
Small, far targets are hard to hit.
- Destructive actions smaller/further from primary actions
- 44px minimum touch targets
- Primary actions in thumb zones

### Hick's Law
More choices = slower decisions.
- One clear primary CTA per view
- Group long menus
- Smart defaults that work for 80%

### Postel's Law
Be liberal in what you accept, conservative in what you produce.
- Accept phone number variations
- Parse multiple date formats
- Unicode in name fields

### Peak-End Rule
Experiences are judged by peak and end moments.
- Errors at the end feel worse than errors in the middle
- Success states should feel satisfying
- Clear completion feedback

### Doherty Threshold
Response under 400ms keeps users in flow.
- Optimistic UI for immediate feedback
- Loading states within 100ms
- Progress indicators for long operations

### Tesler's Law
Complexity can't be eliminated, only moved.
- Don't hide essential features behind "simple" UI
- Predictable behaviors over "magic"
- Progressive disclosure for power features

### Zeigarnik Effect
Incomplete tasks nag at the mind.
- Draft saves for long forms
- Progress indicators
- "Continue where you left off"

---

## How to Use These

When reviewing code:

1. **Identify the violation** — What's wrong?
2. **Name the principle** — Which law?
3. **Explain the impact** — What will users feel?
4. **Offer tiered fixes** — Quick, better, best

Naming the principle helps it stick. "Add a confirmation dialog" is forgettable. "Law of Reversibility" gives it a handle.
