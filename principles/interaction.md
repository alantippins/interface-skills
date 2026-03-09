# The Laws of Interface Quality

What makes software feel solid, intentional, and trustworthy.

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

## Law of Consistency

**The same action should work the same way everywhere.**

Users build mental models. When a swipe deletes in one place and archives in another, the model breaks. When your app works differently than every other app on the platform, users stumble. Consistency lets users transfer what they've learned.

**What violation feels like:** "Wait, why didn't that work?" "This button did something different last time." "This doesn't feel like an iPhone app."

### What to Check

| Check | What to Look For |
|-------|------------------|
| Platform conventions | iOS patterns on iOS, Android on Android, web standards on web |
| Internal consistency | Same gesture/action = same result everywhere in the app |
| Icon meanings | Trash means delete everywhere, not archive in one place |
| Terminology | Same words for same concepts throughout |

### Detection Patterns

```javascript
// 🟡 Inconsistent - swipe does different things
// In EmailList: swipe left = delete
// In TaskList: swipe left = complete
// Pick one meaning per gesture

// 🟡 Inconsistent - different confirmation patterns
// Screen A: delete immediately
// Screen B: confirmation dialog
// Screen C: undo toast
// Pick one and use it everywhere

// 🔴 Platform violation
// Custom gestures that conflict with system gestures
// Non-standard icons for standard actions
// Ignoring platform navigation patterns
```

### Severity

| Situation | Severity |
|-----------|----------|
| Conflicts with platform conventions | 🔴 Blocker |
| Same action behaves differently within app | 🟡 Warning |
| Minor terminology inconsistencies | 🟢 Suggestion |

---

## Law of Craft

**The interface should show intentional design choices, not unexamined defaults.**

Generic interfaces feel cheap. Users notice when something was designed vs. assembled from defaults. Craft isn't about being flashy — it's about every choice being deliberate. A minimal interface can show craft. A complex one can lack it.

**What violation feels like:** "This looks like a template." "This could be any app." "It works but feels unfinished."

### Where Defaults Hide

Defaults don't announce themselves. They disguise themselves as infrastructure — parts that feel like they "just need to work."

| Area | The Trap | Reality |
|------|----------|---------|
| **Typography** | "Pick something readable, move on" | Typography IS your design. The weight of a headline, the personality of a label — these shape feel before anyone reads a word. |
| **Navigation** | "Build the sidebar, get to real work" | Navigation IS your product. Where you are, where you can go, what matters most. A screen floating in space is a component demo, not software. |
| **Data display** | "You have numbers, show numbers" | A number on screen is not design. What does it mean? What will they do with it? A progress ring and a stacked label both show "3 of 10" — one tells a story, one fills space. |
| **Token names** | "Implementation detail" | Your CSS variables are design decisions. `--ink` and `--parchment` evoke a world. `--gray-700` and `--surface-2` evoke a template. |

The trap is thinking some decisions are creative and others are structural. Everything is design. The moment you stop asking "why this?" is when defaults take over.

### What to Check

| Check | What to Look For |
|-------|------------------|
| Typography intentional | Fonts selected for purpose, not defaulted |
| Color coherent | Defined palette with tokens, not random hex values |
| Spacing systematic | Consistent scale (4px/8px), not arbitrary numbers |
| Depth strategy consistent | ONE approach: borders-only, subtle shadows, layered, or surface shifts |
| Details finished | Hover states, focus rings, transitions polished |

### Detection Patterns

```css
/* 🟡 Unexamined defaults */
font-family: system-ui, sans-serif; /* Was this chosen or never changed? */
color: #333; /* Generic, no system */
padding: 13px 17px; /* Arbitrary, no scale */

/* ✅ Intentional choices */
font-family: var(--font-body); /* Part of a system */
color: var(--text-primary); /* Semantic token */
padding: var(--space-3) var(--space-4); /* On a scale */
```

### Quality Tests

Run these during review:

**Swap Test**
> Replace the typeface and colors with generic alternatives. Does it feel different?
> If no → you defaulted. The design has no voice.

**Token Test**
> Are values hardcoded or using a system?
> Hardcoded hex colors and pixel values = no design system.

### Severity

| Situation | Severity |
|-----------|----------|
| No design tokens, all hardcoded values | 🟡 Warning |
| Missing hover/focus/transition states | 🟡 Warning |
| Generic with no distinctive character | 🟢 Suggestion |

---

## Law of Recognition

**Show users what they need — don't make them remember.**

Memory is unreliable. When users have to remember commands, navigate without landmarks, or recall what they did last time, friction builds. Recognition is easy. Recall is hard. Show, don't tell.

**What violation feels like:** "Where was that setting?" "What did I name that thing?" "How do I do that again?"

### What to Check

| Check | What to Look For |
|-------|------------------|
| Recent items visible | Show what they worked on last |
| Options discoverable | Common actions visible, not buried in menus |
| Context preserved | Return to where they left off |
| Search over navigation | Let users find instead of browse for large sets |

### Detection Patterns

```javascript
// 🟡 Requires recall
// Keyboard-only commands with no menu equivalent
// Features only accessible if you know they exist
// No search in apps with lots of content

// ✅ Supports recognition
// Recent files, recent searches, recent contacts
// Command palette that shows available actions
// Breadcrumbs showing where you are
// Suggestions based on context
```

### Severity

| Situation | Severity |
|-----------|----------|
| Critical features only accessible via hidden gestures/shortcuts | 🔴 Blocker |
| No recent items in content-heavy apps | 🟡 Warning |
| No search in apps with 50+ items | 🟡 Warning |

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
