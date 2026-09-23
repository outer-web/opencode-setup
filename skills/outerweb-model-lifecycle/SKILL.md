---
name: outerweb-model-lifecycle
description: Use when creating or changing Laravel Eloquent models, migrations, factories, seeders, policies, relations, casts, scopes, observers, auth models, or model tests in Outerweb projects.
license: MIT
metadata:
  owner: Outerweb
---

# Outerweb Model Lifecycle

Use this skill whenever a task touches Eloquent model creation or behavior.

## Compatibility boundary

- Inspect the installed Laravel, PHP, database, authentication, static-analysis,
  and package capabilities before choosing an API or syntax.
- Follow compatible project conventions and version-matched official
  documentation. Do not introduce a newer framework mechanism merely because
  it is preferred elsewhere.
- Project evidence controls how the bundle is implemented, but historical
  omissions do not weaken the mandatory bundle for a newly created model.
- Do not install or upgrade packages, add tooling, or broaden the approved
  feature to obtain a preferred model pattern.

## Model creation bundle

Every newly created model receives the complete bundle unless the user
explicitly narrows that model's scope:

- Model
- Migration
- Factory
- Seeder
- Policy

Existing models that omit one or more bundle artifacts are not precedent. Do
not backfill unrelated historical omissions unless they are included in the
approved scope.

Connect each artifact through mechanisms the project and installed framework
support. This includes factory association, policy discovery or registration,
and seeder registration in dependency order. If the project intentionally does
not centralize seeders, preserve that topology rather than creating a second
one.

## Model metadata and mass assignment

- Use attributes such as `UseFactory`, `UsePolicy`, `ObservedBy`, `Scope`,
  `Hidden`, and `Override` only when the installed framework supports them and
  the project uses or accepts that metadata mechanism.
- Otherwise use the project's supported conventional discovery, model methods,
  properties, providers, or explicit registration. Do not duplicate metadata
  across competing mechanisms without a compatibility reason.
- Treat existing `Model::unguard()` usage as observational project evidence
  only. Never introduce, enable, or globalize it as part of model work.
- When a project already enables `Model::unguard()` and consistently omits
  mass-assignment declarations, do not add `$fillable` merely to impose a
  different convention. Otherwise preserve the project's secure `$fillable`
  or `$guarded` strategy.

## Policies

- Inspect guards, authenticatable classes, authorization entry points, and
  whether guest authorization is actually required before typing a policy
  principal.
- Type the principal to the project's real authentication topology: use the
  concrete authenticatable, an established shared contract, or another
  supported type that represents the principals that can reach the policy.
  Do not impose universal multi-auth support.
- Make the principal nullable only when the ability intentionally supports
  anonymous access and the framework path can invoke it for guests. Do not make
  every policy nullable by default.
- Treat policy examples as structural only. This skill's inspected
  authentication topology controls principal typing and nullability when an
  example was written for a different topology.
- Implement only abilities exposed by the feature or its framework integration,
  using the project's conventional ability names. Deny unmatched principals
  and access outside the relevant ownership, tenancy, permission, or state
  boundary.
- Keep new policies minimally secure: avoid unconditional allows and broad
  `before` bypasses, and deny destructive abilities unless the approved
  behavior explicitly permits them.
- Keep authorization queries bounded and explicit; do not load collections to
  answer an existence question.

## Relations

- Give every relation an explicit concrete return type such as `BelongsTo`,
  `HasMany`, or `BelongsToMany`.
- Add relation generic PHPDoc in the syntax supported by the installed
  Larastan/PHPStan version. Keep related-model, declaring-model, and custom
  pivot types synchronized with the relation implementation.
- Declare custom pivot generics only when the relation really uses a custom
  pivot model.
- Put relation modifiers on new lines and preserve project conventions for
  inverse relations, keys, morph maps, pivot fields, and timestamps.

## Casts

- Use the project's framework-supported cast declaration. Prefer `casts()` over
  `$casts` only where that method is supported and matches project style.
- Every `casts()` method has an array-shape PHPDoc return directly above it,
  using types understood by the installed static analyzer.
- Keep the PHPDoc and implementation synchronized exactly whenever a cast key,
  class, option, or built-in cast changes. A stale shape is a defect.
- Use enum casts for enum-backed columns. Use custom casts or value objects when
  domain normalization, validation, behavior, or serialization warrants them;
  do not wrap ordinary scalar values without a concrete benefit.
- Ensure value-object storage, nullability, serialization, comparison, and
  round-trip behavior match the column definition and public model contract.

## Migrations

- Treat every migration that may have run in any shared, deployed, or persistent
  environment as immutable. Add a new migration for later schema changes. Edit
  an existing migration only when repository evidence proves it has not run and
  the approved scope permits the edit.
- Put column and constraint modifiers on new lines when chaining them.
- Define foreign keys with the project-supported schema API and choose update
  and delete behavior deliberately. Cascade, set-null, restrict, and no-action
  semantics are all valid when they match lifecycle requirements; never choose
  cascade or set-null mechanically. Nullable foreign keys must agree with any
  set-null action.
- Add required unique constraints and indexes with the schema change, based on
  actual lookup, ordering, and integrity needs. Keep rollback behavior safe and
  symmetrical where the project supports reversible migrations.
- Use generated columns only when they materially improve a repeated query or
  ordering need and the deployed database engine and version support the exact
  expression and index strategy. Otherwise use a compatible query, stored
  value, accessor, or ordinary index as appropriate.

## Factories

- Use `fake()` rather than constructing a faker instance or relying on an
  implicit faker property.
- Use factory relationships for related models instead of unmanaged foreign-key
  literals.
- Use named factory states for meaningful variants that tests or seeders reuse.
- Keep defaults valid, bounded, and side-effect free. Cache an expensive
  repeated fake value or stable configuration lookup only when doing so does
  not accidentally make every generated record identical.
- Use full words in attributes, state names, and variables.

## Seeders

- Keep each required model seeder minimal, bounded, and useful for the project's
  approved local or test data flow. Use factories and `fake()` for generated
  values.
- Do not seed real personal data, secrets, known privileged credentials, or
  production access. Guard environment-specific demo or privileged records and
  follow the project's repeatability strategy.
- Use factory relations and states to create valid linked records. Register
  seeders in dependency order through the project's existing seeder topology.
- Choose iteration by workload. Use `cursor()` for memory-efficient,
  one-record-at-a-time read-only traversal when its single query and hydration
  trade-offs fit. Prefer `lazyById()` or `chunkById()` when rows may be updated,
  stable key progression matters, or work should be processed in batches. Use
  eager loading or set-based writes when they avoid an N+1 query pattern.

## Verification and routing

- Model behavior, persistence, casts, relations, factories, seeders, and
  authorization normally require automated coverage, but do not create or
  modify tests during initial implementation.
- Only after the human reviews the completed implementation and explicitly
  approves post-implementation test work may the same original developer add
  or change tests. Load `outerweb-pest-workflow` for the canonical Pest gate,
  scope, isolation, tooling-approval, and command rules.
- Load `outerweb-quality-tooling` for canonical formatting, static-analysis,
  Composer-script, generated-file, and post-change verification guidance.
  Inspect actual script definitions before running or describing them.
- Run an installed `composer clean-code` after PHP changes when that canonical
  skill requires it, but never assume the script regenerates IDE-helper output.
  Claim regeneration only when the inspected script actually invokes the
  applicable generator. Never hand-edit generated IDE-helper files.
