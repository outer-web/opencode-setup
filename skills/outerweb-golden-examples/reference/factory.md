# Golden Example: Factory

## When to use

Use this small structural illustration for an Eloquent factory, not as paste-ready code. `outerweb-model-lifecycle`, the installed stack, and the project's schema, casts, constraints, authentication, and mass-assignment strategy control the implementation.

## Pattern to copy

- Use `fake()` and a factory-valued foreign key only when the relationship and related factory exist.
- Set `null` only for a column that actually permits it; adapt every field to the schema and casts.
- Keep the factory generic compatible with the installed static analyzer and actual model.

```php
<?php

declare(strict_types=1);

namespace Database\Factories;

use App\Models\Record;
use App\Models\RelatedRecord;
use Illuminate\Database\Eloquent\Factories\Factory;

/**
 * @extends Factory<Record>
 */
class RecordFactory extends Factory
{
    public function definition(): array
    {
        return [
            'related_record_id' => RelatedRecord::factory(),
            'label' => fake()->words(3, true),
            'description' => null,
        ];
    }
}
```

## Why Outerweb likes this

- A factory-valued foreign key creates a related model unless an existing one is supplied or associated. Use only relationships supported by the project.
- Defaults must satisfy real schema and cast constraints; `description` illustrates a nullable default only where that column is nullable. Use `unique()` only for a real uniqueness constraint and a viable value pool; add named states for meaningful variants reused by seeders or tests.
- Generate values per invocation; do not statically cache fake or configuration values when that would make records identical or stale. Use enums and helper methods only when the project, installed versions, and casts support them.
- Follow the project's authentication and mass-assignment controls. Do not introduce `Model::unguard()` or add guarding fields because of this example.
- Every new model still receives a model, migration, factory, seeder, and policy unless the user explicitly narrows that model's scope. This example does not authorize tests, dependencies, tooling, or extra scope.
