---
name: outerweb-guideline-curator
description: Use ONLY when the user wants to update Outerweb OpenCode agents, skills, rules, preferences, anti-patterns, or golden examples. Triggers: remember this, update our rules, make the AI stop doing this, save this as a golden example, we like this style.
license: MIT
metadata:
  owner: Outerweb
---

# Outerweb Guideline Curator

Use this skill only for maintaining the Outerweb OpenCode setup itself.

## Purpose

This skill turns real project feedback into better agents, skills, and golden examples without bloating always-on prompts.

Use it when the user says things like:

- "Remember this preference."
- "Update our rules."
- "The AI keeps doing this, make it stop."
- "We like this implementation style."
- "Save this as a golden example."
- "Outerweb always does it this way."

## First classify the feedback

Classify every requested guideline update into one of these buckets:

- Always-on agent rule: short, universal behavior that must apply in nearly every Outerweb session.
- Domain skill rule: specific behavior for Laravel architecture, model lifecycle, Filament, quality tooling, Pest, packages, or analysis.
- Golden example: useful structure or style that is too verbose for the main prompt.
- Project-local rule: only true for one repository; belongs in that project's `AGENTS.md`, `.ai/guidelines`, or project skill.
- Inbox item: useful observation, but not clear enough to encode yet.

## Token discipline

- Do not copy long examples into `build.md` or `plan.md`.
- Keep always-on agent rules short and high leverage.
- Put detailed, domain-specific behavior in focused skills.
- Put larger examples in `outerweb-golden-examples/reference/*.md`.
- Prefer editing an existing skill over creating a new one unless the trigger domain is clearly distinct.

## Update process

1. Restate the user's requested preference in concrete terms.
2. Decide the correct destination.
3. If the preference conflicts with an existing rule, point out the conflict and ask before changing it.
4. Edit the smallest number of files needed.
5. If adding a golden example, sanitize business-specific details while preserving structure.
6. Validate skill names, frontmatter, and OpenCode config parsing.
7. Remind the user to restart OpenCode.

## Golden example rules

Golden examples should capture structure, not proprietary business logic.

Each golden example should include:

- When to use it.
- What pattern to copy.
- What not to copy.
- A sanitized code skeleton.
- Notes explaining why Outerweb likes the structure.

Avoid:

- Client-specific names, secrets, or business flows.
- Large copy-pasted production files.
- Examples that contradict current skills or agent prompts.

## File destinations

Use these global files unless the user asks for project-local behavior:

- `~/.config/opencode/agents/build.md`
- `~/.config/opencode/agents/plan.md`
- `~/.config/opencode/skills/outerweb-quality-tooling/SKILL.md`
- `~/.config/opencode/skills/outerweb-laravel-architecture/SKILL.md`
- `~/.config/opencode/skills/outerweb-model-lifecycle/SKILL.md`
- `~/.config/opencode/skills/outerweb-filament-admin/SKILL.md`
- `~/.config/opencode/skills/outerweb-pest-workflow/SKILL.md`
- `~/.config/opencode/skills/outerweb-package-selection/SKILL.md`
- `~/.config/opencode/skills/outerweb-analysis-review/SKILL.md`
- `~/.config/opencode/skills/outerweb-golden-examples/reference/*.md`

## Manual update phrases

When the user gives feedback, prefer these interpretations:

- "Always do X" means candidate always-on rule, unless it is domain-specific.
- "When writing models, do X" means `outerweb-model-lifecycle`.
- "When writing Filament, do X" means `outerweb-filament-admin`.
- "When testing, do X" means `outerweb-pest-workflow`.
- "Use this code as an example" means `outerweb-golden-examples`.
- "This is project-specific" means project-local guideline, not global config.

## Validation checklist

- Skill folder name matches `name:` frontmatter.
- Skill description clearly says when to use it.
- No invalid OpenCode config fields were added.
- No generated IDE helper or project source files were edited accidentally.
- The update is concise enough to improve behavior without increasing token usage unnecessarily.
