---
name: outerweb-guideline-curator
description: Govern proposals and approved persistence for Outerweb agents, focused skills, golden examples, specialist capabilities, and project-local guidance.
license: MIT
metadata:
  owner: Outerweb
---

# Outerweb Guideline Curator

This is the canonical policy for deciding whether observed feedback belongs in
durable guidance and, after exact approval, for persisting one governance batch.
Use it for requests to remember a preference, change Outerweb guidance, capture
a reusable success or anti-pattern, create a specialist capability, save a
golden example, or govern project-local instructions.

The dedicated `guideline-curator` owns persistence. Other agents may surface a
non-persistent candidate, but they must not make it current guidance during an
unrelated feature.

## Classifications and destinations

Classify every proposal as exactly one of:

1. **Always-on agent rule** — short, high-leverage behaviour needed throughout
   an agent's ordinary work. Place it in the smallest applicable
   `~/.config/opencode/agents/*.md` prompt; do not duplicate focused domain
   detail there.
2. **Focused skill** — reusable domain or workflow guidance that should load
   only when applicable. Amend the narrowest existing
   `~/.config/opencode/skills/outerweb-*/SKILL.md` or propose a distinct
   `outerweb-*` skill when no maintained skill owns the concern.
3. **Golden example** — reusable structure or style best demonstrated by a
   sanitized example rather than prompt prose. Place it in the matching
   `outerweb-golden-examples` reference and keep its skill index accurate.
4. **Specialist-agent proposal** — a capability with a distinct mandate,
   context boundary, tools, permissions, or independent ownership that does not
   fit an existing agent. Propose the exact agent file, role, mode, model,
   permissions, workflow, and interaction boundaries before creation.
5. **Project-local rule** — behaviour justified only for the current project.
   Place it in the project's root `AGENTS.md`, `.ai/guidelines`, or
   `.ai/rules`, choosing the project's maintained structure and narrowest
   applicable destination.
6. **Inbox** — a potentially useful observation whose evidence, wording,
   applicability, or destination is not ready for durable guidance. Report it
   as a non-persistent candidate only.
7. **Rejected** — feedback that is incorrect, unsafe, obsolete, duplicative,
   irreducibly proprietary, or too situational to preserve. Explain why and do
   not persist it.

An inbox or rejection decision does not create a durable log. Propose such an
artifact separately if one is genuinely needed.

## Evidence threshold

Global Outerweb guidance requires at least one of:

- an explicit user decision that the behaviour is a global Outerweb standard;
- repeated evidence from independent projects that demonstrates the same
  reusable need or success; or
- authoritative framework, package, security, or tooling behaviour combined
  with a documented Outerweb preference for how to apply it.

One project's code, bug, convention, feedback, or successful implementation
defaults to **project-local rule** or **inbox**. It becomes global only when the
user explicitly globalizes it after reviewing the consequences, including where
it will apply and what projects or stacks it may not fit. Repetition inside one
project is not independent-project evidence.

An initial broad request, silence, a previously expressed preference, or
approval of an unrelated implementation feature is not approval to persist.
Approval is proposal-specific and authorizes one exact batch, not later
proposals.

## Required structured proposal

Before any persistence, provide one decision-ready proposal containing:

- **Observed issue or success:** the behaviour worth preventing, requiring, or
  preserving.
- **Evidence and source scope:** concrete sources and whether they represent one
  project, multiple independent projects, authoritative documentation, or an
  explicit company instruction.
- **Classification and destination:** one classification above and the exact
  proposed location.
- **Proposed outcome or wording:** the durable behaviour, concise wording, or
  example structure to persist.
- **Conflicts, duplication, and staleness:** related current guidance, which
  source controls, and whether to replace, correct, consolidate, or add.
- **Sanitization:** what must be removed or generalized before persistence.
- **Benefit and globalization risk:** expected improvement and where a global
  rule could overfit, conflict, age poorly, or increase prompt cost.
- **Exact files:** every file to create or amend, with no open-ended directory
  scope.
- **Recommendation:** approve for persistence, keep in inbox, make
  project-local, or reject.

In direct mode, end after this proposal and wait. In delegated mode, the Project
Manager must give the curator a brief recording the user's explicit approval of
the exact classification, destination, files, and intended outcome or wording.
Do not interpret a delegation without that record as approval.

## Sanitization

Before proposing durable wording and again before writing, remove or generalize:

- client, customer, tenant, project, product, and person names;
- proprietary business rules, decisions, workflows, data, and domain-specific
  identifiers;
- assumptions tied to one language, a language pair, country, region, or locale;
  express locale behaviour through the project's configured locales instead;
- absolute project or machine paths;
- stack, framework, package, runtime, API, or version assumptions unless the
  destination is explicitly scoped to detected compatible versions;
- branding, colors, domains, URLs, logos, and asset names;
- secrets, credentials, tokens, personal data, confidential identifiers, and
  internal-only references.

Preserve only the reusable structure, decision rule, safety boundary, or
technical pattern. If sanitization removes the proposal's useful substance,
classify it as project-local, inbox, or rejected rather than global.

## Conflict, duplication, and staleness inspection

Inspect the proposed destination, relevant agent and skill indexes, matching
golden references, project-local guidance when applicable, and nearby history
before writing.

- Prefer replacing or correcting an obsolete or inaccurate rule over adding a
  second rule that competes with it.
- Consolidate duplicated guidance into the narrowest source of truth and keep
  only minimal routing text elsewhere.
- Check for stale paths, agent and skill IDs, renamed or removed capabilities,
  fixed versions, commands, framework/package APIs, and runtime assumptions.
- Resolve guidance conflicts by stating the controlling source and preserving
  established precedence rather than silently choosing one.
- Treat any materially different classification, destination, file set,
  permission boundary, or outcome discovered during inspection as a changed
  proposal requiring renewed explicit approval.

Do not reference capabilities that no longer exist. Do not preserve stale names
merely for historical continuity.

## Persistence rules

After exact approval:

1. Reconfirm that approval matches the current classification, destination,
   exact files, and outcome.
2. Apply only that one approved batch for the current governance feature.
3. Edit the smallest set of allowed files and do not rewrite unrelated guidance,
   examples, project code, tests, tooling, or configuration.
4. Keep always-on text concise; move focused detail to a skill and substantial
   structure to a golden example.
5. Stop for renewed approval before any material expansion or deviation.
6. Preserve unrelated staged, unstaged, and untracked work.

The curator never implements an application feature and never invokes a
reviewer. In delegated mode the Project Manager invokes review; in direct mode
the user does.

## Validation and review gates

Agent-, skill-, and OpenCode configuration-only changes have an approved
no-authored-test exception. Do not add or run tests for them. Validate with
static and runtime inspection appropriate to the changed scope:

- run `git diff --check` for the exact changed files;
- run `opencode debug agents` and `opencode debug config`;
- inspect agent and skill frontmatter, path-derived IDs, model, mode, color, and
  V2 permission ordering;
- confirm there are no legacy V1 fields such as `permission`, `tools`, `bash`,
  `task`, `prompt`, `temperature`, `top_p`, `disable`, or `maxSteps`;
- establish skill discovery from `outerweb-guideline-curator` being advertised
  and loadable in a fresh runtime skill catalog/tool context; do not use the
  unsupported `opencode debug skills` command;
- treat the curator loading that exact skill as discovery evidence, and have the
  reviewer independently load it when available;
- do not add registration to `opencode.jsonc` unless runtime evidence proves
  automatic global Markdown discovery is insufficient;
- do not restart the OpenCode service automatically; if discovery is stale,
  report the needed fresh-session and, if still needed, service-restart steps;
- search new governance text for client names, locale assumptions, absolute
  project paths, fixed stack versions, branding and colors, and secret-like or
  confidential content.

After persistence, report the exact files, concise diff outcome, validation
commands and results, sanitization and conflict findings, omitted checks, and
residual risks. The implementation-review/user-approval/no-test-static-
validation/final-reviewer sequence still applies. The governance feature is
complete only when `code-reviewer` returns `APPROVED` or `APPROVED WITH NOTES`.
