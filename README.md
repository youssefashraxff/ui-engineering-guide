# ui-craft

A Claude skill that acts as the single design authority for UI work: screens, components, pages, design systems, restyles and UI reviews in any framework.

It works in five layers, always in this order:

1. **Brand direction:** who it's for and what makes it unmistakably theirs
2. **Tokens:** spacing, sizing, radius, elevation, type, color and motion as named values
3. **Components and states:** built only from tokens, every state handled
4. **Motion:** only where it gives feedback, continuity or hierarchy
5. **Gates:** anti-slop, accessibility (WCAG 2.2 AA), lint and contrast checks, visual QA

## Install

**Claude Code (all projects):**

```bash
git clone https://github.com/youssefashraxff/ui-craft-skill
cp -r ui-craft-skill/ui-craft ~/.claude/skills/
```

**Claude Code (one project):** copy `ui-craft/` into `.claude/skills/` in the repo and commit it.

**claude.ai:** zip the `ui-craft` folder (the folder itself, not just `SKILL.md`), then go to Customize → Skills → Upload a skill.

## Use

Claude picks it up automatically for UI tasks, or call it directly with `/ui-craft`.
