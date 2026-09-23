# Golden Example: Model

## When to use

Use this as a small structural illustration for an Eloquent model, not a paste-ready or universal implementation. `outerweb-model-lifecycle`, installed versions, and the actual project schema, auth topology, seeder registration, mass-assignment strategy, and strictness settings control the real model. This example does not authorize tests, dependencies, or extra scope.

## Pattern to copy

- Keep strict typing, concrete relation return types, and generics compatible with the installed static analyzer and actual related model.
- A typed scope is optional; its column and implementation must match the project schema and supported framework API.
- Keep the `casts()` array-shape PHPDoc's keys and literal values exactly in sync with the implementation.
- Factory, policy, and observer attributes are conditional on their companion classes, installed APIs, and project conventions; `#[Override]` is conditional on language support and project convention. Do not introduce an observer as a default.
- Every new model still requires a model, migration, factory, seeder, and policy unless the user explicitly narrows that model's scope. Existing omissions do not override this requirement. Connect the artifacts through the project's supported mechanisms.

```php
<?php

declare(strict_types=1);

namespace App\Models;

use Illuminate\Database\Eloquent\Builder;
use Illuminate\Database\Eloquent\Model;
use Illuminate\Database\Eloquent\Relations\HasMany;

class Record extends Model
{
    /**
     * @return HasMany<RecordItem, $this>
     */
    public function items(): HasMany
    {
        return $this->hasMany(RecordItem::class);
    }

    // Optional: only when the project's schema has this column.
    /** @param Builder<Record> $query */
    public function scopeEnabled(Builder $query): void
    {
        $query->where('is_enabled', true);
    }

    /**
     * @return array{
     *     is_enabled: 'boolean',
     * }
     */
    protected function casts(): array
    {
        return [
            'is_enabled' => 'boolean',
        ];
    }
}
```

## Why Outerweb likes this

- Concrete relation types and compatible generics help static analysis understand relations.
- The casts PHPDoc helps detect drift; it does not prevent drift automatically. Keep it synchronized when a cast changes.
- An existing `Model::unguard()` is observational project evidence, never a reason to introduce it. Follow the project's mass-assignment and strictness choices instead of copying this example as a default.
