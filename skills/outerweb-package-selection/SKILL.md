---
name: outerweb-package-selection
description: Use when considering Composer or NPM packages, Spatie packages, Laravel ecosystem packages, package installation, package replacement, sortable/translatable/model-state features, phone, money, auth, or known-system implementation choices.
license: MIT
metadata:
  owner: Outerweb
---

# Outerweb Package Selection

Use this skill when a feature might be solved by an existing package.

## Default package posture

- Prefer established Laravel ecosystem packages over custom infrastructure for known systems.
- Prefer packages from Spatie when they fit the problem and project constraints.
- Recommend before installing. Do not add Composer or NPM dependencies without user approval.
- Inspect existing `composer.json`, `package.json`, lock files, config files, and usage before recommending anything.
- If the project already uses a package for the domain, extend that package's existing usage instead of introducing an alternative.

## Spatie preferences

Prefer these when relevant:

- `spatie/eloquent-sortable` for user-controlled ordering.
- `spatie/laravel-translatable` for translatable Eloquent attributes.
- `spatie/laravel-model-states` for explicit state machines and transitions.
- Other Spatie packages when they clearly model a known problem and are actively compatible with the project.

## Other common packages

- Use `brick/money` for money values when exact currency math matters.
- Use `propaganistas/laravel-phone` for phone number validation/casting when already present or fitting the domain.
- Use Laravel official packages first when Laravel provides the feature well.
- For Filament admin features, prefer Filament-native mechanisms before custom UI.

## Recommendation format

When recommending a package, include:

- Why this package fits the feature.
- What custom code it avoids.
- Any migration or persisted-data impact.
- How it integrates with the existing app.
- The install command, but do not run it until approved.

## Installation rules

- Ask before adding or updating packages.
- After package changes, run project-standard commands: `composer validate`, `composer refactor`, `composer analyse`, `composer ide-helper`, or simply `composer clean-code` when available.
- If Laravel Boost is installed, run or preserve `php artisan boost:update --ansi` in Composer update workflow.
- Do not introduce a package for a one-off behavior that is clearer as local code.

## Critical thinking

Avoid package reflexes. Recommend a package only when it improves maintainability, correctness, interoperability, or developer speed enough to justify dependency cost.
