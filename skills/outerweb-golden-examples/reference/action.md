# Golden Example: Action

## When to use

Use this structure when a named domain operation merits an Action: it is reused across entry points, coordinates domain changes or external effects, owns atomicity or concurrency, or follows an established project convention. A single-model pass-through does not need an Action just to match an example.

## Structural walkthrough

- The project controls the Action's location, namespace, name, suffix, invocation, and dependency resolution. Use `declare(strict_types=1);` in its PHP file.
- An authorized caller validates and normalizes input at its caller-facing boundary, then invokes a public `execute()` with typed, already validated input. Type every parameter and the result (including `: void` when nothing is returned); return a meaningful domain model or value only when the caller needs one.
- Inside the operation, enforce domain invariants and coordinate the actual domain work across the necessary collaborators. Do not use `ValidationException` as a substitute for boundary validation or authorization.
- Use a transaction only when atomicity, locking, or a protected transition requires one, and keep its boundary as narrow as the workflow permits. Place external effects according to that workflow's consistency requirements, not automatically inside a transaction.
- Add `@throws` PHPDoc when the operation can throw framework or domain exceptions, not as a blanket template.

## Before adapting

The approved feature, installed versions, maintained project conventions, and `outerweb-laravel-architecture` determine the implementation. This structural reference does not authorize new tests, dependencies, or scope. No concrete mutation is shown because an invented operation would imply business rules or package APIs that may not fit the project.
