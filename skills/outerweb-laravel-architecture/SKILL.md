---
name: outerweb-laravel-architecture
description: Use for Laravel architecture, Action Pattern decisions, DTOs, value objects, casts, observers, enums, state machines, controllers, services, commands, jobs, and domain workflow design in Outerweb projects.
license: MIT
metadata:
  owner: Outerweb
---

# Outerweb Laravel Architecture

Use this skill when deciding where Laravel code belongs or how a workflow should be structured.

## Project evidence and compatibility

- Inspect project guidance, Composer manifests and lockfiles, installed PHP and Laravel versions, relevant package versions, and neighbouring code before choosing an API or structure.
- Follow compatible project conventions and version-matched official documentation. Do not assume that an API, attribute, package, directory, suffix, or integration used elsewhere is available or established here.
- Do not install or upgrade packages, introduce a new top-level structure, or broaden the feature merely to obtain a preferred architecture.

## Architecture principles

- Follow the existing project structure first.
- Prefer the smallest correct abstraction.
- Keep controllers, Filament pages, Livewire components, and commands thin.
- Prefer an Action for a named business operation when it is reused across entry points, coordinates models or external effects, owns atomicity or concurrency, or the project consistently structures business operations as Actions.
- Keep simple rendering, straightforward reads, boundary validation and authorization, and component-local state out of no-value pass-through Actions.

## HTTP and Livewire forms

- Use Form Requests for controller-bound user input.
- When compatible Livewire 3+ is already installed and the feature is a first-party server-rendered form, prefer Livewire over adding a controller plus Blade POST form. A thin GET controller or page shell may remain.
- Do not force Livewire for APIs, webhooks, downloads, static or read-only pages, no-JavaScript requirements, Filament-native forms, or projects with another established frontend.
- For non-Filament Livewire form workflows, pair a separate Livewire Form object with a FormRequest as the canonical source of validation rules, messages, and attributes.
- Expose that metadata to the Livewire Form through extension points supported by the installed Laravel and Livewire versions and consistent with the project. Do not require one construction, container-resolution, or delegation API.
- Reusing validation metadata does not by itself execute FormRequest authorization, preparation, normalization, after-hooks, route or authentication context, or dependency injection. Implement applicable authorization and normalization explicitly at a compatible boundary.
- Authorize and normalize explicitly, validate at the boundary, and pass only already validated input to Actions.

## Action Pattern

- Follow demonstrated project conventions for Action locations, namespaces, names, suffixes, dependency resolution, and calls.
- Domain Actions use an `execute()` method with every parameter and return value typed.
- Validate input at the boundary before calling an Action. Actions must trust their typed, validated input and must not throw `ValidationException`; keep validation rules and validation messages in Form Requests, Livewire forms, Filament schemas, or another caller-facing validation layer.
- Use a transaction only when atomicity, locking, or a protected transition requires it; do not wrap every state change or write automatically.
- Use `@throws` PHPDoc when the action can throw framework or domain exceptions.

## PHP style

- Every PHP file should use `declare(strict_types=1);`.
- Use full words for names. Avoid abbreviations except common ones like `id`.
- Use `$exception`, not `$e`.
- Do not mark classes `final` by default; follow the project.
- Use framework attributes and modern PHP features only when the installed versions support them and the project uses or accepts them.
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

- Treat existing `Model::unguard()` usage as observational project evidence only, never a recommendation to introduce or globalize it. Load `outerweb-model-lifecycle` for canonical model, migration, factory, seeder, policy, relation, cast, and mass-assignment guidance.

## Enums and states

- Enum case names use TitleCase.
- Use an explicit state abstraction when transitions, guards, or state-specific behaviour justify it. Do not assume a state package or API; load `outerweb-package-selection` before recommending or changing a dependency.

## Focused guidance and verification

- Load `outerweb-filament-admin` for Filament-specific structure, APIs, authorization, forms, tables, and workflows.
- Load `outerweb-golden-examples` only when a structural example would help. Examples never override project evidence or installed-version compatibility.
- Do not create or modify tests during initial implementation. Only after the human reviews the implementation and explicitly approves test work, load `outerweb-pest-workflow` for canonical Pest, architecture-test, tooling-approval, isolation, and execution guidance.
- Load `outerweb-quality-tooling` for canonical formatting, static-analysis, Composer-script, generated-file, and post-change verification guidance.
