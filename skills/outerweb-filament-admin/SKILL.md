---
name: outerweb-filament-admin
description: Use for Filament admin panels, resources, pages, forms, tables, actions, relation managers, auth pages, tenants, panels, notifications, and Filament tests in Outerweb Laravel projects.
license: MIT
metadata:
  owner: Outerweb
---

# Outerweb Filament Admin

Use this skill for Filament work, especially Filament v5 projects.

## Structure

- Follow the existing panel namespace, such as `app/Filament/Salon`.
- Use generated-style split resources:
  - `Resources/{Plural}/{Resource}.php`
  - `Resources/{Plural}/Pages/*`
  - `Resources/{Plural}/Schemas/*Form.php`
  - `Resources/{Plural}/Schemas/*Infolist.php`
  - `Resources/{Plural}/Tables/*Table.php`
- Keep Resource classes thin and delegate to schema/table classes.
- Put custom Filament actions in panel-specific `Actions` folders when the project does so.
- Use `static make()` wrapper classes for reusable Filament actions.

## Panels

- Inspect the panel provider before adding resources or auth behavior.
- Respect configured guards, password brokers, tenants, colors, domains, paths, middleware, and Vite themes.
- For tenant-aware panels, use `Filament::getTenant()` and existing tenant relationships.
- Do not assume the default `User` model or `web` guard.

## Forms and schemas

- Use `Filament\Schemas\Schema` and `Section` when the project uses Filament v5 schemas.
- Labels should usually use translations, not hardcoded UI copy.
- Put modifiers on new lines: `->nullable()`, `->required()`, `->unique()`, `->maxLength()`, etc.
- Use enum option maps from enum methods like `supportedCases()` and `getLabel()`.
- Put validation mutations close to the field when they are field-specific.

## Tables

- Make important columns searchable and sortable when useful.
- Use `toggleable(isToggledHiddenByDefault: true)` for secondary columns.
- Use `TextColumn::make(...)->isoDateTime()` for timestamps when matching project convention.
- Use `ActionGroup` for secondary row actions and `BulkActionGroup` for bulk actions.
- Use `modifyQueryUsing()` for eager loading and query constraints.
- Default sorting should match the user workflow, not arbitrary `id` ordering.

## Actions

- Filament actions should delegate domain behavior to `app/Actions` classes.
- Use action labels, modal labels, icons, colors, and notifications consistent with existing actions.
- Use visibility rules based on policies, tenant access, or state transitions.
- For complex create/edit flows, prefer wizard steps when it improves UX.

## Custom components

- Use custom schema/form components only when built-ins cannot express the interaction clearly.
- Keep Livewire exposed methods renderless when the UI state can be updated without full render.
- In Blade components, support responsive and dark-mode behavior when the surrounding UI does.
- Avoid generic AI-looking layouts; preserve the panel's visual language.

## Translations

- Prefer `lang/{locale}/filament.php` or existing translation files for Filament copy.
- Add both English and Dutch copy when the project has both locales.
- Avoid hardcoded labels unless the surrounding project already hardcodes that specific area.

## Testing rule

- Do not create or update Filament tests until the human approves the working version or explicitly asks for tests.
- After approval, use the `outerweb-pest-workflow` skill and cover page load, table columns, search, sorting, filters, actions, policies, validation, notifications, redirects, and persistence.
