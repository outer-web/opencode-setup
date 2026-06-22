# Golden Example: Policy

## When to use

Use this shape for policies in projects with multiple authenticatable models.

## Pattern to copy

- Use `?Authenticatable $authenticatable` instead of `User $user`.
- Check the actual auth model with `instanceof`.
- Cover anonymous access.
- Keep destructive permissions explicit.

```php
<?php

declare(strict_types=1);

namespace App\Policies;

use App\Models\Employee;
use App\Models\Record;
use Illuminate\Contracts\Auth\Authenticatable;

class RecordPolicy
{
    public function viewAny(?Authenticatable $authenticatable): bool
    {
        if ($authenticatable instanceof Employee) {
            return true;
        }

        return false;
    }

    public function view(?Authenticatable $authenticatable, Record $record): bool
    {
        if ($authenticatable instanceof Employee) {
            if ($authenticatable->teams()->whereKey($record->team_id)->exists()) {
                return true;
            }
        }

        return false;
    }

    public function create(?Authenticatable $authenticatable): bool
    {
        if ($authenticatable instanceof Employee) {
            return true;
        }

        return false;
    }

    public function update(?Authenticatable $authenticatable, Record $record): bool
    {
        if ($authenticatable instanceof Employee) {
            if (
                $authenticatable->teams()->whereKey($record->team_id)->exists()
                && ! $record->isLocked()
            ) {
                return true;
            }
        }

        return false;
    }
}
```

## Why Outerweb likes this

- It supports projects with `Admin`, `Employee`, `Client`, or other auth models.
- It makes tenant ownership checks explicit.
- It avoids assuming Laravel's default `User` model.
