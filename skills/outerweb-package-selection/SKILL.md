---
name: outerweb-package-selection
description: Use when evaluating, adding, updating, removing, or replacing Composer or JavaScript dependencies in an Outerweb project.
license: MIT
metadata:
  owner: Outerweb
---

# Outerweb Package Selection

Use this skill for evidence-first dependency decisions. Loading it authorizes
investigation and a recommendation, not a dependency change.

## Decision order

- Define the required capability and constraints before choosing a package.
- Prefer a fitting framework-native capability or an installed, directly
  declared dependency when it can meet the requirement cleanly.
- Compare that path with focused local code and, only when its net benefit is
  clear, a mature ecosystem package. Account for ownership and upgrade cost,
  not just initial implementation speed.
- Familiarity with a Spatie package may break a genuine tie; it is never a
  mandate or a substitute for project fit and evidence.

## Project and ecosystem evidence

- Inspect applicable project guidance, manifests, lockfiles, workspace files,
  configuration, scripts, imports, registration, and runtime or build usage.
- Determine whether each relevant package is direct, transitive, unused,
  replaced, abandoned, or already represented by another capability. Confirm
  actual use rather than inferring it from a lockfile entry.
- Never make a transitive package part of the application's contract. Propose
  it as an explicitly approved direct dependency first.
- Confirm exact compatibility with the installed language, runtime, framework,
  adjacent packages, platform extensions, build chain, and dependency solver.
- Use authoritative, version-matched framework, package, registry, and package-
  manager documentation. Review maintenance activity, release and security
  status, licence fit, extension requirements, transitive dependencies,
  plugins or install scripts, and replacement or abandonment notices.
- Assess relevant operational implications: configuration and environment,
  deployment and rollback, persisted data and migrations, queues or scheduled
  work, generated assets, bundle size, server-side rendering, browser support,
  and build or CI requirements.

## Package-manager discipline

- Detect the active JavaScript package manager from the project's package-
  manager declaration, lockfile, workspace configuration, scripts, and current
  conventions. Resolve conflicting signals before proposing a command.
- Use the detected manager; never choose or mix npm, pnpm, Yarn, or Bun by
  personal preference. Do not create a second lockfile.
- For Composer work, derive commands and constraints from the installed
  Composer project and solver state rather than assuming a latest version.

## Recommendation and approval

Keep the recommendation concise and include:

- the requirement and material project evidence;
- the preferred path and why its net benefit exceeds local code;
- viable framework-native, installed-package, local-code, and ecosystem
  alternatives, omitting categories that are genuinely inapplicable;
- direct or transitive status, runtime or development classification, and the
  exact compatible constraint decision;
- the exact add, update, remove, or replace command that the active package
  manager would run, without running it; and
- known compatibility, security, licensing, operational, data, build, browser,
  and follow-up implications, as applicable.

Before any command, obtain separate explicit approval for the exact package
add, update, remove, or replacement action; its direct runtime or development
classification; the constraint decision; and the known implications. Approval
of the feature or implementation is not approval of dependency tooling.

## Approved execution

- Reconfirm the approved action, classification, constraint, command, and
  implications immediately before execution. Stop if solver output or new
  evidence materially changes them.
- Use only the active package manager and the approved command. Never hand-edit
  a generated lockfile.
- Inspect every generated manifest, lockfile, script, plugin, configuration,
  asset, and transitive change; ensure unrelated dependency movement is
  understood and within the approved action.
- Run `composer validate` after applicable Composer manifest or lockfile
  changes, then use the project's established verification commands. Load
  `outerweb-quality-tooling` for canonical quality scripts, generated files,
  and post-change checks.
- Dependency approval does not authorize test creation or test-tooling changes.
  Preserve the implementation-review and explicit testing phase; load
  `outerweb-pest-workflow` only when testing scope or execution is applicable.

## Canonical routing

- Route application placement and workflow design to
  `outerweb-laravel-architecture`.
- Route Filament APIs, plugins, and implementation choices to
  `outerweb-filament-admin`.
- Route quality dependencies, Composer scripts, generated files, and
  verification to `outerweb-quality-tooling`.
- Route Pest dependencies, test tooling, coverage, and test execution to
  `outerweb-pest-workflow` and its approval gates.
