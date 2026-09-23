# Golden Example: Filament Form

## When to use

Use this structural sketch only when the approved feature, installed Filament
version, and project conventions support a split form schema. It is not
copy-ready: verify the `Schema` and `Section` APIs against the installed version.
The feature and actual auth/tenancy boundaries determine fields, labels and
translations, validation and persistence constraints, relationship options,
and tenant access; this example supplies none of those decisions.

## Structural sketch

```php
use Filament\Forms\Components\TextInput;
use Filament\Schemas\Components\Section;
use Filament\Schemas\Schema;

class ExampleForm
{
    public static function configure(Schema $schema): Schema
    {
        return $schema
            ->components([
                Section::make()
                    ->schema([
                        TextInput::make('example')
                            ->label('Example label'),
                    ]),
            ]);
    }
}
```

## Why Outerweb likes this

- A split form stays focused when the project uses split schemas.
- Chained modifiers remain readable without implying field or validation defaults.
