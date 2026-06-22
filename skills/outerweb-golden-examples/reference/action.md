# Golden Example: Action

## When to use

Use this shape for reusable business workflows that may be called from Filament, controllers, commands, jobs, APIs, or tests.

## Pattern to copy

- `declare(strict_types=1);`
- `app/Actions` namespace unless project-specific structure differs.
- Full verb phrase class name ending in `Action`.
- Public `execute()` method with typed parameters and return value.
- Transaction boundary around state changes.
- Return the changed domain model or value.

## Do not copy

- Domain names from this example.
- State transition classes unless the target project uses the same state machine.

```php
<?php

declare(strict_types=1);

namespace App\Actions;

use App\Models\Record;
use App\States\Record\Archived;
use Illuminate\Support\Facades\DB;
use Throwable;

class ArchiveRecordAction
{
    /**
     * @throws Throwable
     */
    public function execute(Record $record): Record
    {
        DB::transaction(function () use ($record): void {
            $record->status->transitionTo(Archived::class);
        });

        return $record;
    }
}
```

## Why Outerweb likes this

- The action is single purpose.
- UI layers can call it without knowing implementation details.
- The transaction boundary is explicit.
- The method name `execute()` is consistent across actions.
