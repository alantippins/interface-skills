# Critique Methodology

Systematic interface critique. Works on code, screenshots, or both.

**Reference files:**

- [checklists.md](references/checklists.md) — Technical checks (states, accessibility, visual coherence, mobile, red flags)
- [interaction.md](references/interaction.md) — The 8 Laws of Interface Quality

---

## Input Modes

**Screenshot:** View the image, critique what you see.

**Code:** Read files, mentally render the interface. Focus on what's inferrable: structure, spacing, color, typography, hierarchy, component organization, interaction patterns.

**Both:** Cross-reference — "code does X but visually Y"

**Live URL:** Use WebFetch for markup, combine with screenshots.

---

## Critique Process

### Step 0: Context & Emotional Lens

Before critiquing:

- **What is this?** — App type, screen purpose, target user
- **What job is this interface hired to do?** — What outcome is the user seeking? What progress are they trying to make? (Not feature, but outcome.)
- **What emotional context?** — Stressful? Casual? High-stakes? Routine?
- **What state is the user likely in?** — Anxious, focused, browsing, deciding?

**Carry this through:** Every finding should consider whether the interface respects or ignores the user's likely emotional state and whether it enables the job they came to do.

### Step 1: First Impressions

One paragraph. Gut reaction. What's the immediate emotional response this creates? Does it feel overwhelming, uncertain, confident, cluttered, calm? What stands out? What feels off? Be direct.

---

## The Lenses

These are ways of seeing, not boxes to check. Hold each lens up to the interface and notice what it reveals. Not every lens applies to every interface — use judgment.

### General

Start with the basics. Is every element earning its place? Anything that doesn't serve the user's goal is stealing attention from what does. Look for paper cuts — the small irritations that compound: empty space while loading, inconsistent hover states, missing placeholders, spacing that shifts between screens. Then stress-test mentally: what happens with twice the content? Half the content? Longer names? The edge cases reveal whether this was designed or just arranged.

### Visual Composition

Look at the interface as a composition, not a collection of items.

**Color.** Count the distinct colors — not "there's blue" but how many blues, how many grays, how many accents. The number tells you something. Four colors working together is intention; twelve scattered around is fragmentation. Then ask: what's each color's job? Accent should mean action or emphasis. When it also means decoration, it stops meaning anything. Look for the relationships — are colors working as a family (analogous, complementary, monochromatic) or just coexisting?

**Type.** List the sizes and weights you see. A clear scale has distinct levels — you can point to the headline, the body, the metadata, the labels. A muddy scale has sizes so close they compete rather than complement. Look for one hero size that establishes importance. If everything's shouting, nothing is. The type stack is the skeleton of hierarchy; if it's not working, nothing else will save it.

**Depth.** What's the strategy — borders, shadows, surface tints, or flat? The question isn't which one, it's whether there's ONE approach applied consistently. Mixed strategies (shadows here, borders there, tints elsewhere) signal "assembled from different sources." When depth is intentional, elevation communicates hierarchy: modals float above cards, cards float above the base surface. When it's not, things just... sit there.

**Weight.** The heaviest visual elements — boldest color, largest type, strongest contrast — should match the most important content. This is where intention becomes visible. When a decorative gradient carries more visual weight than the primary action, the hierarchy is lying. Squint at the screen: does importance survive the blur?

### Interface Composition

Now look at the interface as a system of attention and flow.

**Entry point.** Where does your eye land first? There should be ONE clear answer. If you're bouncing between the hero, the sidebar, the nav badges, and an inline CTA, nothing has claimed priority. The best interfaces are ruthless about this — Linear, Stripe, Apple all establish a single focal point and subordinate everything else. What would they do here?

**Density.** Is the amount of information appropriate for the context? A dashboard used daily can be dense — the user builds fluency. An onboarding screen should breathe — the user is orienting. Settings visited monthly should show the common case and hide the advanced. Density isn't good or bad; it's appropriate or not. Match it to expertise level and task frequency.

**Sequence.** If this takes more than one glance, what order do elements reveal themselves? A clear visual path guides the eye: headline → supporting text → action. A muddy path leaves the user to figure out the reading order on their own. Look at how groupings work — do they guide the sequence or interrupt it? Proximity and whitespace are doing choreography whether you intended it or not.

**Dead ends.** Are there elements that don't lead anywhere? Cards with no action, sections that exist but serve no purpose, information displayed with no next step. These are visual cul-de-sacs. Good interfaces always offer progressive disclosure — there's always somewhere to go next. If a user's attention lands on something, it should reward that attention.

### Interaction

This is where the interface becomes a conversation. Does it help the user do their job, or does it make them work around it? Does it speak their language or system language? Can they tell what's clickable? Do they know what state they're in?

**The Laws.** These are principles to hold while looking, not boxes to check. See [interaction.md](references/interaction.md) for the full framework. The short version:

- **Reversibility** — Can I undo what I just did? Confident users are users who can recover from mistakes.
- **Forgiveness** — Does it prevent errors before they happen? A disabled button during submission, a confirmation before delete.
- **Persistence** — Does my work survive? Refresh, navigation, network failure, closing the tab. Lost work is the deepest betrayal.
- **Transparency** — Do I know what's happening? Loading states, success confirmations, error explanations. Silent interfaces breed anxiety.
- **Escape** — Can I get out? Close the modal, cancel the flow, go back. Trapped users become angry users.
- **Consistency** — Does the same action work the same way everywhere? Or do patterns shift without reason?
- **Craft** — Are these intentional choices or unexamined defaults?
- **Recognition** — Are options visible, or do I have to remember them?

Not every Law applies to every interface. A static marketing page doesn't need Persistence. A checkout flow needs all of them. Use judgment.

**Motion.** If there's animation, is it earning its place? Motion should clarify, not decorate. And users should never wait for an animation to finish before they can act.

### Craft & Technical

Technical quality that users feel even when they can't name it. This is where you look at states, accessibility, and polish — the craft layer beneath the design.

For detailed technical checks, reference [checklists.md](references/checklists.md). The checklist covers interaction states (all five: default, hover, active, focus, disabled), data states (loading, empty, error), accessibility (keyboard navigation, focus visibility, semantics, contrast), motion constraints, and mobile considerations.

The craft lens isn't about checking boxes — it's about noticing whether the interface feels finished or feels like a prototype that shipped too early.

### Consistency & Conventions

Does the interface feel like one designer made it, or like it was assembled from different kits?

**Pattern consistency.** Are similar actions handled the same way throughout? Delete works like delete everywhere? Modals all close the same way? When patterns shift without reason, users lose trust — they can't predict what will happen next.

**Platform conventions.** Does it follow established patterns for its platform — iOS, Android, web? Deviations aren't wrong, but they should be intentional improvements, not accidents. Users carry expectations from every other app they use.

**Component reuse.** Look for elements that should be the same component but aren't. Two card styles that are almost identical. Buttons that look different in different contexts. List items that change treatment between screens. These inconsistencies signal "no system."

**Visual language cohesion.** Step back and ask: does this feel unified? Same voice, same hand, same intention throughout? Or does it feel like three different designers worked on it without talking?

### Flow Coherence

*This lens applies when reviewing multiple screens or a sequence.*

Flows have their own logic. Do the screens connect naturally — is the path obvious, or does the user have to figure out where they are? Does data persist across steps, or do they re-enter information? Do they know where they are in the process (step 2 of 4) and how much is left?

Look for escape routes. Can they abandon the flow at any point? Go back? What happens if something fails mid-flow — can they resume, or do they start over? What happens on refresh — does the URL deep-link to step 3, or does it dump them back at the beginning?

Good flows tell a story. There's a beginning (orientation), a middle (the work), and an end (completion, reward). Bad flows feel like a series of screens that happen to be connected.

---

## Output Format

```markdown
## Context

[1-2 sentences on what this is and who it's for]
[Name the emotional context: anxious checkout, routine dashboard, exploratory browse, etc.]

## First Impressions

[1 paragraph. Gut reaction. What's the overall impression? Name the emotion the interface creates — not just "good" or "confusing" but the specific feeling: "quiet confidence," "overwhelming density," "polished but cold." What stands out? What feels off? Be direct and honest, not tentative. This is the "noticing" step — seeing what's actually there, not what you expect to see.]

## Findings

Write each section as narrative prose with bolded issue names, not bulleted checklists. Lead with observation, then impact, then opportunity.

### Visual Composition

[Color, type, depth, weight distribution — analyzed as a composition, not a list of items. What's the color story? How does the type scale create hierarchy? Is there one depth strategy or several competing?]

### Interface Composition

[Entry point, density, sequence, dead ends. Where does the eye land? Is complexity revealed gradually? Are there visual cul-de-sacs?]

### Interaction

[The Laws — but only the ones that matter for this interface. Skip what doesn't apply. For each relevant Law, what's the finding?]

### Craft

[States, accessibility, polish. The technical quality that users feel even when they can't name it.]

### Consistency & Conventions

[Pattern consistency, platform conventions, component reuse, visual cohesion. Does it feel like one designer made this?]

### User Context

[Return to empathy. Answer these in prose, not bullets:]

- How does this interface make the user feel? Name the emotion precisely.
- What is the user's likely state of mind coming into this?
- Does the interface respect or ignore that state?

## Top Opportunities

[3-5 highest-impact changes, framed as opportunities, each in one sentence]

## High Craft

[What would exceptional look like here? Not just "good enough" — what would surprise the user with thoughtfulness? Explore 2-3 specific possibilities. This is where critique becomes generative.]

[Include file:line for code issues where relevant]
```

---

## Finding Format

Frame findings either as:

- **[Issue]** — [Observation]. [Impact]. [Opportunity].
- **Missing opportunity:** [What could be better]. [What's there now]. [The gap].

For interface design issues, prefer opportunity framing. "We're missing an opportunity to..." feels more actionable than a direct statement of what's wrong.

---

## Voice

The critique should read like a design conversation, not an audit checklist.

### Lead with observation

State what you see before judging it. "There are four background colors competing" comes before "this is fragmented." Let the reader see it too.

### Name emotions precisely

Not "confusing" — _what kind_ of confusing? "Overwhelmed," "uncertain," "under-whelmed," "lost," "no pull," "respect but not excitement," "correct without compelling," "calm competence." The specificity of the emotion is the quality of the insight.

### Frame as opportunity

"We're missing an opportunity to reward progress" lands differently than "progress feedback is missing." Both are true; one invites action.

### Explore what great would look like

Don't just identify gaps — imagine the possibilities. "High craft here would look like..." followed by 2-3 specific ideas. This is where critique becomes generative.

### Write in prose, not bullets

Narrative paragraphs with bolded issue names, not checklist items. The critique should flow like thinking, not scanning.

### Be specific and quantitative

Count elements. Name colors. Measure relative sizes. "14 distinct uses of purple" not "lots of purple." The precision earns trust.

### Be direct without being cold

Decisive: "This is overwhelming" not "might feel overwhelming." But pair directness with care — the goal is to make the work great, not to demonstrate cleverness.

### Connect everything to the user

Every observation should answer: "And that means the user feels...?" If you can't complete that sentence, the observation isn't ready.

---

### Don't

- **Hedge** — no "maybe," "perhaps," "it could be argued"
- **Be vague** — no "feels off" without saying exactly what and why
- **Prescribe without reasoning** — never "change X to Y" without the why
- **Pad with praise** — if something works, say so specifically; don't manufacture positivity
- **Write checklists** — think in compositions and relationships, not items to tick off
- **Be cold** — technical accuracy without warmth misses the point

---

### Tone

A staff product designer helping/teaching someone that wants the interface to be awesome. Direct, honest, but wanting to help them. The goal is to just help the user see what you are seeing and improve their work.

---

## Severity

Order findings by impact:

1. **Structural** — Information architecture, missing functionality, wrong mental model
2. **Behavioral** — How interface responds, flows, communicates
3. **Visual** — Color, type, spacing, shadows

Structural > Behavioral > Visual.

---

## Examples

**Visual Composition:**

> **Fragmented color story** — 14 distinct uses of purple across the page: navigation icons, card borders, badges, text highlights, gradients. Purple has become noise instead of signal. When everything is emphasized, nothing is. Pick 2-3 intentional uses and retire the rest.

**Interface Composition:**

> **No entry point** — Hero, sidebar promo, navigation badges, and inline CTA all compete at roughly equal visual weight. User's eye bounces between them with no clear starting point. The hero is theoretically the entry, but the animated sidebar pulls just as hard. Pick one focal point and subordinate everything else.

**Density:**

> **Dashboard dense, user casual** — This is a settings page users visit once a month, but it's laid out like a trading terminal. 40+ controls visible at once. A monthly visitor needs progressive disclosure — show the common case, reveal advanced on demand.

**Emotional mismatch:**

> **Checkout anxiety ignored** — User is about to spend money. The interface shows a wall of small text, multiple upsells, and a "Place Order" button that's the same size as secondary actions. This is the moment for confidence and focus. Strip everything that isn't "here's what you're getting, here's what you're paying, here's how to complete." The user's anxiety is a design constraint.

**Interaction:**

> **Silent submit** — Button says "Save" but gives no feedback on click. User doesn't know if it worked. Add loading state during async, success confirmation after.

**Flow:**

> **Lost context on back** — User fills shipping address (step 2), clicks back to cart (step 1), returns — address fields empty. State not persisted across navigation.

**Paper cut:**

> **Hover inconsistency** — Primary buttons have hover states. Secondary buttons don't. Table rows are hoverable but don't show it until clicked. Small, but these add up to "unfinished."

**Consistency:**

> **Interaction patterns shift** — Primary actions use filled buttons, except on the settings page where they're outlined. Modals close with X in the corner, except the confirmation dialog which only has "Cancel" and "Confirm" buttons. Each inconsistency is small, but together they signal "assembled, not designed."

**User Context:**

> **How does this make the user feel?** Respect, but not excitement. There's no anxiety, no confusion — but also no pull. The interface is _correct_ without being _magnetic_.
>
> **What state are they in?** Evaluative. Scanning many portfolios, skeptical by default, ready to bounce. Looking for signal.
>
> **Does the interface respect that state?** It respects their time — scannable, fast, no friction. But it doesn't reward curiosity. For a portfolio where the goal is to make someone want to learn more, "calm competence" might not be enough. The user needs a reason to click.

**High craft:**

> What would exceptional look like here? The form validation is technically correct, but where could we take it if we put in a little bit more?
>
> - A subtle progress indicator that grows as the form fills out
> - Smart defaults that pre-fill based on previous entries or context
>
> The current form works. These details would make it _feel_ like someone cared.
