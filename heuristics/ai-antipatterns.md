# AI Code Anti-Patterns

Common issues in AI-generated code (Claude, GPT, Copilot). These are the patterns that get missed when building fast with AI assistance.

---

## The Core Problem

AI generates code that works in the happy path demo. It doesn't generate code that handles:
- What happens when things go wrong
- What happens when users make mistakes
- What happens when the network fails
- What happens when users leave and come back

These anti-patterns are training signal gaps, not AI limitations. As you find them, you're filling in what the training data missed.

---

## Anti-Pattern: State Only in React State

**What it looks like:**
```javascript
const [todos, setTodos] = useState([]);
const [formData, setFormData] = useState({ title: '', description: '' });
```

**The problem:** This state vanishes on refresh, tab close, or navigation. Users lose work they thought was saved.

**Principle violated:** Law of Persistence

**The fix:**
```javascript
// Quick: localStorage
const [todos, setTodos] = useLocalStorage('todos', []);

// Better: backend persistence with optimistic UI
const { data: todos, mutate } = useSWR('/api/todos');
```

**Detection pattern:** `useState` with no corresponding `localStorage`, `sessionStorage`, or API call for persistence.

---

## Anti-Pattern: No Error Handling Around Async

**What it looks like:**
```javascript
const handleSubmit = async () => {
  const result = await fetch('/api/submit', {
    method: 'POST',
    body: JSON.stringify(data)
  });
  setData(result);
}
```

**The problem:** When the fetch fails, nothing happens. Or worse, it crashes. Users see a frozen UI or error boundary.

**Principle violated:** Law of Transparency

**The fix:**
```javascript
const handleSubmit = async () => {
  setIsLoading(true);
  try {
    const result = await fetch('/api/submit', {
      method: 'POST',
      body: JSON.stringify(data)
    });
    if (!result.ok) throw new Error('Failed to submit');
    setData(await result.json());
    toast.success('Submitted successfully');
  } catch (error) {
    toast.error('Failed to submit. Please try again.');
    // Don't clear the form - let them retry
  } finally {
    setIsLoading(false);
  }
}
```

**Detection pattern:** `await fetch` or `await api.` without try/catch wrapper.

---

## Anti-Pattern: Console.log Placeholder Handlers

**What it looks like:**
```javascript
<Button onClick={() => console.log('delete clicked')}>Delete</Button>
<Button onClick={() => console.log('TODO: implement save')}>Save</Button>
```

**The problem:** Button looks clickable, does nothing. Users think the app is broken.

**Principle violated:** Law of Transparency

**The fix:** Either implement the handler or clearly disable the button:
```javascript
<Button onClick={handleDelete}>Delete</Button>
// OR
<Button disabled title="Coming soon">Save</Button>
```

**Detection pattern:** `console.log` inside onClick handlers, especially with "TODO" or "clicked" messages.

---

## Anti-Pattern: No Loading/Disabled State on Buttons

**What it looks like:**
```javascript
<Button onClick={handleSubmit}>Submit</Button>
```

**The problem:** Users click again because nothing happened. Double-submits, duplicate charges, race conditions.

**Principle violated:** Law of Forgiveness

**The fix:**
```javascript
<Button
  onClick={handleSubmit}
  disabled={isLoading}
>
  {isLoading ? 'Submitting...' : 'Submit'}
</Button>
```

**Detection pattern:** `<Button onClick={asyncFunction}>` without `disabled={isLoading}` nearby.

---

## Anti-Pattern: Delete Without Any Safeguard

**What it looks like:**
```javascript
<Button onClick={() => deleteItem(id)}>Delete</Button>
```

**The problem:** One wrong click permanently destroys user data. No confirmation, no undo, no recovery.

**Principle violated:** Law of Reversibility

**The fix (tiered):**
```javascript
// Quick: confirmation dialog
<Button onClick={() => {
  if (confirm('Delete this item?')) deleteItem(id);
}}>Delete</Button>

// Better: undo toast
<Button onClick={() => {
  setDeletedItem(item);
  showUndoToast('Item deleted', () => restoreItem(item));
  softDelete(id);
}}>Delete</Button>

// Best: soft delete to trash
<Button onClick={() => moveToTrash(id)}>Delete</Button>
```

**Detection pattern:** `delete`, `remove`, `destroy` in onClick without `confirm`, `setShowModal`, or undo logic nearby.

---

## Anti-Pattern: Optimistic UI Without Rollback

**What it looks like:**
```javascript
const handleToggle = async () => {
  setIsComplete(!isComplete); // Optimistic update
  await api.updateTodo(id, { isComplete: !isComplete });
}
```

**The problem:** Shows success, actually failed. User thinks item is saved, it's not.

**Principle violated:** Law of Transparency

**The fix:**
```javascript
const handleToggle = async () => {
  const previousValue = isComplete;
  setIsComplete(!isComplete); // Optimistic update
  try {
    await api.updateTodo(id, { isComplete: !isComplete });
  } catch {
    setIsComplete(previousValue); // Rollback
    toast.error('Failed to update. Please try again.');
  }
}
```

**Detection pattern:** State set before await without try/catch and rollback in catch block.

---

## Anti-Pattern: Hard-Coded Happy Path Only

**What it looks like:**
```javascript
const UserProfile = () => {
  const { data } = useFetch('/api/user');
  return <div>{data.name}</div>; // What if data is undefined?
}
```

**The problem:** First edge case = crash. Loading state, empty state, error state all cause runtime errors.

**Principle violated:** Law of Forgiveness

**The fix:**
```javascript
const UserProfile = () => {
  const { data, isLoading, error } = useFetch('/api/user');

  if (isLoading) return <Skeleton />;
  if (error) return <ErrorState message="Failed to load profile" />;
  if (!data) return <EmptyState message="Profile not found" />;

  return <div>{data.name}</div>;
}
```

**Detection pattern:** Data access without null check, loading check, or error check.

---

## Anti-Pattern: Modal Without Escape

**What it looks like:**
```javascript
<Modal open={isOpen}>
  <form onSubmit={handleSubmit}>
    <input />
    <Button type="submit">Submit</Button>
  </form>
</Modal>
```

**The problem:** User can't close the modal without submitting. No X, no ESC, no backdrop click.

**Principle violated:** Law of Escape

**The fix:**
```javascript
<Modal
  open={isOpen}
  onClose={() => setIsOpen(false)}
  closeOnEsc
  closeOnOverlayClick
>
  <form onSubmit={handleSubmit}>
    <button type="button" onClick={() => setIsOpen(false)}>Cancel</button>
    <input />
    <Button type="submit">Submit</Button>
  </form>
</Modal>
```

**Detection pattern:** `<Modal` without `onClose` prop or close button inside.

---

## Anti-Pattern: No Auth Check on Destructive Operations

**What it looks like:**
```javascript
// API route
export async function DELETE(req) {
  const { id } = await req.json();
  await db.delete(items).where(eq(items.id, id));
  return Response.json({ success: true });
}
```

**The problem:** Anyone can delete anything. No auth check, no ownership verification.

**Principle violated:** Law of Forgiveness (assumes good actors, punishes bad requests with data loss)

**The fix:**
```javascript
export async function DELETE(req) {
  const session = await getSession(req);
  if (!session) return Response.json({ error: 'Unauthorized' }, { status: 401 });

  const { id } = await req.json();
  const item = await db.query.items.findFirst({ where: eq(items.id, id) });

  if (item.userId !== session.user.id) {
    return Response.json({ error: 'Forbidden' }, { status: 403 });
  }

  await db.delete(items).where(eq(items.id, id));
  return Response.json({ success: true });
}
```

**Detection pattern:** DELETE/PUT handlers without `getSession`, `auth`, or ownership check.

---

## Detection Checklist

When reviewing AI-generated code, check for these patterns:

```
[ ] useState without persistence mechanism
[ ] await/fetch without try/catch
[ ] console.log in onClick handlers
[ ] Button onClick without disabled state
[ ] delete/remove without confirmation/undo
[ ] State update before await without rollback
[ ] Data access without loading/error/empty checks
[ ] Modal without onClose
[ ] API DELETE/PUT without auth check
```

---

## Why AI Generates These Patterns

1. **Training data bias:** Most code examples are minimal demos, not production code
2. **Context window limits:** Error handling is "extra" that gets trimmed
3. **Happy path prompts:** "Build a todo app" doesn't mention error handling
4. **Speed optimization:** Shorter = faster generation = better benchmarks

The skill of building robust software is in knowing what the demo code left out.
