# Critique Methodology

Surface interface quality concerns. Works on anything: code, screenshots, specs, plans.

**Reference files:**

- [checklists.md](references/checklists.md) — Technical checks (states, accessibility, visual coherence, mobile, red flags)
- [interaction.md](references/interaction.md) — Principles of Interface Quality

---

## Detect Input Type

**Artifact** (code, screenshot) → Critique what exists. Output: findings, opportunities.

**Spec/Plan** (feature description, Claude Code plan, PRD, user story) → Surface what's unaddressed. Output: questions, gaps.

The principles and lenses apply to both. The output format adapts.

---

## Input Modes

**Screenshot:** View the image, critique what you see.

**Code:** Read files, mentally render the interface. Focus on what's inferrable: structure, spacing, color, typography, hierarchy, component organization, interaction patterns.

**Both:** Cross-reference — "code does X but visually Y"

**Spec/Plan:** Read the description, surface interaction concerns that haven't been addressed.

---

## Critique Process

### Step 0: Read the room

**Working from a single screenshot with no other context? Ask first.** Before running through the bullets below, post one question: *What is this and what does it do? One sentence is fine.* Then proceed once the user has answered. This is the cheapest way to catch the kind of fundamental misread that no amount of careful looking will fix — the device frame that's actually the product concept, the flat rectangle that's actually a designed button, the "high craft" section that recommends things already shipped. If the input is code, a spec, or a screenshot with context already provided, skip the question and go straight to the bullets.

Then get oriented:

- **The screen** — what does it do, who's it for, where does it sit in the product?
- **The job** — what did the user come here to get done? (The outcome, not the feature.)
- **The headspace** — what state are they in when they show up? Anxious, focused, browsing, deciding, distracted, under pressure. Pick the specific word.

**Carry this through.** Every finding should ask whether the interface respects or ignores that state.

### Step 1: What I'm seeing

Not a gut reaction. A take. 2-3 paragraphs of connective, opinionated narrative that tells the story across findings before you break them into categories. Hard cap. If you find yourself writing a fourth, the through-line isn't tight enough yet — go back and find the one sentence that subsumes the rest.

**If you're working from limited context — a single screen, no info about the product, no sense of what's already shipped, open with calibration.** Something like: _"I'm working from one screen with no other context. Some of what's below will be wrong if this product does X or already does Y. Push back."_ This is calibration, not hedging. Calibration tells the reader where your confidence ends; hedging weakens claims you're confident in. Different things. Do it once, at the top, and then proceed confidently within those limits. The calibration recontextualizes every finding below as "if this isn't already done, here's where it'd land."

Then name the through-line. The thing that makes every other finding smaller if it's fixed, or worse if it's ignored. Carry the emotional context through: how this makes the user feel, what state they're coming in with, whether the interface respects that. End on a sentence that sets up the categorical sweep. "the shape is right, here's what's in the way," or "this needs a rethink, not a polish." This is where the friend-voice lives.

---

## The Lenses

These are ways of seeing, not boxes to check. Hold each lens up to the interface and notice what it reveals. Not every lens applies to every interface — use judgment.

### General

Is every element earning its place? Anything that doesn't serve the user's goal is stealing attention from what does. Look for paper cuts. The small irritations that compound: empty space while loading, inconsistent hover states, missing placeholders, spacing that shifts between screens. Then stress-test mentally: what happens with twice the content? Half the content? Longer names? The edge cases reveal whether this was designed or just arranged.

### Visual Composition

Look at the interface as a composition, not a collection of items.

**Color.** Count the distinct colors. Not "there's blue" but how many blues, how many grays, how many accents. The number tells you something. Four colors working together is intention; twelve scattered around is fragmentation. What's each color's job? Accent should mean action or emphasis. When it also means decoration, it stops meaning anything. Look for the relationships. Are colors working as a family (analogous, complementary, monochromatic) or just coexisting?

**Type.** List the sizes and weights you see. A clear scale has distinct levels and hierarchy. You can point to the headline, the body, the metadata, the labels. A muddy scale has sizes so close they compete rather than complement. Look for one hero size that establishes importance. If everything's shouting, nothing is. Type is the skeleton of hierarchy. If it's not working, nothing else will save it.

**Depth.** What's the strategy here. Borders, shadows, surface tints, or flat? The question isn't which one, it's whether there's ONE approach applied consistently. Mixed strategies (shadows here, borders there, tints elsewhere) signal "assembled from different sources." When depth is intentional, elevation communicates hierarchy: modals float above cards, cards float above the base surface. When it's not, things just... sit there.

**Weight.** The heaviest visual elements. Boldest color, largest type, strongest contrast — should match the most important content. This is where intention becomes visible. When a decorative gradient carries more visual weight than the primary action, the hierarchy is lying. Squint at the screen: does importance survive the blur?

### Interface Composition

Look at the interface as a system of attention and flow.

**Entry point.** Where does your eye land first? Where should the user focus? There should be ONE clear answer. If you're bouncing between the hero, the sidebar, the nav badges, and an inline CTA, nothing has claimed priority. The best interfaces are ruthless about this. Linear, Raycast, Notion all pick one place for your eye to land. What would they do here?

**Density.** Is the amount of information appropriate for the context? A dashboard used daily can be dense — the user builds fluency. An onboarding screen should breathe — the user is orienting. Settings visited monthly should show the common case and hide the advanced. Density isn't good or bad; it's appropriate or not. Match it to expertise level and task frequency.

**Sequence.** If this takes more than one glance, what order do elements reveal themselves? A clear visual path guides the eye: headline → supporting text → action. A muddy path leaves the user to figure out the reading order on their own. Look at how groupings work — do they guide the sequence or interrupt it? Proximity and whitespace are doing choreography whether you intended it or not.

**Dead ends.** Are there elements that don't lead anywhere? Cards with no action, sections that exist but serve no purpose, information displayed with no next step. These are visual cul-de-sacs. Good interfaces offer progressive disclosure — there's always somewhere to go next. If a user's attention lands on something, it should reward that attention.

### Interaction

Does the interface help the user do their job, or make them work around it? Does it speak their language or system language? Can they tell what's clickable? Do they know what state they're in?

**The Principles.** These are principles to hold while looking, not boxes to check. See [interaction.md](references/interaction.md) for the full framework. The short version:

- **Reversibility** — Can I undo what I just did? Confident users can recover from mistakes.
- **Forgiveness** — Does it prevent errors before they happen? A disabled button during submission, a confirmation before delete.
- **Persistence** — Does my work survive refresh, navigation, network failure, closing the tab?
- **Transparency** — Do I know what's happening? Loading states, success confirmations, error explanations. Silent interfaces feel broken.
- **Escape** — Can I get out? Close the modal, cancel the flow, go back.
- **Consistency** — Does the same action work the same way everywhere? Or do patterns shift without reason?
- **Craft** — Are these intentional choices or unexamined defaults?
- **Recognition** — Are options visible, or do I have to remember them?

Not every principle applies to every interface. A static marketing page doesn't need Persistence. A checkout flow needs all of them. Use judgment.

**Motion.** If there's animation, is it earning its place? Motion should clarify, not decorate. And users should never wait for an animation to finish before they can act.

### Craft & Technical

Technical quality that users feel even when they can't name it. Look at states, accessibility, and polish — the craft layer beneath the design.

For detailed technical checks, reference [checklists.md](references/checklists.md). The checklist covers interaction states (all five: default, hover, active, focus, disabled), data states (loading, empty, error), accessibility (keyboard navigation, focus visibility, semantics, contrast), motion constraints, and mobile considerations.

The craft lens isn't about checking boxes — it's about noticing whether the interface feels finished or feels like a prototype that shipped too early.

### Coherence

Does the screen feel like it belongs to the rest of the product, or like it wandered in from somewhere else?

**Inside your own product** — Does this match how the rest of the app already works? Buttons styled the same, modals closed the same, list items treated the same, destructive actions handled the same. When a screen drifts from its own product's patterns, users feel it before they can name it — "this feels like a different app." Monthly visitors especially.

**Against the platform** — iOS, Android, web. Each platform carries muscle memory users bring to every new app. Deviations are fine when they're earned; they're noise when they're accidental. If you're breaking a platform convention, know why.

**As one hand** — Step back and squint. Does this read as made by one person who knew what they were doing, or assembled from three different sources? Same voice, same hand, same intention — or three designers who never talked.

### Flow Coherence

_This lens applies when reviewing multiple screens or a sequence._

Flows have their own logic. Do the screens connect naturally — is the path obvious, or does the user have to figure out where they are? Does data persist across steps, or do they re-enter information? Do they know where they are in the process (step 2 of 4) and how much is left?

Look for escape routes. Can they abandon the flow at any point? Go back? What happens if something fails mid-flow — can they resume, or do they start over? What happens on refresh — does the URL deep-link to step 3, or does it dump them back at the beginning?

Good flows tell a story. There's a beginning (orientation), a middle (the work), and an end (completion, reward). Bad flows feel like a series of screens that happen to be connected.

---

## Output Format

```markdown
## Context

[1-2 sentences on what this is and who it's for]
[Name the emotional context: anxious checkout, routine dashboard, exploratory browse, etc.]

## What I'm seeing

[2-3 paragraphs, hard cap. Connective, opinionated narrative. Friend-voice, thinking out loud, a single through-line. Not a gut reaction — a take. If a fourth paragraph is forming, the through-line isn't tight enough — find the one sentence that subsumes the rest.

If working from limited context (single screen, no info about the product or what's shipped), open with calibration: "I'm working from one screen with no other context. Some of what's below will be wrong if the product does X or already does Y. Push back." This is calibration, not hedging — it tells the reader where your confidence ends. Then proceed confidently within those limits.

Name the thing that makes every other finding smaller if you fix it, or worse if you don't. Empathy and state-of-mind observations live here. End on a sentence that sets up the categorical sweep below — "the shape is right, here's what's in the way," or "this needs a rethink, not a polish."]

## Findings

Write each section as narrative prose with bolded issue names, not bulleted checklists. Lead with observation, then impact, then opportunity. Only the lenses that matter for this interface — skip what doesn't apply.

### General

[Paper cuts, scale, in-between states, intentionality. What small things are accumulating? What breaks when content gets longer? What's missing between the happy-path states? Is every element earning its place?]

### Interaction

[The Principles, organized as bolded sub-headers. Only the ones that apply. For each, lead with observation, then impact, then opportunity.]

**Reversibility** — [if applicable]
**Forgiveness** — [if applicable]
**Persistence** — [if applicable]
**Transparency** — [if applicable]
**Escape** — [if applicable]
**Recognition** — [if applicable]

### Visual Composition

[Color, type, depth, weight — analyzed as a composition, not a list of items. What's the color story? How does the type scale create hierarchy? Is there one depth strategy or several competing?]

### Interface Composition

[Entry point, density, sequence, dead ends. Where does the eye land? Is complexity revealed gradually? Are there visual cul-de-sacs?]

### Craft

[States, accessibility, polish. The technical quality that users feel even when they can't name it.]

### Coherence

[Inside your own product, against the platform, as one hand. Does this screen belong here?]

## Top Opportunities

[3-5 highest-impact changes, framed as opportunities, each in one sentence]

## High Craft

[What would exceptional look like here? Not just "good enough" — what would surprise the user with thoughtfulness? Explore 2-3 specific possibilities. This is where critique becomes generative. Always present — not optional.]

## Closing

[Two beats: the empathy return, then the pushback invitation.

**Return to the user.** One short paragraph. Name the feeling the interface creates *now*, name the feeling it would create if the top opportunities landed, and the gap between them. This is the bookend — the opening named where the user shows up; the closing names where they end up. Don't restate findings. Stay in the user's head.

**Invite pushback.** One line:

> What did I miss or get wrong?

Cite file:line for code issues when it helps the user navigate — but never paste source code blocks. The finding lives in the prose, not the snippet.]
```

---

## Finding format

Findings are paragraphs, not sentence-clusters. Each one opens with a bolded take that names the thing, then unfolds. What's there, what it's doing to the reader, what would change it. The opening should be something you'd say out loud, not a category label.

Not this: **Color** — too many uses of purple. Distracts from hierarchy. Reduce.

This: **Purple stopped meaning anything.** It's on the nav, the badges, the headline highlights, two gradients. By the time the eye reaches the CTA, purple is wallpaper. Pick the two or three places where it actually points at something and let everything else go quiet.

For interface issues, frame as missed opportunities rather than mistakes. "We're missing a chance to..." moves the reader forward. "You got this wrong" makes them defensive. Same finding, different center of gravity.

---

## Voice

Follow the voice guidelines in [SKILL.md](SKILL.md#voice).

---

## For Specs & Plans

When the input is a spec, plan, or feature description (not an artifact), shift from critique to question-surfacing.

### Intent Questions (ask first)

Before interaction questions, establish intent:

- **Who is this human?** Not "users." The actual person. Where are they when they open this? What's on their mind?
- **What must they accomplish?** Not "use the feature." The verb. What action, what outcome?
- **What should this feel like?** Say it in words that mean something. "Clean and modern" means nothing. Warm like a notebook? Cold like a terminal? Dense like a trading floor? Calm like a reading app?

If the spec doesn't answer these with specifics, ask.

### Craft Questions

These decisions shape everything downstream. Surface them early:

- **Depth strategy:** Borders-only, subtle shadows, layered shadows, or surface color shifts? Pick ONE.
- **Typography:** What typeface fits the feel? Don't default — select.
- **Color temperature:** Warm, cool, neutral? What colors exist in this product's world?
- **Information density:** Spacious or dense? What serves the user's task?

### Interaction Questions

Work through each principle. Surface what's unaddressed:

**Reversibility:** Can users recover from mistakes? Undo, trash, version history?

**Forgiveness:** What happens on double-click? Bad input? Are destructive actions distinguishable from safe ones?

**Persistence:** What survives refresh? Navigation? API failure? Is there autosave?

**Transparency:** How will they know it worked? What does loading look like? What do errors show?

**Escape:** Can they cancel at any point? Close modals? Go back in flows?

**Consistency:** Does this work like similar actions elsewhere in the app? Does it match the platform (iOS, Android, web), or earn the deviation?

**Recognition:** Are options visible or must they remember them?

### Output Format for Specs

```markdown
## [Feature Name]

### Questions

**Intent:**

- [Questions about who/what/feel if unclear]

**Craft:**

- [Decisions that need to be made early]

**Interaction:**

**Reversibility:**

- [Questions about recovery]

**Persistence:**

- [Questions about state survival]

[...etc, only principles that apply]

### Suggestions

[If you have enough context to suggest answers, offer them as defaults to accept or override]
```

---

## Severity

Order findings by impact:

1. **UX** — Information architecture, missing functionality, wrong mental model
2. **Interaction** — How interface responds, flows, communicates
3. **Visual** — Color, type, spacing, shadows

UX > Interaction > Visual.

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

---

## Influences

The interaction principles trace back to [Nielsen's 10 Usability Heuristics](https://www.nngroup.com/articles/ten-usability-heuristics/) (1994). Reversibility and Escape from "User control and freedom." Transparency from "Visibility of system status." Forgiveness from "Error prevention." Consistency from "Consistency and standards." Recognition from "Recognition rather than recall." [Laws of UX](https://lawsofux.com/) is the other one worth knowing.
