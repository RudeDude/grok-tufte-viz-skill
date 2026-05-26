# grok-tufte-viz-skill — Staging Area

This directory contains an adapted version of the excellent **tufte-viz** skill originally published as a Claude Code skill in this gist:

**Source:** https://gist.github.com/aparente/e48c353755958621b3c0004593105a90

The goal of this staging folder (inside the self-bio repo) is to prepare a clean, Grok-CLI-native version of the skill before importing it into the user's personal `~/.grok/skills/` collection (or a project-local `.grok/skills/`).

## Final Skill Name (after import)

`tufte-viz`

## Contents (Current)

```
grok-tufte-viz-skill/
├── README.md                 # This file
├── SKILL.md                  # Adapted main skill file (frontmatter + workflow + Grok guidance)
└── references/
    ├── tufte-principles.md   # Core Tufte principles (from Visual Display of Quantitative Information)
    └── analytical-design.md  # Later work (Envisioning Information, Visual Explanations, Beautiful Evidence)
```

## What Was Changed / Adapted

1. **File layout** — References moved into a proper `references/` subdirectory (original gist used flat `references__*.md` names because of gist limitations). All internal links updated.

2. **Frontmatter enriched** — Added `when-to-use`, `metadata.short-description`, and a more precise multi-line `description` to match the style and auto-invocation quality of other high-quality Grok skills (`help`, `create-skill`, bundled `design`/`review`, etc.).

3. **Grok-specific guidance added** (new section near the top):
   - How to use `image_gen` to actually *produce* Tufte-style visualizations (not just critique).
   - How to critique user-pasted chart images/screenshots.
   - Explicit integration notes with `pptx`, `docx`, `xlsx`, `review`, and `design` skills.
   - Concrete workflow for "generate the improved version."

4. **Claude references neutralized** — Minor title/description language cleaned; the skill is now presented as a general Grok skill.

5. **Demo HTML files omitted** — The original gist contains four very large demonstration HTML files (full inline SVG path data for real datasets). These were intentionally left out:
   - They are huge and would bloat any skill distribution.
   - They are excellent for *illustration* but not required at runtime.
   - Users are directed back to the original gist for the beautiful before/after examples.

6. **Sources & Credits section** added at the bottom of SKILL.md.

7. **Minor polish** — Improved checklists, clearer Grok workflow steps, consistent formatting.

## Installation / Import (Once Ready)

The intended final location is:

```bash
~/.grok/skills/tufte-viz/
```

### Simple manual import (recommended while experimenting)

```bash
# From inside this directory
mkdir -p ~/.grok/skills/tufte-viz/references

cp SKILL.md ~/.grok/skills/tufte-viz/
cp references/*.md ~/.grok/skills/tufte-viz/references/

# Verify
grok inspect --json | jq '.skills[] | select(.name == "tufte-viz")'
```

### Or as a project-local skill (if you want it version-controlled with this repo)

```bash
mkdir -p .grok/skills/tufte-viz/references
cp SKILL.md .grok/skills/tufte-viz/
cp references/*.md .grok/skills/tufte-viz/references/
```

Grok will discover it with highest priority (local > repo > user).

## Testing the Skill

After import:

```bash
/skills tufte-viz
# or simply
/tufte-viz
```

Then try prompts like:
- "Critique this chart: [paste image or describe it]"
- "Redesign this temperature anomaly plot using Tufte principles"
- "I need a small-multiples view of the last 8 quarters of revenue by region"
- "Apply the eraser test to the dashboard I just described"

## Future Enhancements (Possible)

- Tiny curated SVG examples (instead of linking to the big demos)
- A helper script that can generate a Tufte-styled matplotlib/seaborn style or a clean SVG template
- Deeper `image_gen` prompt templates for common chart types
- Optional integration with code execution for data transformation before viz

## License / Attribution

The original content and structure come from the gist by aparente (https://gist.github.com/aparente/e48c353755958621b3c0004593105a90). This adaptation preserves the core intellectual contribution while making it a first-class citizen in the Grok CLI skills ecosystem.

## Next Steps (for the user)

1. Review the files in this directory (especially the adapted SKILL.md).
2. Decide on scope (user `~/.grok/skills/` vs. project-local).
3. Run the import commands above.
4. Test with real visualization tasks.
5. Iterate (this staging folder makes future tweaks easy before re-importing).

---

*Staging folder created in the self-bio workspace for controlled adaptation.*
