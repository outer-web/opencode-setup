# Golden Example: Factory

## When to use

Use this shape for Laravel model factories.

## Pattern to copy

- Use `fake()`.
- Use factory relationships for foreign keys.
- Set explicit nullable defaults.
- Use enum helper methods when available.
- Add factory generic PHPDoc.

```php
<?php

declare(strict_types=1);

namespace Database\Factories;

use App\Enums\Locale;
use App\Models\Record;
use App\Models\Team;
use Illuminate\Database\Eloquent\Factories\Factory;

/**
 * @extends Factory<Record>
 */
class RecordFactory extends Factory
{
    public function definition(): array
    {
        return [
            'team_id' => Team::factory(),
            'owner_id' => null,
            'locked_at' => null,
            'first_name' => fake()->firstName(),
            'last_name' => fake()->lastName(),
            'email' => fake()->unique()->safeEmail(),
            'locale' => fake()->randomElement(Locale::supportedCases()),
        ];
    }
}
```

## Why Outerweb likes this

- Defaults are explicit.
- Relationships are generated consistently.
- Faker usage is modern and uniform.
