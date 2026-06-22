---
name: outerweb-model-lifecycle
description: Use when creating or changing Laravel Eloquent models, migrations, factories, seeders, policies, relations, casts, scopes, observers, auth models, or model tests in Outerweb projects.
license: MIT
metadata:
  owner: Outerweb
---

# Outerweb Model Lifecycle

Use this skill whenever a task touches Eloquent model creation or model behavior.

## Model creation bundle

When creating a model, create the full bundle unless the user explicitly narrows the task:

- Model
- Migration
- Factory
- Seeder
- Policy

Also wire the seeder into `DatabaseSeeder` unless the project intentionally avoids central seeder registration.

## Model attributes

- Use `#[UseFactory(ModelFactory::class)]` when the project uses Laravel factory attributes.
- Use `#[UsePolicy(ModelPolicy::class)]` for models with policies.
- Use `#[ObservedBy(...)]` for observers when present.
- Use `#[Scope]` for local scopes when the project uses attribute scopes.
- Use `#[Hidden([...])]` for auth-sensitive models when appropriate.
- Use `#[Override]` on overridden framework methods such as `casts()`.

## Policies

- Every model gets a policy.
- Policy methods use `?Authenticatable $authenticatable`, not `User $user`.
- This supports multiple auth models such as `Admin`, `Employee`, `Client`, and `User`.
- Check access with `instanceof` for the relevant authenticatable model.
- Cover anonymous access by accepting nullable authenticatables.
- Include `viewAny`, `view`, `create`, `update`, `deleteAny`, and `delete` when relevant.
- Default to denying destructive actions unless the domain explicitly allows them.

Example signature:

```php
public function update(?Authenticatable $authenticatable, Appointment $appointment): bool
{
    if ($authenticatable instanceof Employee) {
        return $authenticatable->salons()
            ->whereKey($appointment->salon_id)
            ->exists();
    }

    return false;
}
```

## Relations

- Add explicit relation return types such as `BelongsTo`, `HasMany`, and `BelongsToMany`.
- Add PHPStan generic PHPDoc to relations.
- Use pivot model generics for custom pivot relations.
- Put relation modifiers on new lines.

Example:

```php
/**
 * @return BelongsToMany<Employee, $this, EmployeeService>
 */
public function employees(): BelongsToMany
{
    return $this->belongsToMany(Employee::class)
        ->using(EmployeeService::class)
        ->withTimestamps();
}
```

## Casts

- Use the `casts()` method instead of a `$casts` property when matching modern Laravel style.
- Every model with a `casts()` method must have an array-shape PHPDoc return type directly above the method.
- This casts PHPDoc is mandatory so PHPStan understands casted attributes.
- Do not add, remove, or change casts without updating the PHPDoc array shape.
- Use custom casts for domain values like money, percentages, phone numbers, and time slots.
- Use enum casts for enum-backed columns.

Example:

```php
/**
 * @return array{
 *     published_at: 'datetime',
 *     status: 'App\\Enums\\Status',
 *     price: 'App\\Casts\\MoneyCast',
 * }
 */
#[Override]
protected function casts(): array
{
    return [
        'published_at' => 'datetime',
        'status' => Status::class,
        'price' => MoneyCast::class,
    ];
}
```

## Migrations

- Put column modifiers on new lines.
- Use `foreignId()->constrained()` and explicit `cascadeOnDelete()` or `nullOnDelete()`.
- Add unique constraints and indexes during migration creation, not as an afterthought.
- Use generated columns when they simplify repeated sorting/searching, if the database supports them.
- Do not modify production-run migrations unless explicitly allowed; create a new migration.

## Factories

- Always use `fake()`.
- Use factory relationships for related models.
- Use states for named variants such as `unverified()` or `unpublished()`.
- Cache expensive repeated fake values or config lookups in static factory properties when useful.
- Use full words in attribute and variable names.

## Seeders

- Always use `fake()` when generating fake data.
- Use factories for model creation.
- Use `cursor()` for iterating existing records in seeders.
- Register model seeders in `DatabaseSeeder` in dependency order.
- Keep seeders realistic enough for local UX and manual validation.

## IDE helper

- After creating or changing models, relations, scopes, casts, factories, or migrations, run `composer clean-code` when available.
- `composer clean-code` should regenerate IDE helper output.
- Never hand-edit generated IDE helper files.
