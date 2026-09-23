# Golden Example: Filament Resource

## When to use

Use this structural sketch only when the approved feature, installed Filament version, and sibling/project conventions support a split resource. It is not copy-ready: choose the project's model, namespace, imports, routes, and compatible APIs from version-matched documentation. The `Filament\Schemas\Schema` API illustrated below is not for Filament 3.

## Structural sketch

- Keep the resource thin by delegating form and table configuration where split classes are maintained.
- Add an infolist and create/view/edit pages only when the feature needs them and the installed API and project structure support them. Register only the needed pages and routes using project conventions.
- Follow the project's language and configuration for labels; translations are not unconditional.
- Routes and visibility are not authorization. Apply the project's policies, guard, and tenancy boundaries.

```php
// Illustrative only: resolve symbols, signatures, and paths against the target project.
class RecordResource extends Resource
{
    protected static ?string $model = Record::class;

    public static function form(Schema $schema): Schema
    {
        return RecordForm::configure($schema);
    }

    public static function table(Table $table): Table
    {
        return RecordsTable::configure($table);
    }
}
```

## Why Outerweb likes this

- Resource classes remain readable when delegation matches the maintained project structure.
- Form and table concerns stay separate without implying extra pages, infolists, or authorization.
