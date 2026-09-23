---
name: outerweb-quality-tooling
description: Use for evidence-first inspection and safe use of installed Laravel/PHP quality tooling, or to prepare an exact separately approved tooling proposal.
license: MIT
metadata:
  owner: Outerweb
---

# Outerweb Quality Tooling

Use this skill to inspect and safely run the quality tooling a Laravel/PHP
project actually maintains. Loading it authorizes investigation and an exact
proposal, not installation, configuration, generation, or activation.

## Evidence and precedence

Before proposing or running a command, inspect only as deeply as the task needs:

- applicable `AGENTS.md`, project OpenCode instructions, `.ai/guidelines`, the
  relevant `.ai/rules`, and package-specific guidance;
- worktree status and relevant existing diffs so pre-existing work remains
  identifiable and preserved;
- `composer.json`, `composer.lock`, installed versions, Composer plugins, and
  whether each relevant package is a direct or transitive dependency;
- the exact definitions of relevant Composer scripts, every referenced alias or
  subcommand, and applicable install, update, or other lifecycle hooks;
- maintained PHPStan/Larastan, Pint, Rector, Pest/PHPUnit, Laravel Boost, and IDE
  Helper configuration, bootstrap, includes, paths, exclusions, baselines,
  generated targets, and wrappers; and
- the actual Git-hook mechanism, including tracked hook sources, installation
  scripts, configured hook paths, local hooks, and relevant CI enforcement.

Project guidance and maintained project configuration control. Follow their
configured versions, paths, scripts, rule sets, thresholds, and generated-file
policy instead of imposing a generic Outerweb template. Resolve conflicting
signals before acting and report any material conflict. A missing package,
script, hook, lifecycle entry, generated file, or configuration file is not
permission to create it.

## Change and approval boundary

- Never opportunistically add, remove, update, or reclassify a package or tool;
  create or alter a script, hook, lifecycle entry, configuration, or generated
  file; or install or activate a hook.
- Feature approval is not tooling approval. Before any tooling change, obtain
  separate explicit approval for the exact package constraints and
  classification, commands, files, generated effects, script or hook behavior,
  lifecycle side effects, and compatibility implications.
- In delegated mode, act only on the Project Manager's record of that exact user
  approval. In direct mode, obtain it from the user. If solver output or later
  inspection materially changes the proposal, stop for renewed approval.
- Route dependency evaluation through `outerweb-package-selection`. Never
  hand-edit a generated lockfile. Validate an approved Composer manifest or
  lockfile change with `composer validate` and inspect all resulting changes.

## Safe command selection

Inspect a script recursively before execution. Establish what every subcommand
does, which files it can rewrite, whether it invokes a formatter, refactor,
generator, test, package-manager operation, plugin, or lifecycle event, whether
it boots the application, and whether it can reach persistent data, external
services, or unrelated paths.

- Prefer a maintained project script only when its inspected behavior is safe
  for the current phase and scope. A direct installed command can be safer when
  a wrapper contains unrelated or mutating work.
- Run `composer clean-code` after PHP changes only when every nested command has
  been inspected and proven installed, in scope, and safe in the current phase.
  It must not author or rewrite protected tests, alter unapproved tooling or
  setup, install dependencies, invoke unsafe lifecycle behavior, generate
  unapproved output, or mutate persistent data or external systems. This is the
  controlling quality-tooling condition wherever broader routing text says to
  run a defined `clean-code` script.
- If that proof is incomplete, do not run `composer clean-code`. Run only the
  narrow installed checks or supported dry runs whose safety is established,
  and report the omitted command and subchecks with the reason.
- Start with the narrowest relevant files or targets, then broaden only as
  proportionate verification requires. Record the command, scope, result,
  omissions, and every file it changed.
- Never issue a direct migration or other persistent-data mutation command.
  Test-runner-managed schema work is allowed only under the independently
  proven isolation rules in `outerweb-pest-workflow`.
- Never weaken analysis, formatting, refactoring, validation, authorization,
  type-safety, test, or coverage rules merely to make a check pass.

Before a mutating tool runs, preserve scoped pre-run evidence sufficient to
distinguish its output from existing work. Inspect every changed file afterward.
If reversal is needed, restore only tool-attributable changes from that recorded
evidence; never overwrite unrelated work or use destructive Git cleanup.

## Tool-specific guidance

### PHPStan and Larastan

- Inspect the maintained configuration chain, bootstrap, extensions, analysed
  paths, exclusions, baseline or ignored errors, and the installed versions
  before selecting a command.
- Use the project's configured analysis level and rules. Prefer the narrowest
  supported relevant target before the configured broader analysis.
- Correct code findings within scope. Do not lower the level, broaden ignores,
  extend a baseline, or remove an extension to obtain a pass.

### Pint

- Inspect the project's Pint configuration or preset, exclusions, script
  options, and targeted-file support. The maintained project style controls.
- Prefer a supported check-only mode for verification. Run a mutating format
  only against attributable in-scope files, then inspect every edit; never
  replace project rules with a universal ruleset.

### Rector

- Inspect the installed Rector and integration versions, configuration, sets,
  bootstrap, skips, configured paths, and Composer wrapper before use.
- Begin with the supported dry-run and narrowest relevant configured target.
  Apply changes only when the current implementation scope authorizes the
  refactor, and manually review every transformation.

### IDE Helper

- Inspect the installed package, maintained configuration, exact Artisan or
  Composer wrapper, model-inspection behavior, generated targets, and project
  tracking policy. Never infer that `clean-code` invokes IDE Helper.
- Never hand-edit generated helper output. Generation is a mutating tooling
  change, not a validation step; run it only when its exact files and side
  effects are approved and safe, then inspect every generated diff.

### Laravel Boost

- Detect Boost from the manifest and lockfile, then inspect maintained Boost
  configuration, available MCP capabilities, scripts, and lifecycle entries.
  Use version-matched documentation and observational capabilities only when
  relevant.
- Do not assume Boost is installed or prescribe a version. Never install,
  update, configure, generate, or record guidance through Boost, or invoke a
  Boost lifecycle command, without exact approval and inspected side effects.
  Do not use mutating runtime capabilities as quality checks.

## Hooks

- Detect the project's real hook mechanism and deployment path before proposing
  anything. Do not prescribe a universal hook file or installation template.
- Inspect every command a hook can call. A hook must preserve and return the
  exact failing command status without masking failures through pipelines,
  command chaining, or later successful commands.
- Base decisions on command exit status and scoped file evidence, not fragile
  parsing of human-readable output. Do not attribute a whole dirty worktree to
  the hook or tool; distinguish pre-existing, staged, unstaged, and generated
  changes within the relevant scope.
- Editing a tracked hook, changing its installer, selecting a hook path, and
  installing or activating it are separate side effects that require inclusion
  in the exact approved proposal.

## Pest and test tooling

`outerweb-pest-workflow` is canonical for test authoring, Pest and Drift,
browser coverage, test-tooling approval, database and external-side-effect
isolation, execution, and completion. Its rules override summaries here:

- Do not create or modify tests until the human has reviewed the implementation
  and explicitly approved post-implementation test work. The same original
  developer owns the approved test phase.
- Use Pest functional style for newly authored Laravel, Livewire, Filament, and
  browser tests. Drift conversion remains post-approval, requires separately
  approved tooling and the smallest exact current-feature scope, and never
  permits opportunistic project-wide conversion.
- Relevant browser behavior requires the canonical real-browser Pest coverage;
  Boost, Playwright, or manual checks do not replace it.
- Installing or changing Pest, Drift, plugins, browser binaries, scripts,
  bootstrap, configuration, manifests, or lockfiles requires separate exact
  tooling approval and project-compatible constraints.
- Inspect each test command and independently prove disposable database,
  application, and external-side-effect isolation before running it. Meet
  project-enforced coverage thresholds; never impose a blanket percentage.

OpenCode agent-, skill-, and configuration-only changes retain their approved
no-authored-test exception and use static/runtime validation plus final review.
That exception never extends to application code, scripts, hooks, generators,
commands, or any other executable behavior.

## Reporting

Report the inspected project controls; exact commands and scopes; pass, failure,
and omission results; changed or generated files; attribution limits; and any
approval, compatibility, isolation, or safety blocker. Do not claim a broad
quality pass when only targeted checks ran.
