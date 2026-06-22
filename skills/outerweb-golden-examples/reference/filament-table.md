# Golden Example: Filament Table

## When to use

Use this shape for Filament tables with searchable columns, filters, grouped actions, eager loading, and sensible sorting.

```php
<?php

declare(strict_types=1);

namespace App\Filament\Admin\Resources\Records\Tables;

use App\Models\Record;
use Filament\Actions\ActionGroup;
use Filament\Actions\BulkActionGroup;
use Filament\Actions\DeleteAction;
use Filament\Actions\DeleteBulkAction;
use Filament\Actions\EditAction;
use Filament\Actions\ViewAction;
use Filament\Tables\Columns\TextColumn;
use Filament\Tables\Filters\TernaryFilter;
use Filament\Tables\Table;
use Illuminate\Database\Eloquent\Builder;

class RecordsTable
{
    public static function configure(Table $table): Table
    {
        return $table
            ->columns([
                TextColumn::make('name')
                    ->label(__('filament.tables.columns.name'))
                    ->sortable()
                    ->searchable(),
                TextColumn::make('email')
                    ->label(__('filament.tables.columns.email'))
                    ->toggleable(isToggledHiddenByDefault: true)
                    ->sortable()
                    ->searchable(),
                TextColumn::make('status')
                    ->label(__('filament.tables.columns.status'))
                    ->toggleable(isToggledHiddenByDefault: true)
                    ->sortable(),
                TextColumn::make('created_at')
                    ->isoDateTime()
                    ->sortable()
                    ->toggleable(isToggledHiddenByDefault: true),
            ])
            ->filters([
                TernaryFilter::make('is_active')
                    ->label(__('filament.tables.filters.is_active'))
                    ->queries(
                        /** @param Builder<Record> $query */
                        true: function (Builder $query): void {
                            $query->whereNotNull('activated_at');
                        },
                        /** @param Builder<Record> $query */
                        false: function (Builder $query): void {
                            $query->whereNull('activated_at');
                        },
                    ),
            ])
            ->recordActions([
                ViewAction::make()
                    ->iconButton(),
                EditAction::make()
                    ->iconButton(),
                ActionGroup::make([
                    DeleteAction::make(),
                ]),
            ])
            ->toolbarActions([
                BulkActionGroup::make([
                    DeleteBulkAction::make(),
                ]),
            ])
            /** @param Builder<Record> $query */
            ->modifyQueryUsing(function (Builder $query): void {
                $query->with('owner');
            })
            ->defaultSort('name', 'asc');
    }
}
```

## Why Outerweb likes this

- Secondary columns are available but hidden by default.
- Row actions stay compact.
- Query eager loading is explicit.
- Filter closures are typed for PHPStan.
