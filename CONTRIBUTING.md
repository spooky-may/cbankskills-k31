# Contributing to CN Finance

Thank you for your interest in contributing. This document covers how to add new skills, improve existing ones, and contribute to the showcase site.

---

## Ways to contribute

- **New skill** — add a `SKILL.md` to an existing vertical
- **New vertical** — add a new folder under `skills/plugins/vertical-plugins/`
- **Bug fix** — fix incorrect instructions in an existing `SKILL.md`
- **Web improvements** — improve the showcase site in `web/`
- **Documentation** — improve guides in `docs/`

---

## Skill authoring

### Structure

Each skill lives in its own folder with exactly one `SKILL.md`:

```
skills/plugins/vertical-plugins/[vertical]/skills/[skill-name]/
└── SKILL.md
```

### SKILL.md format

```markdown
---
name: your-skill-name
description: One paragraph describing what the skill does, when to use it,
  what inputs it expects, and what output it produces. Be specific.
---

## Overview
...

## Instructions
...

## Output format
...
```

**Rules for skill authors:**

1. `name` must be kebab-case and match the folder name
2. `description` must be a single paragraph — this appears in the Claude UI
3. All instructions must be unambiguous — assume Claude has no prior context
4. Specify output format explicitly (page count, word count, sections)
5. Include at least one worked example in the skill body
6. Do not reference proprietary data sources unless the vertical already ships an MCP connector for it

### Testing a skill before submitting

```bash
# Install the skill locally via Claude Code CLI
claude plugin install ./skills/plugins/vertical-plugins/[vertical]

# Test the slash command
/your-skill-name [test input]
```

---

## Adding a new vertical

1. Create the folder structure:

```bash
mkdir -p skills/plugins/vertical-plugins/[vertical]/skills
mkdir -p skills/plugins/vertical-plugins/[vertical]/commands
```

2. Add a `.claude-plugin/plugin.json`:

```json
{
  "name": "vertical-name",
  "version": "1.0.0",
  "description": "One-line description",
  "author": "your-name"
}
```

3. Add the vertical to `web/content/verticals.ts` with all required fields.

4. Create a placeholder in `web/public/demos/[vertical]/` for demo assets.

---

## Web app contributions

The showcase site is a standard Next.js 14 App Router project.

```bash
cd web
npm install
npm run dev
```

- Components go in `components/` — follow PascalCase naming
- Use Tailwind color tokens from `tailwind.config.ts`, never raw hex values
- Prefer Server Components unless the component genuinely needs browser state
- Run `npm run typecheck` and `npm run lint` before opening a PR

---

## Pull request checklist

- [ ] Skill `name` in frontmatter matches folder name
- [ ] `description` is a single paragraph
- [ ] Typecheck passes (`npm run typecheck` from `web/`)
- [ ] No raw hex colors in components
- [ ] No new external UI libraries added without prior discussion
- [ ] `CHANGELOG.md` updated if the change is user-facing

---

## Code of conduct

Be professional. Finance is a high-stakes domain — accuracy matters. If you're unsure whether a skill's output is correct for a given workflow, flag it rather than ship it.
