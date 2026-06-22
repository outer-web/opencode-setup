# Golden Example: Filament Resource

## When to use

Use this shape for Filament resources in projects that split resources into pages, schemas, and tables.

## Pattern to copy

- Resource class stays thin.
- Form, infolist, and table delegate to dedicated classes.
- Labels come from translations.
- `#[Override]` is used for overridden Filament methods/properties when the project uses it.

```php
<?php

declare(strict_types=1);

namespace App\Filament\Admin\Resources\Records;

use App\Filament\Admin\Resources\Records\Pages\CreateRecord;
use App\Filament\Admin\Resources\Records\Pages\EditRecord;
use App\Filament\Admin\Resources\Records\Pages\ListRecords;
use App\Filament\Admin\Resources\Records\Pages\ViewRecord;
use App\Filament\Admin\Resources\Records\Schemas\RecordForm;
use App\Filament\Admin\Resources\Records\Schemas\RecordInfolist;
use App\Filament\Admin\Resources\Records\Tables\RecordsTable;
use App\Models\Record;
use BackedEnum;
use Filament\Resources\Resource;
use Filament\Schemas\Schema;
use Filament\Support\Icons\Heroicon;
use Filament\Tables\Table;
use Override;

class RecordResource extends Resource
{
    #[Override]
    protected static ?string $model = Record::class;

    #[Override]
    protected static string|BackedEnum|null $navigationIcon = Heroicon::OutlinedRectangleStack;

    #[Override]
    protected static ?string $recordTitleAttribute = 'name';

    #[Override]
    public static function getModelLabel(): string
    {
        return __('filament.resources.records.label');
    }

    #[Override]
    public static function getPluralModelLabel(): string
    {
        return __('filament.resources.records.plural_label');
    }

    #[Override]
    public static function form(Schema $schema): Schema
    {
        return RecordForm::configure($schema);
    }

    #[Override]
    public static function infolist(Schema $schema): Schema
    {
        return RecordInfolist::configure($schema);
    }

    #[Override]
    public static function table(Table $table): Table
    {
        return RecordsTable::configure($table);
    }

    #[Override]
    public static function getPages(): array
    {
        return [
            'index' => ListRecords::route('/'),
            'create' => CreateRecord::route('/create'),
            'view' => ViewRecord::route('/{record}'),
            'edit' => EditRecord::route('/{record}/edit'),
        ];
    }
}
```

## Why Outerweb likes this

- Resource classes remain readable.
- Form/table/infolist concerns are easy to test and evolve.
- Translations are built in from the start.
