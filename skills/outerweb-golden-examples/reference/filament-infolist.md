# Golden Example: Filament Infolist

## When to use

Use this shape for Filament infolists with contextual callouts and grouped entries.

```php
<?php

declare(strict_types=1);

namespace App\Filament\Admin\Resources\Records\Schemas;

use App\Models\Record;
use Filament\Infolists\Components\TextEntry;
use Filament\Schemas\Components\Callout;
use Filament\Schemas\Components\Section;
use Filament\Schemas\Schema;

class RecordInfolist
{
    public static function configure(Schema $schema): Schema
    {
        return $schema
            ->columns(1)
            ->components([
                Callout::make(function (Record $record): string {
                    if ($record->isVerified()) {
                        return __('filament.infolists.callouts.record_verified.title');
                    }

                    return __('filament.infolists.callouts.record_unverified.title');
                })
                    ->description(function (Record $record): string {
                        if ($record->isVerified()) {
                            return __('filament.infolists.callouts.record_verified.description');
                        }

                        return __('filament.infolists.callouts.record_unverified.description');
                    })
                    ->info(),
                Section::make()
                    ->columns(2)
                    ->schema([
                        TextEntry::make('name')
                            ->label(__('filament.infolists.entries.name')),
                        TextEntry::make('email')
                            ->label(__('filament.infolists.entries.email')),
                    ]),
            ]);
    }
}
```

## Why Outerweb likes this

- Contextual messaging is close to the display schema.
- Layout is explicit and simple.
- UI text is translated.
