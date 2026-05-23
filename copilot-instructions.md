# GitHub Copilot — Workspace Instructions

## RevealJS Presentations

Always use the RevealJS Presenter skill (`.github/skills/revealjs-presenter/SKILL.md`) when:
- Creating a RevealJS presentation from content or outline
- Converting document content into slide format
- Building a pitch deck, technical talk, or educational presentation
- User requests "slides", "presentation", "deck", or mentions RevealJS

### Required: Read the skill before acting

Before creating or modifying any RevealJS presentation, read the full skill file:
`.github/skills/revealjs-presenter/SKILL.md`

Then read the active theme file (currently BOLD):
`.github/skills/revealjs-presenter/themes/bold.md`

### Canonical Reveal.initialize() — from SKILL.md §1.1

```javascript
Reveal.initialize({
  hash:                 true,
  center:               true,
  transition:           'fade',
  transitionSpeed:      'fast',
  backgroundTransition: 'fade',
  width:                1920,
  height:               1080,
  margin:               0.08,
  minScale:             0.2,
  maxScale:             2.0,
});
```

Never deviate from these values unless the user explicitly requests it.

### Base CSS Reset — from SKILL.md §1.3

Always apply the base CSS reset from SKILL.md §1.3 as the foundation, then layer the active theme's CSS variables and typography rules on top.

### Active Theme

**BOLD** (`themes/bold.md`) 
