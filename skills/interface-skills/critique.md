# Critique Methodology

Systematic interface critique. Works on code, screenshots, or both.

**Reference files:**
- [checklists.md](references/checklists.md) — Technical checks (states, accessibility, mobile, red flags)
- [interaction.md](references/interaction.md) — The 8 Laws of Interface Quality

---

## Input Modes

**Screenshot:** View the image, critique what you see.

**Code:** Read files, mentally render the interface. Focus on what's inferrable: structure, spacing, color, typography, hierarchy, component organization, interaction patterns.

**Both:** Cross-reference — "code does X but visually Y"

**Live URL:** Use WebFetch for markup, combine with screenshots.

---

## Critique Process

### Step 0: Context

Before critiquing:
- **What is this?** — App type, screen purpose, target user
- **What emotional context?** — Stressful? Casual? High-stakes? Routine?

A divorce filing app demands different care than a podcast player.

### Step 1: First Impressions

One paragraph. Gut reaction. What stands out? What feels off? Be direct.

---

## The Questions

Work through these. Not every question applies to every interface — use judgment.

### General

- Is every element and decision intentional?
- Is it easy to understand the design?
- Are there paper cuts? Small issues that compound into negative experience.
  - Empty space while loading, wrong icon placement, inconsistent hover states, missing tooltips, missing placeholders, inconsistent spacing across screens
- Will it scale? What happens with more content, longer content, in-between states?
- Is it focused on essentials? What can be removed to support primary goals?

### Visual Style

- Are style and visual techniques suited to the concept and problem?
- Do colors, icons, and illustrations work together?
- Do all elements look like they belong together, even different types?
- Does typography support readability?

### Layout

- Does layout work across viewport sizes AND take unique advantage of each? (Not just "works at mobile" — does mobile get a better experience?)
- Is it clear there's more content to scroll/move to?
- Is the structure easy to understand?
- Are related elements visually related through alignment, grouping, hierarchy?
- Are visual relationships consistent throughout?

### Composition & Hierarchy

- Is attention drawn to important elements first?
- Does composition guide the eye through the design?
- Is density appropriate for context? (Office vs driving vs glancing)

### Interaction

Core questions:
- Does it help the user do their job?
- Does it speak user language, not system language?
- Are patterns consistent throughout and with existing functionality?
- Is it clear which elements are interactive?
- Does it communicate current state well?

**The Laws** — check these specifically (see [interaction.md](references/interaction.md) for depth):

| Law | Question |
|-----|----------|
| **Reversibility** | Can I undo actions? Is there a way out? |
| **Forgiveness** | Does it prevent mistakes? Handle errors gracefully? |
| **Persistence** | Does work survive refresh, navigation, failure? |
| **Transparency** | Do I get clear feedback? Do I know what's happening? |
| **Escape** | Can I exit any state? Close modals? Cancel flows? |
| **Consistency** | Same action = same result everywhere? |
| **Craft** | Intentional choices or defaults? |
| **Recognition** | Options visible, not memorized? |

Animation & touch:
- Are animations appropriate to concept?
- Do I wait for animations to finish?
- Does it support touch well?

### Flow Coherence

**When reviewing multiple screens or a sequence:**

- Do screens connect naturally? Is the path obvious?
- Does data persist across steps?
- Does user know where they are in the flow?
- Can user abandon/back out at any point?
- If something fails mid-flow, can they resume?
- Does the sequence tell a story?
- What happens on refresh mid-flow? Deep-link to step 3?

---

## Output Format

```markdown
## Context
[1-2 sentences on what this is and who it's for]

## First Impressions
[1 paragraph, direct]

## Findings

### [Category]
**[Issue]** — [Observation]. [Impact]. [Opportunity].

[Group by: General, Visual, Layout, Composition, Interaction, Flow]
[Include file:line for code issues]

## Top Opportunities
[3-5 highest-impact changes, ranked]
```

---

## Voice

**Be:**
- Specific — count things, name colors, cite lines
- Decisive — "This is overwhelming" not "might feel overwhelming"
- Impact-aware — connect observation to user effect
- Constructive — every problem paired with opportunity

**Don't:**
- Hedge — no "maybe," "perhaps"
- Be vague — no "feels off" without specifics
- Prescribe without reasoning — never "change X to Y" without why
- Pad with praise — if something works, say so specifically; don't manufacture positivity

**Tone:** Senior designer reviewing with a junior they respect. Direct, honest, wants the work to be great.

---

## Severity

Order findings by impact:

1. **Structural** — Information architecture, missing functionality, wrong mental model
2. **Behavioral** — How interface responds, flows, communicates
3. **Visual** — Color, type, spacing, shadows

Structural > Behavioral > Visual.

---

## Examples

**Visual:**
> **Competing backgrounds** — Four distinct background colors on one screen. Cards are white, sidebar is gray, header is blue-tinted, content area is off-white. They don't establish hierarchy — they fragment the layout. Pick a surface strategy and commit.

**Layout:**
> **Mobile doesn't adapt** — At 480px, the data table just shrinks. All 8 columns compress into illegibility. This is "works at mobile," not "good at mobile." Reorder to show the 2-3 most important columns, let users expand for detail.

**Interaction:**
> **Silent submit** — Button says "Save" but gives no feedback on click. User doesn't know if it worked. Add loading state during async, success confirmation after.

**Flow:**
> **Lost context on back** — User fills shipping address (step 2), clicks back to cart (step 1), returns — address fields empty. State not persisted across navigation.

**Paper cut:**
> **Hover inconsistency** — Primary buttons have hover states. Secondary buttons don't. Table rows are hoverable but don't show it until clicked. Small, but these add up to "unfinished."
