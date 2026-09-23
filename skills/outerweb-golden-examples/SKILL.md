---
name: outerweb-golden-examples
description: Use when the user asks for Outerweb golden examples, structural examples, preferred code shape, or when implementing Actions, models, policies, factories, seeders, Filament artifacts, or Livewire forms and examples would improve consistency.
license: MIT
metadata:
  owner: Outerweb
---

# Outerweb Golden Examples

Use this skill to load concise structural examples of code Outerweb likes.

These are structural references, not project requirements or ready-to-copy implementations.

## Available references

- `reference/action.md`: Structural Action walkthrough covering typed `execute()` boundaries and conditional transactions; no copy-ready class.
- `reference/livewire-form.md`: Non-Filament Livewire form with FormRequest validation metadata; use only with compatible installed versions and project conventions.
- `reference/filament-resource.md`: Version-sensitive split resource delegating to form and table classes; add an infolist only when the feature and installed API warrant it.
- `reference/filament-table.md`: Version-sensitive split-table sketch with columns and a filter, plus guidance on optional actions, query modification, and sorting.
- `reference/filament-form.md`: Version-sensitive Filament form schema with labels and chained modifiers.
- `reference/filament-infolist.md`: Version-sensitive Filament infolist with callout, section, and entries.
- `reference/policy.md`: Illustrative single-auth policy; choose principal typing and guest access from the project's actual auth topology and authorization entry points.
- `reference/model.md`: Eloquent model with conditional attribute metadata, relations, scopes, and casts PHPDoc.
- `reference/factory.md`: Factory with `fake()`, relationships, and defaults; enum helpers only when available.
- `reference/seeder.md`: Seeder with factories and linked data; cursor iteration only when appropriate.

## How to use examples

- Load only the reference matching the artifact being changed.
- Treat code, domain, paths, auth topology, locale helpers, and package APIs as illustrative, not defaults.
- Copy structure only where the approved feature, maintained project guidance and conventions, installed versions, and version-matched documentation permit. Project evidence takes precedence over examples.
- Examples do not authorize extra scope, dependencies, tooling, or tests.
- For detailed decisions, use `outerweb-laravel-architecture`, `outerweb-model-lifecycle`, or `outerweb-filament-admin` as applicable.

## Maintenance

Use `outerweb-guideline-curator` when the user wants to add, update, or remove golden examples.
