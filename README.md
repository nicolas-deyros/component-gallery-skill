# component-gallery-skill

A skill for [Claude Code](https://claude.ai/code) that generates high-quality UI components using best practices from [component.gallery](https://component.gallery), with cross-references to **Material Design**, **Atlassian DS**, and **Carbon (IBM)**.

## What it does

- Generates UI components in **Tailwind CSS or native CSS** based on context
- Decides automatically which approach to use (rules included)
- Fixes common AI spacing mistakes: box model, margin collapse, Flexbox errors
- References how **Material, Atlassian and Carbon** solve each component
- Fetches live data from component.gallery via `web_search` fallback
- Framework-agnostic: React, HTML, Vue — works with any stack

## Install

```bash
npx skills add nicolas-deyros/component-gallery-skill
```

Or globally (available in all your projects):

```bash
npx skills add nicolas-deyros/component-gallery-skill -g
```

## Usage

Just ask Claude to create a component:

```
Create a button component with primary, secondary and danger variants
Build an accordion for a FAQ section
Make a modal dialog with a form inside
Create a data table with sortable columns
```

The skill automatically:
1. Looks up the canonical name and alternatives from component.gallery
2. Decides Tailwind vs CSS native based on your project context
3. Applies visual rules (spacing, box model, Flexbox, z-index scale)
4. Delivers the component with variants, states, and accessibility notes
5. Shows how Material, Atlassian and Carbon solve the same component

## Components covered

### Actions
Button · Icon Button · Button Group · Toggle Button · Split Button · FAB

### Forms
Input / Text Field · Textarea · Select · Combobox · Checkbox · Radio · Switch · Slider · Date Picker · File Upload · Search

### Navigation
Navbar · Sidebar · Tabs · Breadcrumb · Pagination · Stepper · Link · Menu

### Overlays & Feedback
Modal · Tooltip · Popover · Toast · Alert · Spinner · Skeleton · Progress Bar

### Content
Card · Accordion · Table · List · Avatar · Badge / Tag / Chip · Empty State · Carousel · Tree View · Rating · File Attachment

### Layout
Header · Footer · Segmented Control · Rich Text Editor

## Design systems referenced

| Design System | Source |
|---|---|
| Material Design 3 | [m3.material.io](https://m3.material.io/components) |
| Atlassian Design System | [atlassian.design](https://atlassian.design/components) |
| Carbon (IBM) | [carbondesignsystem.com](https://carbondesignsystem.com/components/overview) |

## Skill structure

```
component-gallery-skill/
├── SKILL.md                  ← Orchestrator + CSS/Tailwind rules (always in context)
└── references/
    ├── components.md         ← ~40 components with variants, states, accessibility
    ├── material.md           ← Material Design 3 reference
    ├── atlassian.md          ← Atlassian DS reference
    └── carbon.md             ← Carbon IBM reference
```

Reference files are loaded on demand — only what's needed for each request, keeping context lean.

## Visual rules enforced

The skill explicitly corrects the most common AI spacing mistakes:

- **Semantic spacing** — padding belongs to the component, margin to the layout
- **No margin collapse** — `gap` over `margin` for sibling elements
- **Explicit box model** — `box-sizing: border-box` always declared in native CSS
- **Correct Flexbox** — `shrink-0` only on icons/avatars, `gap` not `margin` for alignment
- **Fixed heights** — buttons use `height` not `min-height + padding-y`
- **z-index scale** — dropdown 100 · sticky 200 · overlay 300 · modal 400 · toast 500 · tooltip 600

## Compatibility

Works with Claude Code and any agent supported by [skills.sh](https://skills.sh).

## License

MIT
