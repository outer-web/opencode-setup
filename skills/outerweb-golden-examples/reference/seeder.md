# Golden Example: Seeder

## When to use

Use this shape for realistic local/demo data that links existing records.

## Pattern to copy

- Iterate existing parents with `cursor()`.
- Use factories for creation.
- Copy related attributes deliberately when the seed data should mirror linked records.
- Add extra fake records for realistic local UX.

```php
<?php

declare(strict_types=1);

namespace Database\Seeders;

use App\Models\Record;
use App\Models\Team;
use App\Models\User;
use Illuminate\Database\Seeder;

class RecordSeeder extends Seeder
{
    public function run(): void
    {
        foreach (Team::query()->cursor() as $team) {
            foreach (User::query()->cursor() as $user) {
                Record::factory()
                    ->create([
                        'team_id' => $team->id,
                        'owner_id' => $user->id,
                        'first_name' => $user->first_name,
                        'last_name' => $user->last_name,
                        'email' => $user->email,
                        'locale' => $user->locale,
                    ]);
            }

            Record::factory()
                ->count(10)
                ->create([
                    'team_id' => $team->id,
                ]);
        }
    }
}
```

## Why Outerweb likes this

- The generated data is coherent and useful for manual validation.
- Factories remain the source of fake values.
- `cursor()` avoids loading unnecessary records into memory.
