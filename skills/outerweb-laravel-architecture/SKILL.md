---
name: outerweb-laravel-architecture
description: Use for Laravel architecture, Action Pattern decisions, DTOs, value objects, casts, observers, enums, state machines, controllers, services, commands, jobs, and domain workflow design in Outerweb projects.
license: MIT
metadata:
  owner: Outerweb
---

# Outerweb Laravel Architecture

Use this skill when deciding where Laravel code belongs or how a workflow should be structured.

## Architecture principles

- Follow the existing project structure first.
- Do not create new base folders without a clear reason or explicit approval.
- Prefer the smallest correct abstraction.
- Keep controllers, Filament pages, Livewire components, and commands thin.
- Put reusable business workflows in Actions when they may be used by API, controllers, Filament, commands, jobs, or tests.
- Ask per feature if the Action Pattern choice is not obvious.

## Action Pattern

- Action classes live in `app/Actions` unless the project already uses a more specific convention.
- Name actions with a full verb phrase and `Action` suffix, such as `CreateAppointmentAction`.
- Use an `execute()` method, not `__invoke()`.
- Type every parameter and return value.
- Wrap multi-write workflows in `DB::transaction()`.
- Use `@throws` PHPDoc when the action can throw framework or domain exceptions.
- Call other actions through the container when matching project convention: `app(OtherAction::class)->execute(...)`.

## PHP style

- Every PHP file should use `declare(strict_types=1);`.
- Use full words for names. Avoid abbreviations except common ones like `id`.
- Use `$exception`, not `$e`.
- Do not mark classes `final` by default; follow the project.
- Prefer Laravel 13 attributes and modern PHP features when the project uses them.
- Add `#[Override]` to overridden methods when the project uses it.
- Prefer PHPDoc blocks over inline comments. Use inline comments only for non-obvious complexity.
- Use array-shape PHPDoc for arrays passed across boundaries.

## Dates and time

- Prefer `CarbonImmutable` for business logic.
- If the app uses `Date::use(CarbonImmutable::class)`, do not introduce mutable `Carbon` without a concrete reason.
- Normalize date/time values inside DTOs or value objects when needed.

## DTOs and value objects

- Use DTOs for structured data crossing action, Filament, Livewire, or serialization boundaries.
- Use constructor property promotion for simple DTOs.
- Use value objects when behavior or validation belongs with the value.
- Implement `Stringable`, `Arrayable`, or `JsonSerializable` only when the value is actually serialized that way.
- Normalize and validate in the constructor or named constructor.

## Models and strictness

- Respect projects that enable `Model::preventLazyLoading()`, `Model::shouldBeStrict()`, and `Model::unguard()`.
- Do not add `$fillable` by default when the project uses `Model::unguard()` and existing models omit fillable/guarded.
- Eager load deliberately to avoid N+1 queries.
- Prefer `cursor()` for read-only seeding or large iteration.
- Enforce morph maps when polymorphic auth/domain models are involved.

## Enums and states

- Enum case names use TitleCase.
- Enums used in UI may implement Filament contracts like `HasLabel`.
- Prefer Spatie Model States for explicit state machines when the domain has transitions.
- Put allowed transitions in the state config and test edge cases after human approval.

## Architecture tests

Outerweb projects may enforce architecture with Pest. Respect these patterns:

- Commands end in `Command` and extend Laravel command classes.
- Controllers end in `Controller` and expose only conventional public methods.
- Models live under `App\Models` and do not end in `Model`.
- Policies end in `Policy`.
- Filament providers end in `PanelProvider`.
- Avoid debug helpers and direct `env()` usage in app code.

Do not add or modify architecture tests until the human approves the implementation or explicitly requests tests.
