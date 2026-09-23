---
name: outerweb-filament-admin
description: Use for Filament admin panels, resources, pages, forms, tables, actions, relation managers, auth pages, tenants, panels, notifications, and Filament tests in Outerweb Laravel projects.
license: MIT
metadata:
  owner: Outerweb
---

# Outerweb Filament Admin

Use this skill for Filament work after discovering the target project's installed
stack and established conventions.

## Start from project evidence

- Inspect Composer manifests and the lockfile for the installed Filament major,
  related packages, and plugins before choosing APIs.
- Inspect panel providers, configuration, sibling resources and pages, auth
  setup, policies, tenancy, translations, date and time formatting, and
  project-local guidance before designing the change.
- Use documentation and APIs compatible with the detected package versions.
  Do not infer that an API exists from a newer Filament release or from an
  installed but unused plugin.
- Follow the project's panel namespaces, directories, naming, and generator
  output. Do not copy domain names or paths from examples.
- Load `outerweb-golden-examples` only when a reference would help, and use its
  Filament examples only when their structure, imports, and APIs are compatible
  with the target project. Adapt structure rather than names or business logic.

## Resources and panel structure

- Choose inline or split resource definitions from sibling resources, project
  generators, and the size of the feature. Do not impose split schema, table,
  infolist, or page classes on a project that keeps them inline.
- Keep resource and page classes focused. When the project uses split classes,
  delegate to them consistently rather than mixing structures without a reason.
- Inspect the panel provider before changing discovery, authentication,
  middleware, navigation, domains, paths, assets, themes, or plugins.
- Do not assume a default authenticatable model, guard, password broker, panel,
  or plugin configuration.

## Authorization and tenancy

- Treat policies and authorization checks as the security boundary. Hidden or
  disabled navigation, fields, and actions improve presentation but do not
  replace server-side authorization.
- Authorize page access, records, and mutations with the project's policy and
  guard conventions, including destructive and bulk operations.
- Use the tenancy mechanism configured by the detected Filament version and
  project. Scope resource queries, relation options, lookups, actions, and
  mutations to the authorized tenant.
- Never trust a tenant or record identifier merely because it came from route,
  request, or component state. Reject cross-tenant access and preserve existing
  tenant ownership and membership rules.

## Forms, schemas, infolists, and tables

- Prefer Filament-native fields, layouts, infolist entries, table features,
  actions, validation, and notifications before introducing custom components
  or bespoke Livewire behavior.
- Use component classes, method names, and action placement supported by the
  installed Filament and plugin versions.
- Keep field-specific validation and state transformations near the field when
  that matches the project, while preserving domain invariants below the UI
  boundary.
- Build enum labels and options from the contracts, methods, casts, or mappings
  the project actually provides. Do not assume a universal `supportedCases()`
  helper.
- Make useful columns searchable, sortable, filterable, or toggleable according
  to the workflow and existing table density. Eager load deliberately and use
  default sorting that supports the task.
- Format dates and times with the project's timezone, locale, display format,
  and compatible Filament APIs. Do not impose one timestamp helper or format.

## Actions and workflows

- Load `outerweb-laravel-architecture` when deciding whether behavior belongs
  in a Filament callback, model, domain service, or Action.
- Extract a meaningful named business operation when it is reused, coordinates
  effects, owns atomicity or concurrency, or follows an established project
  pattern. Do not create pass-through Actions for simple component-local work.
- Follow the project's Action location and invocation convention rather than
  requiring a fixed directory or wrapper shape.
- Keep validation and authorization at the appropriate boundary before invoking
  domain behavior. Keep labels, modals, icons, notifications, visibility, and
  post-action navigation consistent with sibling Filament actions.

## Language and interface quality

- Put Filament copy in the project's existing translation structure when that
  is the established convention, and update every locale configured for the
  affected interface. Do not assume a particular language or locale pair.
- Preserve the panel's established visual hierarchy, spacing, density, and
  interaction patterns. Support its responsive layouts and dark mode where
  applicable.
- Preserve accessible labels, descriptions, focus behavior, keyboard use,
  contrast, and error communication. Use custom Blade or Livewire components
  only when native Filament components cannot express the required interaction.

## Testing rule

Do not create or update Filament tests based on an initial request for tests.
The sole authorization is the user's explicit approval, given after they review
the implemented working feature. After that approval, load
`outerweb-pest-workflow` for the applicable Filament test strategy and execution
safeguards.
