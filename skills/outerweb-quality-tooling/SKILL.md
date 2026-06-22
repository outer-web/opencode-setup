---
name: outerweb-quality-tooling
description: Use when working in Laravel projects with composer.json, PHPStan, Pint, Rector, Pest, Laravel Boost, Barryvdh IDE Helper, composer clean-code, or pre-commit hooks. Adds and maintains Outerweb quality scripts and hooks.
license: MIT
metadata:
  owner: Outerweb
---

# Outerweb Quality Tooling

Use this skill whenever a Laravel project needs tooling inspection, setup, maintenance, or post-change verification.

## Core workflow

- Inspect `composer.json` before choosing commands.
- Prefer project Composer scripts over raw vendor binaries.
- Always run `composer clean-code` after PHP/code changes when present.
- If `composer clean-code` is missing in a Laravel project, add the standard Outerweb Composer scripts automatically.
- If an expected script already exists with different behavior, do not overwrite silently. Ask first and explain the difference.
- After editing `composer.json`, run `composer validate`.
- Never hand-edit generated IDE helper files such as `_ide_helper.php`, `_ide_helper_models.php`, or `.phpstorm.meta.php`.
- Regenerate IDE helper output through `composer ide-helper` or `composer clean-code`.

## Standard dev packages

Outerweb Laravel projects should normally include these dev tools:

- `barryvdh/laravel-ide-helper`
- `larastan/larastan`
- `laravel/boost`
- `laravel/pint`
- `pestphp/pest`
- `pestphp/pest-plugin-laravel`
- `rector/rector`
- `driftingly/rector-laravel`

Ask before installing missing packages. Do not add dependencies silently.

## Standard Composer scripts

When missing, add these scripts to `composer.json` without removing existing scripts:

```json
{
  "test": [
    "@php artisan config:clear --ansi",
    "@php vendor/bin/pest --parallel --coverage --min=100 --exclude-group=browser --exclude-group=stress"
  ],
  "test-unit": [
    "@php artisan config:clear --ansi",
    "@php vendor/bin/pest --parallel --group=unit"
  ],
  "test-feature": [
    "@php artisan config:clear --ansi",
    "@php vendor/bin/pest --parallel --group=feature"
  ],
  "test-arch": [
    "@php artisan config:clear --ansi",
    "@php vendor/bin/pest --parallel --group=arch"
  ],
  "test-stress": [
    "@php artisan config:clear --ansi",
    "@php vendor/bin/pest --parallel --group=stress"
  ],
  "test-browser": [
    "@php artisan config:clear --ansi",
    "@php vendor/bin/pest --parallel --group=browser"
  ],
  "setup-git-hooks": [
    "cp -f scripts/pre-commit .git/hooks/pre-commit",
    "chmod +x .git/hooks/pre-commit"
  ],
  "ide-helper": [
    "@php artisan ide-helper:generate",
    "@php artisan ide-helper:meta",
    "@php artisan ide-helper:models -N --reset"
  ],
  "refactor": [
    "@php vendor/bin/rector",
    "@php vendor/bin/pint --parallel"
  ],
  "analyse": [
    "@php vendor/bin/phpstan analyse"
  ],
  "clean-code": [
    "@composer refactor",
    "@composer analyse",
    "@composer ide-helper"
  ]
}
```

## Composer lifecycle scripts

- If `post-update-cmd` exists, ensure it includes `@php artisan boost:update --ansi` when Laravel Boost is installed.
- Ensure `post-update-cmd` includes `@composer setup-git-hooks` when the standard hook is present.
- Ensure `post-update-cmd` includes `@composer refactor` and `@composer ide-helper` when the tools are installed.
- If `post-update-cmd` exists with different entries, append missing entries without removing existing ones.
- If a conflicting behavior exists, ask before changing it.

## Standard pre-commit hook

When missing in a Laravel project where code changes are requested:

- Create `scripts/pre-commit` with the standard hook below.
- Add `setup-git-hooks` to Composer scripts if missing.
- Add `@composer setup-git-hooks` to `post-update-cmd` if missing.
- If the project has a `.git` directory, run `composer setup-git-hooks` after writing the file.
- If `scripts/pre-commit` already exists but differs, do not overwrite silently. Ask first.

Use the emoji version exactly:

```sh
#!/bin/sh

echo "🔍 Running clean-code..."

# Run your composer script
composer clean-code
EXIT_CODE=$?

if [ $EXIT_CODE -ne 0 ]; then
  echo "❌ clean-code failed. Commit aborted."
  exit 1
fi

# Check if any files were modified (Rector, Pint, etc.)
if ! git diff --quiet; then
  echo "⚠️ clean-code made changes."
  echo "👉 Please review and re-stage your files."
  exit 1
fi

echo "✅ Code is clean. Proceeding with commit."
exit 0
```

## PHPStan

- Outerweb uses PHPStan/Larastan at max level: `level: 10`.
- Prefer a minimal `phpstan.neon` with Larastan and Carbon extensions when present.
- Fix PHPStan findings in code instead of weakening rules.

## Pint

- Outerweb uses Laravel Pint with strict rules such as `declare_strict_types`, `strict_comparison`, `ordered_class_elements`, `global_namespace_import`, and `Pint/phpdoc_type_annotations_only`.
- Do not manually fight Pint formatting. Run the script and accept its style unless it conflicts with project-specific code.

## Rector

- Use Rector for automated refactors.
- Laravel projects should use Rector Laravel sets when available.
- Do not add broad Rector changes unrelated to the requested task unless `composer clean-code` makes them.

## Testing rule

Outerweb testing workflow overrides Laravel Boost:

- Do not create, update, or run new tests for implementation work until the human validates the working version or explicitly requests tests.
- Quality tools still run immediately. `composer clean-code` is not optional.
- After human approval, prompt to add Pest tests.
