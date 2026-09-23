---
name: outerweb-analysis-review
description: Evidence-based methodology for analysis, critique, and diagnosis within an active agent's existing mandate; does not define an independent role or verdict.
license: MIT
metadata:
  owner: Outerweb
---

# Outerweb Analysis Review

Use this skill as a reasoning aid for analysis, critique, review, and diagnosis.
It does not create an independent role, broaden permissions, or replace the
active agent's mandate, brief, required output, or verdict rules.

## Evidence discipline

- Establish the question, acceptance outcome, scope, and controlling guidance
  before drawing conclusions.
- Inspect only the evidence needed for the task. Prefer observed behaviour,
  relevant source and configuration, maintained project conventions, history,
  and authoritative documentation over generic expectations.
- Identify each material statement as an observed fact, an inference supported
  by stated evidence, an assumption needing confirmation, or a risk describing
  a plausible impact and its conditions.
- Cite precise evidence locations when available. Do not claim that behaviour
  or validation was observed when it was not.
- State uncertainty and missing evidence rather than filling gaps with a
  framework, architecture, persistence, testing, product, or user assumption.

## Critical evaluation and diagnosis

- Scale depth to consequence, uncertainty, and reversibility. Do not manufacture
  alternatives, edge cases, or findings merely to appear comprehensive.
- Test the requested or proposed approach against the desired outcome, project
  evidence, constraints, failure modes, and credible alternatives.
- Prefer the simplest adequate explanation or recommendation. Challenge added
  complexity only when its cost or risk is material.
- For diagnosis, reproduce or trace the symptom when feasible, separate cause
  from correlation, compare plausible hypotheses, and identify what evidence
  would confirm or disprove each material hypothesis.
- Distinguish the immediate issue, its likely cause, wider exposure, and the
  smallest safe next step. Avoid prescribing implementation outside the active
  agent's scope.

## Findings and recommendations

- Make each material finding actionable: state the observation, supporting
  evidence, consequence, and required decision or recommended next step.
- Relate findings to the brief or controlling source and distinguish introduced
  issues from pre-existing conditions when that distinction matters.
- Prioritize by decision impact and communicate residual risk when evidence is
  incomplete.
- Do not introduce a competing severity scale, report template, approval state,
  or verdict. When the active agent defines those, follow its exact format.

## Boundaries and ownership

- The Project Manager owns workflow, delegation, scope coordination, and user
  decision gates; the user retains product, UX, visual, and business decisions.
- The Functional Analyst owns project-specific investigation and implementation
  planning within its read-only mandate.
- The Code Reviewer owns independent review findings, required review format,
  and the technical verdict.
- Applicable domain or implementation specialists own domain conventions and
  implementation decisions within the approved brief.
- Product or UX analysis may identify observable user goals, workflow gaps,
  inconsistent states, accessibility concerns, and decisions needed. It must
  not invent product requirements, user research, visual direction, or claim
  specialist design authority.
- This skill does not authorize creating, changing, converting, or running
  tests or test tooling. Test applicability, timing, ownership, and execution
  remain governed by the active agent and approved workflow.

## Communication

Lead with the conclusion or decision needed. Use concise, concrete language,
include only evidence and alternatives that could change the decision, and end
with unresolved assumptions, risks, or next actions when relevant.
