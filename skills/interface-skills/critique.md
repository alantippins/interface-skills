# Critique Mode

Visual and screenshot analysis. Systematic UI review based on design principles.

---

## When to Use

- Screenshot pasted into conversation
- User asks for visual feedback on a design
- Reviewing a live UI or mockup
- "What's wrong with this?" or "How can I improve this?"

---

## How It Works

1. **Context** — Understand what this is and who uses it
2. **First impressions** — Gut reaction before analysis
3. **Systematic review** — Walk through visual/interaction principles
4. **Top opportunities** — Prioritized, actionable improvements

---

## Step 1: Context

Before critiquing, establish:

- **What is this?** — App type, screen purpose, platform
- **Who uses it?** — User context, emotional state, task at hand
- **What's the intent?** — What should users feel or accomplish here?

If unclear, ask. Don't critique a login screen as if it were a dashboard.

---

## Step 2: First Impressions

Capture gut reaction (2-3 sentences):

> On first glance, [what stands out]. The overall feel is [emotional impression].
> [One thing that works] and [one thing that doesn't].

This isn't analysis yet — it's the immediate response a user would have.

---

## Step 3: Systematic Review

Work through these categories. Reference [references/visual.md](references/visual.md) for details.

### Visual Design

**Color:**
- Is there a coherent palette or random hex values?
- Single accent color or multiple competing?
- Gray for structure, color for meaning?
- Sufficient contrast (4.5:1 minimum)?

**Typography:**
- Intentional font selection or system default?
- Clear hierarchy (primary, secondary, tertiary, muted)?
- Appropriate weight/size relationships?
- Headings with presence (weight + tight tracking)?

**Depth & Shadows:**
- ONE consistent depth strategy?
  - Borders-only
  - Subtle shadows
  - Layered shadows
  - Surface color shifts
- Or mixed approaches (anti-pattern)?

**Spacing:**
- Consistent base unit (4px/8px)?
- Same gaps for same relationships?
- Symmetrical padding by default?

**Polish:**
- Hover states visible?
- Focus states present?
- Transitions smooth?

### Interface Design

**States:**
- Data states visible? (loading, empty, error, success)
- Interaction states present? (default, hover, active, focus, disabled)
- Disabled elements explain why?

**Feedback:**
- Actions confirm completion?
- Loading indicators present?
- Errors explain what to do?

**Hierarchy:**
- Clear visual priority?
- One primary CTA per view?
- Squint test passes?

**Navigation:**
- User knows where they are?
- Clear paths forward and back?
- Escape routes available?

### Consistency & Conventions

- Platform conventions followed?
- Internal consistency (same action = same result)?
- Standard icon meanings?
- Terminology consistent?

### User Context

- Touch targets adequate (44px)?
- Thumb zone awareness?
- Appropriate for user's emotional state?
- Cognitive load appropriate for task?

---

## Step 4: Output Format

```markdown
## Visual Critique

### First Impression
[2-3 sentences on gut reaction]

### What's Working
- [Specific positive 1]
- [Specific positive 2]

### Opportunities

**🔴 Critical:**
- [Issue] — [Why it matters] — [Fix]

**🟡 Important:**
- [Issue] — [Why it matters] — [Fix]

**🟢 Polish:**
- [Issue] — [Why it matters] — [Fix]

### Top 3 Actions
1. [Most impactful change]
2. [Second priority]
3. [Third priority]
```

---

## Voice Rules

### Be Specific
Not: "The typography could be better"
Yes: "The body text is 14px Inter at regular weight — increasing to 16px and using -0.01em letter-spacing would improve readability"

### Be Decisive
Not: "You might want to consider..."
Yes: "Change this to..."

### Be Factual First
Lead with observation, then interpretation:
- "The submit button is the same size as cancel" (fact)
- "This makes primary action unclear" (interpretation)

### Critique the Work, Not the Person
Not: "You didn't think about..."
Yes: "This screen doesn't address..."

---

## Common Patterns to Watch For

### Visual Red Flags (🟡)
- Harsh borders demanding attention
- Dramatic surface lightness jumps
- Pure white cards on colored backgrounds
- Multiple hues across surfaces
- Large radius on small elements
- Glow effects as primary affordances
- Different sidebar/canvas colors

### Structural Red Flags (🔴/🟡)
- Missing interaction states (🔴)
- Missing data states (🔴)
- Mixed depth strategies (🟡)
- Inconsistent spacing (🟡)
- Multiple competing accents (🟡)
- Only two text hierarchy levels (🟡)

### Craft Red Flags (🟡)
- Default/system fonts
- Arbitrary spacing values
- Generic token names
- Missing hover/focus/transitions

---

## Quality Tests to Run

### Swap Test
> Replace typeface and colors with generic alternatives. Feels different?
> If no → defaulted.

### Squint Test
> Blur vision. Is hierarchy still perceivable?
> If no → relies on color alone.

### Signature Test
> Can you identify 5 elements unique to this product?
> If no → generic.

---

## Example Critique

```markdown
## Visual Critique: Settings Dashboard

### First Impression
Clean structure with clear sections. The sidebar feels heavy compared to
the content area. Toggle states are ambiguous — hard to tell what's on vs off.

### What's Working
- Consistent spacing in form groups
- Clear section headings with appropriate weight
- Logical information architecture

### Opportunities

**🔴 Critical:**
- Toggle states indistinguishable — Add clear on/off colors and labels.
  Users shouldn't guess at state.
- No loading indicator on save — Add "Saving..." state to prevent
  double-submit anxiety.

**🟡 Important:**
- Sidebar darker than content creates visual weight imbalance — Use same
  background with subtle border separator.
- Form labels are same weight as values — Make labels secondary color
  to establish hierarchy.

**🟢 Polish:**
- Section headers could use tighter tracking (-0.02em) for more presence.
- Consider adding subtle hover states to form rows.

### Top 3 Actions
1. Fix toggle states — accessibility and usability blocker
2. Add save feedback — prevents anxiety and double-submit
3. Balance sidebar weight — improves overall visual harmony
```

---

## When Screenshot is Unclear

If the image is:
- **Too small:** Ask for higher resolution
- **Partial:** Ask what's cropped out
- **Ambiguous context:** Ask about user flow, purpose, platform

Don't guess at what you can't see.
