# Golden Example: Filament Form

## When to use

Use this shape for Filament v5 schema classes.

```php
<?php

declare(strict_types=1);

namespace App\Filament\Admin\Resources\Records\Schemas;

use App\Enums\Locale;
use Filament\Forms\Components\Select;
use Filament\Forms\Components\TextInput;
use Filament\Schemas\Components\Section;
use Filament\Schemas\Schema;

class RecordForm
{
    public static function configure(Schema $schema): Schema
    {
        return $schema
            ->columns(1)
            ->components([
                Section::make()
                    ->schema([
                        TextInput::make('first_name')
                            ->label(__('filament.forms.labels.first_name'))
                            ->required()
                            ->maxLength(255),
                        TextInput::make('email')
                            ->label(__('filament.forms.labels.email'))
                            ->email()
                            ->nullable()
                            ->maxLength(255)
                            ->unique(ignoreRecord: true),
                        Select::make('locale')
                            ->label(__('filament.forms.labels.locale'))
                            ->required()
                            ->options(
                                collect(Locale::supportedCases())
                                    ->mapWithKeys(function (Locale $locale): array {
                                        return [$locale->value => $locale->getLabel()];
                                    })
                            ),
                    ]),
            ]);
    }
}
```

## Why Outerweb likes this

- Modifier chains are readable.
- Labels are translated.
- Enum options come from the enum instead of duplicated arrays.
