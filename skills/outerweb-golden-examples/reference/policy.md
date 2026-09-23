# Golden Example: Policy

## When to use

Use this as a small structural illustration, not a multi-auth or tenant template. Before adapting it, inspect the project's guards, reachable authenticatable classes, authorization entry points, installed framework APIs, and policy discovery or registration. The approved feature and `outerweb-model-lifecycle` control which abilities exist and how the policy is connected.

## Illustrative single-auth case

This sketch assumes that only `User` can reach this policy, `User::records()` is an existing ownership relation, and `Record` has an `is_archived` state. Replace those assumptions with the actual project's principal, relationships, permissions, and states. Include `viewAny` only if a framework integration or feature invokes it; this example denies listing while permitting an eligible individual record view. Do not add `create`, `update`, or other abilities solely to complete a template.

```php
<?php

declare(strict_types=1);

namespace App\Policies;

use App\Models\Record;
use App\Models\User;

class RecordPolicy
{
    public function viewAny(User $user): bool
    {
        return false;
    }

    public function view(User $user, Record $record): bool
    {
        return ! $record->is_archived
            && $user->records()->whereKey($record->getKey())->exists();
    }
}
```

## Adapt to the project

- Use a concrete authenticatable for a single reachable auth model, or an established shared contract where that represents the reachable principals. Only when multiple auth models can actually reach the same policy should a broader `Authenticatable` principal plus explicit `instanceof` branches be considered; deny unmatched principals. Make a principal nullable only for an ability intentionally available to guests *and* invoked for guests by the installed framework path. Do not assume guest access.
- Implement only class-level and record-level abilities the feature or its framework integration invokes. Enforce applicable permission, ownership, tenancy, and state boundaries with explicit denial on failure. Use tenant relations or helpers only if they exist and match the project's real tenancy model. A matching numeric ID across different principal types does not establish ownership; check the appropriate relationship and principal type.
- `viewAny` authorizes access to a listing, not the records in its query. Scope the actual query independently to the authorized records; an allowed `viewAny` is not a tenant or ownership filter. Keep authorization existence checks bounded.
- Do not grant destructive abilities without explicit user-approved authorization behavior. Omit or deny abilities that are not permitted; verify the actual gate and policy integration so an absent method cannot be mistaken for a broader grant elsewhere.
- Add `before()` only for an expressly approved superuser bypass. Type it for the principals that can reach this policy, return `null` to defer when the bypass does not apply, and remember that policy `before()` is called only for abilities with a matching policy method. Do not let it silently authorize unrelated abilities.
- Every newly created model still requires its model, migration, factory, seeder, and policy unless the user explicitly narrows that model's scope. Use the project's installed versions, lifecycle conventions, and supported policy discovery or registration; this example authorizes no additional tests, dependencies, or scope.
