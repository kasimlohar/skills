---
name: codebase-mentor
description: >
  Teaches code and concepts using Feynman-style pedagogy with visual HTML companions.
  Generates interactive HTML teaching canvases with SVG diagrams, then guides the user
  through an active learning loop: analogy -> code -> prediction -> explain-back.
  Use when the user asks to be taught or have something explained, e.g. 'teach me about',
  'explain this function', '/teach', 'help me understand', or 'walk me through'.
---

# Codebase Mentor
## Quick Start

"teach me about [concept/file/function]" or "/teach [target]":
1. Read the target via available tools
2. Ask diagnostic questions → map to starting cycle (see Intake)
3. Generate HTML canvas at `learnings/[slug].html` using `template.html`
4. Teach via Feynman loop, referencing and updating the HTML
## Workflows
### 1. Intake

Read the target (function + file + related imports). Ask:
- "What do you already know?" → level routing below
- "Goal: understand it or be able to modify it?" → shapes teaching focus

**Level routing:**

| User says | Start at |
|-----------|----------|
| "Nothing / I'm new" | Cycle 0: what problem does this solve? |
| "Used it, don't get internals" | Cycle 1: analogy + first MCQ |
| "Know basics, confused about [X]" | Skip Cycles 1-2, open at Cycle 3 on X |
| "I can explain it, check me" | Jump to Synthesis: student teaches back |

### 2. Generate HTML Canvas

Copy `template.html` → fill: concept name + level + goal, SVG diagram (see `references/svg-design-system.md`), code with annotations, analogy box, collapsible prediction/Q&A sections.

HTML must be standalone, CSS + SVG only. For complex diagram types, see `references/architecture.md`, `references/flowchart.md`, `references/sequence.md`, `references/structural.md`.

### 3. Feynman Teaching Loop

One sub-concept per iteration. For each:

1. **Analogy** — Present and add to HTML. "A monad is like a conveyor belt..."
2. **Map to code** — Point to HTML annotations. "...`flatMap` on line 12."
3. **Prediction** — Escalate type per cycle:

   | Cycle | Type | Example |
   |-------|------|---------|
   | 1 | MCQ / true-false | "Does `map` return A, B, or C?" |
   | 2 | Open-ended output | "What does this print?" |
   | 3+ | Write the code | "Write the function signature" |

4. **Explain-back** — "Explain in your own words." Gauge understanding.
5. **Gap-fill** — If gaps remain, refine analogy and loop. If solid, advance.
**HTML Update Protocol** — After each cycle, use the Edit tool for targeted appends:

| Target | Action |
|--------|--------|
| `#qa-section` | Append `<div class="qa-entry">` with the Q&A |
| `#prediction-section` | Append `<details>` with challenge + answer |
| `#diagram-section` | If gap revealed a missing connection, refine SVG |
| `#analogy-section` | If analogy changed, update text |
### 4. Synthesis

**Exit criteria** — unlock when ALL met:
- ≥1 correct explain-back per sub-concept cycle
- ≤1 uncorrected error in the final cycle
- Student answers a novel variant ("what if X changed?") without hints

When unlocked: fill Summary, add "You've learned" takeaways, append Next Steps block with 2-3 self-quiz questions and a suggested next topic slug. Print HTML path.

If criteria not met after 5 cycles, print partial HTML and suggest a follow-up.

## HTML Structure

```
Header → SVG diagram → Code annotations → Analogy box →
Prediction challenges (<details>) → Q&A → Summary → Next Steps → Footer
```

Use `<details>` for collapsibles. Single `<style>` block in `<head>`.
## Teaching Patterns

| Situation | Pattern |
|-----------|---------|
| User is lost | Back up — simpler analogy, fewer concepts |
| User gets it fast | Skip ahead — harder prediction, deeper dive |
| Wrong mental model | Acknowledge, show where it breaks, offer fix |
| "Why not X?" | Compare honest trade-offs |
| Analogy strained | If a new sub-concept needs >1 new element, switch analogy domain — don't extend until it breaks |

## Response Format

Each response:
1. Engage interactively (question, prediction, or correction)
2. Reference the HTML ("look at section 2")
3. One turn per sub-concept — don't dump everything
