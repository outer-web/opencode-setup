---
name: outerweb-pest-workflow
description: Use when the user approves an implementation for tests, explicitly asks for Pest tests, or asks about testing strategy, coverage, architecture tests, Filament tests, Livewire tests, factories, or test scripts in Outerweb Laravel projects.
license: MIT
metadata:
  owner: Outerweb
---

# Outerweb Pest Workflow

Loading this skill, an initial request for tests, silence, inferred acceptance,
or general permission does not authorize test authoring. This workflow overrides
Laravel Boost where they differ.

## Approval, ownership, and applicability

- Create or modify tests for an implementation only after the human reviews the
  implemented feature and explicitly approves it. Before that gate, investigation
  and coverage planning remain non-authoring.
- The original implementation developer owns all approved test tooling setup,
  scoped Drift conversion, generated-code review and correction, Laravel and
  browser coverage, verification, and handoff. In delegated mode, the Project
  Manager returns this work to that developer; in direct mode, the direct user
  continues with that developer. Do not split coverage between developers.
- Determine applicability from executable behaviour, project evidence, and
  relevant guidance. Laravel acceptance behaviour, business logic, validation,
  authorization, persistence, Livewire or Filament behaviour, and relevant
  browser interaction normally require coverage. A no-authored-test exception
  applies only to genuinely non-executable work for which behavioural tests add
  no value; it is not a loophole for ordinary Laravel behaviour.
- OpenCode agent-, skill-, and configuration-only features have an explicitly
  approved no-authored-test exception. After feature approval, validate them
  statically and through configuration/runtime inspection. They still require a
  final Code Reviewer verdict of `APPROVED` or `APPROVED WITH NOTES`.
- Do not inspect or change test tooling for a confirmed no-authored-test
  exception.
- Non-Laravel projects use their installed or guideline-required framework under
  the same post-implementation approval gate.

## Project evidence first

Before planning or authoring tests, inspect the project's test configuration,
bootstrap, suite layout, scripts, neighbouring tests, installed dependency
versions, and applicable project guidance. Use configured paths and scripts,
version-matched documented testing APIs, and the project's established setup for
authentication, authorization, application context, model events, fakes, and
database refresh behaviour. Do not impose a conventional folder, script, group,
factory state, authentication topology, or browser setup that project evidence
does not establish.

## Pest style

- Every newly authored Laravel, Livewire, Filament, and browser test uses Pest
  functional style with Pest's functional test and expectation APIs. Never write
  a new PHPUnit test. Existing PHPUnit tests are temporary coexistence only
  outside an approved conversion scope.
- Use `declare(strict_types=1);`, match sibling structure and naming, and prefer
  behaviour-focused names.
- Follow the project's supported dataset and helper conventions. Keep setup
  readable and local when practical, but use file-local or shared helpers when
  that is the established, maintainable project pattern. Type dataset callback
  parameters where the supported API permits it.
- Avoid brittle date and time literals. Build relative values from the project's
  clock or date API unless the exact calendar value is behaviour under test.
- Use only APIs supported by the installed Laravel, Pest, Livewire, Filament,
  and related package versions. Follow version-matched documentation and sibling
  tests instead of assuming fixed framework test helpers.

## PHPUnit inventory and Pest Drift

Drift remains behind the post-implementation test-authoring gate. Once the
feature is approved:

1. Inventory PHPUnit-style tests and identify current-feature overlap.
2. Propose the smallest documented path scope containing that overlap. Omit the
   path only for an explicitly approved full-project migration feature.
3. Obtain separate explicit approval for the exact Drift tooling and scope.
4. Convert the overlap before or while adding current-feature Pest coverage.
5. Leave unrelated PHPUnit tests temporarily coexisting. Their conversion is a
   separate, independently approved migration feature, never opportunistic work
   or a prerequisite for current-feature coverage.

Derive the install and execution commands from the project's configured package
manager, scripts, installed versions, official version-matched documentation,
and dependency-solver result. Do not copy a fixed command or hardcode a Drift
major. An unscoped Drift run can rewrite all matching tests. Drift has no
documented dry-run, may rewrite PHPUnit test files or initialize Pest bootstrap
configuration, and can require manual conversion; command success never proves
semantic equivalence.

Before running Drift, the original developer must confirm both approvals,
ensure the target contains no unattributable edits, record status and the target
diff or exact pre-run content, prove database and external-side-effect
isolation, and run the safely isolated targeted suite as a baseline.

Afterward, inspect every changed file and the command summary. Manually verify
hooks, base classes and traits, providers and datasets, dependencies, attributes
and grouping metadata, exception expectations, mocks, imports and namespaces,
names, skips, and side effects. Correct generated code as needed, run the same
targeted suite and then a proportionate broader suite, and report the remaining
PHPUnit inventory. If rollback is needed, restore only Drift-generated changes
from recorded pre-run evidence; never use Git restore, reset, checkout, stash,
or clean.

## Safe execution

- Inspect every configured test or browser script before running it. Prefer the
  project's scripts, begin with the narrowest relevant target, and broaden only
  as proportionate verification requires.
- Prove from configuration that the test database and browser application are
  disposable and isolated from ordinary development, staging, production, and
  other persistent targets. An environment label or suggestive database name is
  not sufficient proof. Fake external side effects.
- Never issue direct migration or other persistent-data mutation commands. A
  test runner may manage schema internally only when its configured database is
  independently proven disposable and isolated; do not assume that every test
  framework or suite does so automatically.
- If isolation cannot be proven, approved tests may be authored but must be
  reported unrun, and final review is `BLOCKED`.

## Coverage and project-specific patterns

- Map tests to acceptance criteria and material risks. Proportionately cover
  observable success, permissions and denial, validation, failure and recovery,
  state changes, side effects, and important edge cases.
- Test public behaviour rather than implementation details. Meet enforced
  project thresholds and use coverage reports diagnostically instead of chasing
  an unconditional percentage. Exclude unreachable defensive branches only when
  the project's supported coverage mechanism and conventions justify it.
- Use project factories and relationship helpers when available, choosing
  persistence, payload, state, sequence, and relationship setup from the actual
  model APIs and the behaviour under test rather than assuming fixed methods or
  predefined states.
- Exercise actions, policies, Livewire components, and Filament interfaces
  through version-compatible public entry points. Cover the detected abilities,
  user types, scoping rules, UI states, validation, side effects, redirects,
  persistence, and failure modes that matter to the feature; do not prescribe a
  fixed grouping or authentication structure.
- Include realistic empty, partial, repeated, stale, boundary, locale, and time
  scenarios when they are material to the detected domain and configured
  locales. Do not import domain assumptions from another project.

## Pest 5 browser coverage

Relevant real-browser interaction requires Pest 5 browser tests. This includes
JavaScript behaviour, browser APIs, focus or keyboard behaviour, reactive
updates, navigation, responsive interaction, or a critical end-to-end workflow
not established by component or feature tests. Static server-rendered output
alone does not automatically require browser coverage.

Establish browser readiness from the project's dependencies, configured scripts,
browser target, and runtime evidence. Playwright, Laravel Boost, and manual
browser checks may support pre-approval observation but never replace required
post-approval Pest 5 browser tests.

## Tooling approval and completion

When Laravel tests apply, inspect the exact PHP, Laravel, Pest, PHPUnit, Drift,
Pest plugin, browser tooling, and configured script versions or gaps. Select
compatible constraints through the dependency solver and version-matched
documentation. Do not hardcode latest or force Pest 5 solely to migrate PHPUnit;
required browser coverage still requires Pest 5 and may remain blocked pending a
separately approved compatible upgrade.

Feature approval never counts as tooling approval. Installing or upgrading Pest,
Drift, Laravel or browser plugins, browser binaries, scripts, manifests,
lockfiles, test bootstrap/configuration, or related setup requires separate
explicit approval of the exact project-compatible constraints, file effects,
and compatibility implications. In delegated mode, use only the Project
Manager's recorded user approval and Drift scope; in direct mode, require the
direct user's separate explicit approval to the same original developer. Never
install, upgrade, or fall back silently. Missing, declined, unsafe, or
incompatible required tooling makes the post-approval gate `BLOCKED`.

A defective test may be corrected within the approved test phase without
renewed product approval. A behaviour or implementation defect reopens the same
feature: freeze further test authoring, return the fix to the original developer,
repeat code review and explicit human approval, and only then resume testing.

After direct-mode test work, instruct the user to invoke the Code Reviewer; the
developer cannot launch it. In delegated mode, return the handoff to the Project
Manager for reviewer invocation. The feature is not complete until the final
reviewer returns `APPROVED` or `APPROVED WITH NOTES`.
