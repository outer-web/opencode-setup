# Golden Example: Seeder

## When to use

Use this small structural illustration for bounded, linked seed data, not as paste-ready code. The approved feature, project schema, authentication and data boundaries, installed APIs, and `outerweb-model-lifecycle` determine the real seed shape.

## Pattern to copy

- Use a factory relationship only when the related model, factory, and relation exist in the project; adapt the association to its schema.
- Keep generated records bounded and free of real personal data, secrets, or privileged access.

```php
<?php

declare(strict_types=1);

namespace Database\Seeders;

use App\Models\Record;
use App\Models\RelatedRecord;
use Illuminate\Database\Seeder;

class RecordSeeder extends Seeder
{
    public function run(): void
    {
        Record::factory()
            ->for(RelatedRecord::factory(), 'relatedRecord')
            ->create();
    }
}
```

## Adapt to the project

- A factory `create()` inserts records each time; it is not idempotent. Follow the project's repeatability strategy and register seeders in dependency order through its established orchestration, unless it intentionally maintains a noncentral seeder topology.
- If the approved workload requires existing records, choose `cursor()`, keyset batching, eager loading, or set-based operations according to the query and write pattern. Do not copy unbounded nested scans or repeated per-record writes.
- A newly created model still needs its model, migration, factory, seeder, and policy unless the user explicitly narrows that model's scope. Follow the `outerweb-pest-workflow` approval gate for any tests; this example authorizes neither tests nor extra scope.
- Never run seeders as validation or treat this example as permission to mutate persistent data.
