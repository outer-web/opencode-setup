# Golden Example: Livewire Form

## When to use

Prefer this shape for a first-party, non-Filament server-rendered form when compatible Livewire 3+ is already installed and maintained project conventions support it. Do not force it for APIs, webhooks, downloads, static or read-only pages, no-JavaScript requirements, Filament-native forms, or a project with another established frontend.

## Structural walkthrough

- **FormRequest:** Keep shared validation rules, messages, and attributes as canonical metadata. If metadata depends on a route, authenticated principal, container service, or other request context, use a context-aware design supported by the installed versions and project rather than assuming it is available from an isolated request object.
- **Livewire Form:** Keep form state separate from the component and reuse that metadata through extension points supported by the installed Livewire and Laravel versions and the project convention. Choose the actual integration only after inspecting the installed APIs; do not prescribe direct construction or a particular method signature.
- **Entry point:** Explicitly authorize the actual operation and relevant record using the project's access rules. Perform relevant input normalization and any extra validation explicitly at the appropriate boundary; explicitly validate form state. Pass only validated fields to meaningful domain work. Use an Action when the operation warrants one or that is the maintained project convention, not as a pass-through by default.
- **PHP structure:** In implemented PHP files, use strict types, full names, and typed method boundaries where the installed stack and maintained project conventions support them. This walkthrough is not runnable code or a namespace, field, policy, guard, translation-key, normalization, or Action template.

## Lifecycle boundary

Reading FormRequest metadata methods does **not** invoke its request lifecycle: `authorize`, `prepareForValidation`, `passedValidation`, `after` validation hooks, route or authentication context, and container injection are not supplied merely by calling those methods. Implement applicable checks and transformations explicitly at a supported boundary; do not assume FormRequest lifecycle behavior has run.

## Before adapting

Project evidence, maintained conventions, installed versions, and version-matched documentation control the implementation. Use `outerweb-laravel-architecture` for boundary and domain design, `outerweb-filament-admin` instead for Filament-native forms, and `outerweb-pest-workflow` only after explicit post-implementation approval for actual Livewire behavior testing. This reference authorizes no tests, dependencies, or additional scope; no tests apply to this guidance-only change.
