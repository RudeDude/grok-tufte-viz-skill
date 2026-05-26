---
name: tufte-viz
description: |
  Ideate and critique data visualizations using Edward Tufte's principles from "The Visual Display of Quantitative Information" and later works. Use this skill when:
  (1) Designing new data visualizations or charts
  (2) Critiquing or improving existing visualizations, dashboards, or figures
  (3) Reviewing reports, papers, or slides for graphical integrity and clarity
  (4) Deciding between visualization approaches (small multiples vs. overlaid lines, etc.)
  (5) Reducing chartjunk, increasing data-ink ratio, or applying the eraser/collision tests
  (6) Planning high-density displays, sparklines, or explanatory graphics
  Applies principles: data-ink ratio, chartjunk elimination, graphical integrity, lie factor, small multiples, layering & separation, micro/macro, range-frames, and analytical design.
when-to-use: Use when the user asks to design, improve, critique, or review any chart, dashboard, figure, data visualization, or asks for "Tufte style", "small multiples", "less chartjunk", "higher data-ink", or similar. Also useful proactively on any pasted chart image or data-heavy slide.
metadata:
  short-description: "Tufte data visualization principles — critique, design, small multiples, data-ink, integrity"
---

# Tufte Visualization Skill

Apply Edward Tufte's principles to design clear, honest, high-density data visualizations and to critique existing ones.

## Grok-Specific Guidance

When working in Grok:

- **Generating output**: Prefer clean, minimal SVG (or high-quality PNG via the `image_gen` tool) that follows the principles below. When the user wants an actual image, craft an extremely precise prompt for `image_gen` that encodes the Tufte treatment (no heavy grids, direct labels, range ticks, shared scales, grayscale with purposeful color, etc.).
- **Critiquing user images**: If the user pastes or uploads a screenshot/PDF/image of a chart, first describe what you see, then run it through the full critique workflow (graphical integrity, data-ink, chartjunk, eraser test, collision test, Tufte test).
- **Integration with other skills**: This skill pairs extremely well with:
  - `pptx`, `docx`, `xlsx` — when the goal is a report or presentation containing figures.
  - `review` / `design` — when evaluating or creating design docs that contain visualizations.
  - `image_gen` — for producing the final clean artifact.
- Always offer both **critique** and **concrete improved version** (code or generated image) unless the user only asked for one.

## Workflow

### For new visualizations:

1. **Clarify the data story**
   - What comparisons matter?
   - What's the key insight to communicate?
   - Who's the audience?

2. **Select approach** using Tufte principles:
   - High comparison need → Small multiples
   - Dense data → Consider data tables, sparklines
   - Time-series → Line charts with minimal grid
   - Part-to-whole → Avoid pie charts; prefer bar/table or stacked small multiples

3. **Design with data-ink in mind**
   - Start minimal, add only what's necessary
   - Every element must earn its ink
   - Default to grayscale; use color purposefully (never rainbow for sequential data)

4. **Apply the eraser test before shipping**
   - For every element (label, tick, gridline, border, annotation): can it be erased without losing information that's not already conveyed elsewhere?
   - Watch for duplicate encodings: numeric labels next to a value already marked by a tick; legends duplicating direct labels; per-panel scale annotations duplicating a shared-scale caption.
   - If two elements compete for the same job, keep the visual one and drop the textual one (or vice versa) — not both.

5. **Apply the collision test before shipping**
   - For every text element in the plot (axis labels, point annotations, epoch labels, baseline labels, explanatory notes): mentally draw its bounding box. Does anything else — another text element, a data line, dense markers — live in or cross that box?
   - The eraser test catches *redundant* elements; the collision test catches *crowded* ones. Both must pass.
   - Standard fixes: move explanatory prose out of the plot into the figcaption; relocate band/epoch labels to a dedicated strip above the plot; push baseline/reference labels to the outside margin; give each in-plot annotation a leader line so the marker and the text occupy clearly separated space.
   - Watch especially: inverted axes (top of plot is now where extreme values cluster, where annotations also want to go); shared-scale small multiples (labels stacked near zero in every panel); dense scatter (text vanishes into the dot cloud unless explicitly cleared).

6. **Apply the Tufte test** (see references/tufte-principles.md and references/analytical-design.md)

### For critiquing visualizations:

1. **Check graphical integrity**
   - Calculate lie factor if proportions seem off
   - Verify baselines and scales
   - Look for 3D distortion or truncated axes

2. **Identify chartjunk**
   - Decorative elements
   - Heavy grids
   - Unnecessary 3D effects
   - Moiré patterns / busy fills

3. **Evaluate data-ink ratio**
   - What can be erased?
   - What's redundant?

4. **Run the full checklist** (eraser + collision + Tufte tests)

5. **Suggest improvements** with specific before/after recommendations (text description +, when possible, a minimal improved SVG or a precise `image_gen` prompt).

## Key Principles Reference

Load these files for the full detailed principles and checklists:

- `references/tufte-principles.md` — core principles from *The Visual Display of Quantitative Information*: lie factor, data-ink, chartjunk, small multiples, graphical integrity, data density.
- `references/analytical-design.md` — extensions from *Envisioning Information*, *Visual Explanations*, and *Beautiful Evidence*: the six principles of analytical design, sparklines, layering & separation, micro/macro, range-frames, causality, confections, escaping flatland.

**Quick Tufte Checklist (use on every critique or design):**
- [ ] Lie Factor ≈ 1.0 (no visual distortion)
- [ ] Maximum data-ink ratio (erase everything that fails the eraser test)
- [ ] Zero chartjunk
- [ ] Clear, direct labeling (no legends when you can label the data itself)
- [ ] Answers "compared to what?"
- [ ] Shows causality or mechanism where relevant
- [ ] Multivariate (not over-reduced to 1–2 variables)
- [ ] Words, numbers, images integrated — not segregated
- [ ] Reveals multiple levels of detail (micro + macro)
- [ ] Layering: primary data dominates, secondary recedes (light grids, gray underlays)
- [ ] Appropriate data density
- [ ] Range-frames or data-carrying axes used where helpful

## Producing a Tufte-Style Visualization (Grok Workflow)

When the user wants you to *make* the improved version:

1. Summarize the data story and chosen treatment in 1–2 sentences.
2. Decide the exact form (small multiples, sparkline table, range-frame line chart, etc.).
3. Output either:
   - A minimal, clean SVG (preferred for precision), or
   - A highly detailed prompt for the `image_gen` tool that explicitly encodes every Tufte decision (no heavy borders, direct labels at ends of lines, shared y-scale stated in caption, single light zero line, range ticks only, etc.).
4. If the user will embed this in slides or docs, also provide the plain-language caption that belongs underneath the figure.

## Sources & Credits

This skill was adapted from the outstanding gist by aparente:

https://gist.github.com/aparente/e48c353755958621b3c0004593105a90

Original files included:
- SKILL.md
- references__tufte-principles.md
- references__analytical-design.md
- Four large demonstration HTML files (giss-temperature, kyoto-sakura, sunspot-butterfly, sunspot-pretty) showing dramatic before/after treatments.

The giant demo HTML files were intentionally omitted from this distribution due to size (they contain full inline SVG path data). View the original gist for the beautiful interactive before/after examples.

All core principles and the excellent "eraser test" / "collision test" language are preserved and lightly extended for Grok usage.
