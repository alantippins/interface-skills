---
name: typeset
description: "Typography critique. Works on code, screenshots, or briefs."
argument-hint: "[--plan]"
---

# Typeset

By Alan Tippins

A typography critique focused on what the user feels. Findings by job, top changes to make. Install alongside staff-designer — they share a methodology.

## How It Works

| Input          | Output                                       |
| -------------- | -------------------------------------------- |
| Code           | Findings, top 3 changes, optional code flags |
| Screenshot     | Findings, top 3 changes                      |
| Spec / Brief   | Generate a typography system (`--plan`)      |

Detect from context. If `--plan` is passed, or the input is a brief with no existing typography to review, generate a system. If the input is a screenshot, review visually. Otherwise, audit code visually first, then add code flags.

---

## Methodology

The four-job framework (Hierarchy, Rhythm, Measure, Signal) lives in staff-designer. Load it before proceeding:

→ Read `~/.claude/skills/staff-designer/references/typography.md`

Apply the Orient → Count → Audit sequence from that file.

For code input, also reference [references/checks.md](references/checks.md) for implementation-level flags.

---

## Audit Output

```
## Findings

Hierarchy — [prose, specific and quantitative. Skip if the job is clean.]
Rhythm — [prose. Skip if clean.]
Measure — [prose. Skip if clean.]
Signal — [prose. Skip if clean.]

## Top 3
1. [specific change, one sentence]
2. [specific change, one sentence]
3. [specific change, one sentence]

## Code Flags
- [one-liners, code input only, skip section if nothing to flag]
```

**Findings.** Write what the user feels. Raw `<span>` that renders correctly is not a finding. Skip any job that's clean — a short honest audit beats four-section theater. Name what's working in one sentence; spend the words on the real issues. After naming a problem, show what great looks like specifically.

Hypothetical failures ("would break in monochrome," "would collapse under long copy") belong in Top 3 as a real change, not in findings. Audit the current experience, not imagined ones.

**Font direction.** Assume the typeface was chosen. Don't comment on an established design-system font as a stylistic preference. Font commentary belongs in `--plan` mode, or as a finding when the Orient step's Font Fit check surfaces a real mismatch — no custom font loaded, expressive product running on a utility sans, marketing hero using the body UI font. Default is silence.

**Code Flags.** Token inconsistencies, off-system classes, raw HTML. One line each. Advisory. Skip the section if there's nothing to flag.

**Top 3.** The three highest-impact changes. Visual first, code second. One sentence each, specific: "Swap `leading-5` to `leading-normal` on OnboardingValueCard description" beats "fix line-height."

---

## Plan Methodology

When `--plan` is passed or the input is a brief:

1. **Identify the reading context** — Use the context table from the typography methodology to set defaults.
2. **Choose base size** — 13–14px for data tools. 15–16px for apps. 16–18px for reading-heavy products. 18–22px for display-first marketing.
3. **Set the scale** — Choose a ratio:
   - Dense tools: custom increments (12/14/16/20/24)
   - Apps and task flows: 1.25 (Minor Third)
   - Reading products: 1.333 (Perfect Fourth)
   - Expressive / marketing: 1.5 (Perfect Fifth) or higher
4. **Map hierarchy** — Assign scale steps to the four levels. Name them semantically.
5. **Set rhythm** — Line-height per context. Spacing relationships.
6. **Define measure** — Max-width for body. Constraints for narrow columns.
7. **Write signal rules** — How weight, size, and color map to importance for this system.

Make decisions. State the ratio, state the base, state why it fits the context.

---

## Plan Output

```
## Font
[Typeface recommendation with reasoning. Specific: "Inter for UI, DM Serif Display at heading for warmth."]

## Scale
Base: [size]px · Ratio: [ratio or named increment]

| Step | Size  | Semantic Name | Use               |
| ---- | ----- | ------------- | ----------------- |
| xs   | [px]  | muted         | captions, labels  |
| sm   | [px]  | secondary     | supporting text   |
| base | [px]  | primary       | body copy         |
| lg   | [px]  | subheading    | section headers   |
| xl   | [px]  | heading       | page headings     |
| 2xl  | [px]  | display       | hero, emphasis    |

## Hierarchy Map
Primary: [step] · [weight] · [color token]
Secondary: [step] · [weight] · [color token]
Tertiary: [step] · [weight] · [color token]
Muted: [step] · [weight] · [color token]

## Rhythm
Body line-height: [value]
Heading line-height: [value]
Label line-height: [value]
Section spacing: [value]

## Measure
Body max-width: [ch or rem]
Narrow column: [value]
Use text-balance on headings. Use text-pretty on body.
Use tabular-nums on numeric data.

## Signal Rules
[How weight, size, and color reinforce semantic importance for this system]

## Tailwind / CSS
[Concrete implementation — classes or custom properties, ready to copy]
```

---

## Voice

Same posture as staff-designer — direct, specific, quantitative, oriented toward the upside. Typeset is the typography depth layer: it goes where staff-designer's Craft principle points but doesn't follow.

Name what's actually there before naming what's wrong. Frame findings as what the typography could be doing. "The description sits at the same weight and line-height as the label above it — one level doing two jobs, and the user has to work harder to parse the card" is a finding. "The hierarchy is unclear" is not.

After naming a problem, describe the better version specifically. "Giving descriptions a looser line-height would let them breathe as supporting copy instead of competing with the label for attention" beats "increase line-height on descriptions."

Skip jobs that are clean. Saying nothing about Measure when measure is fine is correct. Filling four sections because there are four sections is how drift starts.

For plan mode: make decisions. "Use a 1.333 ratio — Perfect Fourth — because this is a reading-heavy product and the intervals give headings enough presence without needing large sizes" is useful. A table of options asking the user to choose is not.

---

## Foundation

- [references/checks.md](references/checks.md) — Implementation-level patterns to flag when reviewing code
