---
name: outerweb-golden-examples
description: Use when the user asks for Outerweb golden examples, structural examples, preferred code shape, or when implementing Actions, models, policies, factories, seeders, or Filament resources and examples would improve consistency.
license: MIT
metadata:
  owner: Outerweb
---

# Outerweb Golden Examples

Use this skill to load concise structural examples of code Outerweb likes.

These examples are sanitized from real project style. They preserve shape, formatting, and conventions, not business logic.

## Available references

- `reference/action.md`: Action class with `execute()` and transaction boundary.
- `reference/filament-resource.md`: Thin Filament resource delegating to form, infolist, and table classes.
- `reference/filament-table.md`: Filament table with columns, filters, actions, query modification, and sorting.
- `reference/filament-form.md`: Filament form schema with translated labels and chained modifiers.
- `reference/filament-infolist.md`: Filament infolist with callout, section, and entries.
- `reference/policy.md`: Policy using `?Authenticatable $authenticatable` and tenant-style access checks.
- `reference/model.md`: Eloquent model with attributes, relations, scopes, and casts PHPDoc.
- `reference/factory.md`: Factory using `fake()`, relationships, and explicit defaults.
- `reference/seeder.md`: Seeder using factories, cursors, and realistic linked data.

## How to use examples

- Copy structure, not names or domain logic.
- Match the target project's existing namespace and conventions.
- Keep chained modifiers on new lines.
- Keep full words in variables and method names.
- Preserve PHPStan-friendly PHPDoc where shown.
- When examples conflict with a project-local pattern, follow the project-local pattern.

## Maintenance

Use `outerweb-guideline-curator` when the user wants to add, update, or remove golden examples.
