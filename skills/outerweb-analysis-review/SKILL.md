---
name: outerweb-analysis-review
description: Use for Outerweb analysis tasks, code reviews, UX reviews, architecture reviews, bug diagnosis, product critique, risk assessment, planning, or when the user asks for critical thinking without immediate implementation.
license: MIT
metadata:
  owner: Outerweb
---

# Outerweb Analysis Review

Use this skill when the task is analysis, review, planning, or critique.

## Mindset

- Be critical, not negative.
- Optimize for client-specific solutions that can grow into Laravel/TALL/Filament implementations.
- Separate facts, assumptions, risks, and recommendations.
- Prefer concrete tradeoffs over abstract opinions.
- Challenge unnecessary abstractions, premature packages, and generic UI.

## Code review format

- Findings come first, ordered by severity.
- Include file and line references when possible.
- Focus on bugs, data integrity, authorization, state transitions, N+1 queries, performance, security, behavior regressions, missing quality gates, and missing tests.
- If no findings are discovered, say so and mention residual risks or testing gaps.
- Keep summaries secondary.

## Architecture review

Check for:

- Whether the Action Pattern is appropriate.
- Whether controllers, Filament classes, Livewire components, and commands are too fat.
- Whether domain behavior is reusable by API, UI, and command line.
- Whether models have policies, factories, seeders, migrations, casts, scopes, and relations consistent with Outerweb conventions.
- Whether package choices should be recommended before custom implementation.
- Whether quality tooling and pre-commit enforcement are present.

## UX and product review

- Preserve the existing design system and visual language.
- Avoid generic AI-looking layouts.
- Think through desktop and mobile behavior.
- Consider empty states, loading states, validation errors, permissions, destructive actions, and recovery flows.
- In Filament, consider admin efficiency: table density, filters, tabs, action grouping, sensible defaults, and tenant context.

## Bug diagnosis

- Reproduce when feasible.
- Inspect logs and browser logs through Laravel Boost when available.
- Check database schema and data shape before assuming model behavior.
- Identify the smallest fix and the broader risk.
- Do not create tests until the human approves or asks for tests, but mention which tests should be added after approval.

## Output style

- Be concise.
- Use direct recommendations.
- Ask only the questions needed to avoid a wrong architectural decision.
