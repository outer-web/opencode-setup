# Golden Example: Model

## When to use

Use this shape for Eloquent models with factory attributes, policy attributes, relations, scopes, and casts.

## Pattern to copy

- PHPStan generics for relations.
- Attribute-based factory, policy, observer, and scopes when the project uses them.
- Mandatory casts PHPDoc directly above `casts()`.
- `#[Override]` on `casts()`.

```php
<?php

declare(strict_types=1);

namespace App\Models;

use App\Enums\Locale;
use App\Observers\RecordObserver;
use App\Policies\RecordPolicy;
use Database\Factories\RecordFactory;
use Illuminate\Database\Eloquent\Attributes\ObservedBy;
use Illuminate\Database\Eloquent\Attributes\Scope;
use Illuminate\Database\Eloquent\Attributes\UseFactory;
use Illuminate\Database\Eloquent\Attributes\UsePolicy;
use Illuminate\Database\Eloquent\Builder;
use Illuminate\Database\Eloquent\Factories\HasFactory;
use Illuminate\Database\Eloquent\Model;
use Illuminate\Database\Eloquent\Relations\BelongsTo;
use Illuminate\Database\Eloquent\Relations\HasMany;
use Override;

#[ObservedBy([RecordObserver::class])]
#[UseFactory(RecordFactory::class)]
#[UsePolicy(RecordPolicy::class)]
class Record extends Model
{
    /** @use HasFactory<RecordFactory> */
    use HasFactory;

    /**
     * @return BelongsTo<Team, $this>
     */
    public function team(): BelongsTo
    {
        return $this->belongsTo(Team::class);
    }

    /**
     * @return HasMany<RecordItem, $this>
     */
    public function items(): HasMany
    {
        return $this->hasMany(RecordItem::class);
    }

    public function isLocked(): bool
    {
        return filled($this->locked_at);
    }

    /** @param Builder<Record> $query */
    #[Scope]
    protected function whereUnlocked(Builder $query): void
    {
        $query->whereNull('locked_at');
    }

    /**
     * @return array{
     *     locked_at: 'datetime',
     *     locale: 'App\\Enums\\Locale',
     * }
     */
    #[Override]
    protected function casts(): array
    {
        return [
            'locked_at' => 'datetime',
            'locale' => Locale::class,
        ];
    }
}
```

## Why Outerweb likes this

- PHPStan can understand relations and casts.
- Model metadata is visible through attributes.
- Scopes are typed.
- The casts PHPDoc prevents static analysis drift.
