# Golden Example: Filament Table

## When to use

Use this split-table shape only when the installed Filament API and the project's resource structure support it. The paired `enabled` column and filter assume an illustrative boolean field; replace or omit both if the schema differs. This is not copy-ready: resolve the namespace, model fields, imports, translations, timezone/date formatting, guard, tenancy, and query conventions from the project.

```php
class RecordsTable
{
    public static function configure(Table $table): Table
    {
        return $table
            ->columns([
                TextColumn::make('name'),
                TextColumn::make('enabled'),
                // Add columns and modifiers only for real fields and useful workflows.
            ])
            ->filters([
                TernaryFilter::make('enabled'),
            ]);
    }
}
```

## Why Outerweb likes this

- Add search, toggle visibility, filters, and default sorting only when they serve the workflow and workload; a hidden column is not access control. Match each filter's name and meaning to the field or explicit query it actually uses.
- Eager load only relationships the table reads. On large data sets, check indexes and query plans for search, filtering, sorting, and relationship access; add a table query modifier only when the project needs one. A table query modifier alone does not secure other resource entry points.
- Add row or bulk actions, especially destructive actions, only when project-approved. Enforce server-side authorization with the project's guard and policies, tenant-safe record selection, and correct per-record and bulk policy handling; UI visibility is not authorization.
- Use typed filter or query callbacks only when the installed Filament version accepts their signatures. Use the project's configured translation and date/time conventions rather than fixed keys, locales, or formats.
