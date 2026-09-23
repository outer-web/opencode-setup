# Golden Example: Filament Infolist

## When to use

Use this structural sketch only when the approved feature, installed Filament
version, and project conventions support a split infolist and a contextual
callout. Verify the `Schema`, `Callout`, `Section`, and `TextEntry` APIs against
the installed version. Fields, translations, layout, callout content, and data
visibility must come from the feature and project; this example does not define
authorization or relationship loading.

## Structural sketch

```php
use Filament\Infolists\Components\TextEntry;
use Filament\Schemas\Components\Callout;
use Filament\Schemas\Components\Section;
use Filament\Schemas\Schema;
use Illuminate\Database\Eloquent\Model;

class ExampleInfolist
{
    public static function configure(Schema $schema): Schema
    {
        return $schema
            ->columns(1)
            ->components([
                Callout::make(fn (Model $record): string => __('Viewing details for :name', [
                    'name' => $record->getAttribute('name'),
                ]))
                    ->description(__('Review the fields below.'))
                    ->info(),
                Section::make()
                    ->columns(2)
                    ->schema([
                        TextEntry::make('name')
                            ->label(__('Name')),
                        TextEntry::make('summary')
                            ->label(__('Summary')),
                    ]),
            ]);
    }
}
```

## Why Outerweb likes this

- Record-context messaging stays close to the displayed fields, without
  implying a business status or a relationship lookup.
- Layout is explicit and illustrative; use the project's field, translation,
  and visibility conventions instead of copying these choices.
- The informational callout communicates neutral context, not an authorization
  decision.
