---
name: outerweb-pest-workflow
description: Use when the user approves an implementation for tests, explicitly asks for Pest tests, or asks about testing strategy, coverage, architecture tests, Filament tests, Livewire tests, factories, or test scripts in Outerweb Laravel projects.
license: MIT
metadata:
  owner: Outerweb
---

# Outerweb Pest Workflow

Use this skill only when tests are explicitly requested or the human has approved the working implementation.

## Hard rule

Outerweb testing workflow overrides Laravel Boost:

- Do not create, update, or run new tests for implementation work before human validation.
- After the human says the implementation works or is approved, prompt to add Pest tests.
- When tests are approved, aim for 100% coverage of application code and realistic failure scenarios.

## Test style

- Use Pest functional style with `describe()`, `it()`, `test()`, and `expect()`.
- Use `declare(strict_types=1);` in test files.
- Match sibling test structure and naming.
- Use behavior-focused test names like `can ...`, `does not ...`, `only shows ...`, and `returns no ... when ...`.
- Use inline `->with([...])` datasets beside the test unless the project uses named datasets.
- Type dataset callback parameters.

## Setup conventions

- Check `tests/Pest.php` before writing tests.
- Respect global fakes for HTTP, mail, notifications, queues, events, and database refresh behavior.
- If events are faked while model events are still needed, preserve the Eloquent model event dispatcher like the project does.
- For Filament resource tests, use the project setup for panel, tenant, employee, auth guard, and booting the panel.

## Test organization

- Unit tests live in `tests/Unit`.
- Feature tests live in `tests/Feature`.
- Filament resource tests live under the panel path, such as `tests/Feature/Filament/Salon/Resources`.
- Architecture tests live in `tests/Architecture` when present.
- Browser tests live in `tests/Browser`.

## Commands

Prefer project Composer scripts:

- `composer test`
- `composer test-unit`
- `composer test-feature`
- `composer test-arch`
- `composer test-stress`
- `composer test-browser`

For fast feedback, run targeted Pest or project scripts first. Run broader suites only when needed or before final test handoff.

## Coverage expectations

- Main test script should use Pest parallel coverage with `--min=100` when project tooling supports it.
- Cover every line and branch that matters.
- Use `@codeCoverageIgnoreStart` / `@codeCoverageIgnoreEnd` only for defensive branches that are practically unreachable and already justified by project convention.

## Factories in tests

- Use factories for model setup.
- Use `create()` for persisted state and `make()` for payloads.
- Use factory states instead of manual overrides when available.
- Use `Sequence` for ordered sorting/scope tests.
- Use explicit `attach()` for pivot relationships when the relationship matters to the behavior.

## Action tests

- Resolve actions through the container: `app(Action::class)->execute(...)`.
- Assert model state and related records after execution.
- Cover edge cases and real-world failure modes, not just the happy path.

## Policy tests

- Group by ability with `describe('viewAny', ...)`, `describe('view', ...)`, etc.
- Use `Gate::forUser($authenticatable)->allows(...)` for authenticated cases.
- Use `Gate::allows(...)` for anonymous cases.
- Cover each relevant authenticatable model, tenant-linked and not-linked cases, and destructive denials.

## Filament tests

- Use `Livewire::test(...)` for Filament pages.
- Use `TestAction::make()` for page/table actions.
- Cover page load, table records, search, sorting, filters, tabs, action visibility, action execution, validation, notifications, redirects, and persistence.
- Assert both UI behavior and database/model state.

## Real-life edge cases

Tests should mimic situations that can break production:

- Missing optional contact data.
- Auth models that are not default `User`.
- Tenant-linked versus tenant-unlinked users.
- State transitions that are allowed, denied, repeated, or stale.
- Overlapping schedules and appointments.
- Empty result sets and partially configured domain data.
- Locale, phone, money, time, and timezone edge cases.
