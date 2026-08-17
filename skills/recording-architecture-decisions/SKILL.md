---
name: recording-architecture-decisions
description: Record and maintain Architecture Decision Records (ADRs) for durable, cross-cutting engineering decisions. Use when documenting architectural constraints, boundaries, strategies, policies, ownership rules, persistence choices, integration approaches, or long-lived technical tradeoffs and their rationale. Do not use for temporary plans, implementation notes, feature requirements, progress reports, routine documentation, or small local choices.
---

# Record Architecture Decisions

Maintain a durable, consistent architecture decision history using the ADR convention defined by this skill.

Do not treat ADRs as plans, specifications, task lists, or implementation logs.

## ADR convention

Use this convention for ADRs managed by this skill:

- directory: `docs/adr/`;
- index: `docs/adr/README.md`;
- template: `assets/adr-template.md`;
- identifier: four-digit sequential number starting at `0001`;
- filename: `NNNN-short-kebab-case-title.md`;
- date format: `YYYY-MM-DD`;
- statuses:
  - `Proposed`
  - `Accepted`
  - `Rejected`
  - `Deprecated`
  - `Superseded by ADR NNNN`

Every ADR must contain these sections in this order:

1. `Status`
2. `Date`
3. `Context`
4. `Decision`
5. `Consequences`
6. `Alternatives`
7. `References`

Do not introduce additional lifecycle statuses or change the ADR structure unless the skill itself is being changed.

## Handle existing ADR conventions

Before creating or modifying an ADR, inspect `docs/adr/` if it exists.

If the repository already uses this convention, continue using it.

If no ADR convention exists, initialize the convention defined by this skill.

If the repository already contains a materially incompatible ADR convention, do not mix formats or silently migrate existing records. Report the conflict and leave the existing convention unchanged unless the user explicitly asks to migrate it.

A convention is materially incompatible when it differs in ways that would create ambiguous lifecycle, numbering, indexing, or record structure.

## Qualify the candidate

Record an ADR only when the decision:

- is expected to constrain multiple changes, components, or contributors over time;
- establishes a durable architecture or product-engineering boundary, strategy, policy, or tradeoff;
- has meaningful alternatives or consequences;
- benefits from preserving why the choice was made.

Reject the ADR form when the content is primarily:

- a temporary implementation sequence, checklist, milestone, or progress ledger;
- routine setup, contributor instructions, API documentation, or release notes;
- a feature requirement without a durable engineering decision;
- a small local refactor or easily reversible implementation detail;
- volatile truth better represented by executable configuration.

Route rejected material to the artifact that owns it:

- issue or pull request for temporary implementation work;
- contributor documentation for human workflow;
- repository skill for repeatable agent procedure;
- executable configuration for volatile operational truth;
- product documentation for feature behavior or requirements.

## Choose the lifecycle action

### Propose

Create a new ADR with status `Proposed` when the decision is still under consideration.

Allocate the next sequential four-digit identifier by inspecting the existing ADR filenames and index.

Copy `assets/adr-template.md` and replace all placeholders.

Do not reuse missing identifiers.

### Accept

Change an ADR from `Proposed` to `Accepted` only when the decision has actually been made.

Acceptance must be supported by at least one authoritative signal, such as:

- an explicit user instruction;
- repository history showing that the decision has already been adopted;
- an accepted issue, pull request, or other authoritative project record.

Do not turn an agent recommendation into an accepted architecture decision.

Before accepting, ensure the decision, consequences, and alternatives are sufficiently clear.

### Reject

Change an ADR from `Proposed` to `Rejected` when the considered decision has explicitly been declined.

Preserve the proposal and its rationale as historical context.

Do not delete rejected ADRs or reuse their identifiers.

### Supersede

Create a new ADR when an accepted decision is replaced by a new decision.

The new ADR receives a new sequential identifier and follows the normal template.

Change the old ADR status to:

`Superseded by ADR NNNN`

Add a reference from the old ADR to the new ADR.

Add a reference from the new ADR to the superseded ADR.

Do not materially rewrite the old accepted decision.

### Deprecate

Change an ADR status to `Deprecated` when the decision no longer applies and no replacement decision exists.

Explain the reason in the ADR while preserving the historical decision itself.

Do not use `Deprecated` when another ADR replaces the decision. Use supersession instead.

## Preserve decision history

Treat accepted, rejected, deprecated, and superseded ADRs as historical records.

Do not materially rewrite their original context, decision, consequences, or alternatives.

Allowed maintenance is limited to:

- typo and grammar fixes;
- formatting corrections;
- broken-link repair;
- minor clarifications that do not change the original meaning;
- lifecycle metadata and reciprocal references required by deprecation or supersession.

Record substantive changes as a new ADR.

## Handle retrospective decisions

An ADR may document a decision that was made before the ADR existed.

Keep historical facts distinguishable from decisions being made now.

Use the original decision date only when it can be established reliably from repository history or another authoritative source.

Do not invent or estimate historical dates.

When the original date cannot be established reliably, use the date the retrospective ADR is recorded and make the retrospective nature explicit in `Context`.

Do not imply that an undocumented historical alternative was considered unless evidence supports that claim.

## Write the ADR

Copy `assets/adr-template.md` for every new ADR.

### Context

Explain:

- the problem or constraint requiring a durable decision;
- relevant architectural forces and boundaries;
- why the decision matters beyond one local implementation.

Include only context needed to understand the decision.

### Decision

State the adopted or proposed decision precisely.

Define:

- what is being decided;
- where the decision applies;
- important boundaries or invariants;
- what the decision deliberately does not cover when ambiguity is likely.

Do not turn this section into an implementation plan.

### Consequences

Describe meaningful consequences of the decision.

Include both benefits and costs where applicable.

Consider:

- constraints introduced;
- operational or maintenance impact;
- coupling or ownership effects;
- migration or compatibility implications;
- risks and limitations;
- future options enabled or closed.

Do not present only positive consequences.

### Alternatives

Record credible alternatives that were genuinely considered.

For each meaningful alternative, explain briefly why it was not selected.

Do not invent alternatives solely to make the ADR appear complete.

When no meaningful alternative existed, state that explicitly and explain why.

### References

Link relevant authoritative material when available, such as:

- related ADRs;
- issues;
- pull requests;
- architecture documentation;
- authoritative code locations.

Use relative repository links when practical.

Do not duplicate procedural documentation in the ADR.

## Maintain the ADR index

Ensure `docs/adr/README.md` exists.

Use this table structure:

```markdown
| ID                               | Decision         | Status   | Date       |
|----------------------------------|------------------|----------|------------|
| [0001](0001-example-decision.md) | Example decision | Accepted | 2026-01-01 |
```

Keep entries ordered by ascending ADR identifier.

For every ADR, the index must contain:

* the four-digit ID;
* a relative link to the ADR file;
* the ADR title without the `ADR NNNN:` prefix;
* the exact ADR status;
* the ADR date.

Update the index whenever an ADR is created or its lifecycle status changes.

Do not remove rejected, deprecated, or superseded ADRs from the index.

## Verify the result

Before handoff:

* confirm the candidate qualifies as a durable architecture decision;
* verify the four-digit identifier is unique and sequential;
* verify the filename matches `NNNN-short-kebab-case-title.md`;
* verify all required sections exist and appear in the required order;
* verify the status is one of the allowed statuses;
* verify dates use `YYYY-MM-DD`;
* verify the ADR index matches the ADR;
* verify supersession references are reciprocal;
* verify relative links resolve where practical;
* verify historical ADR content was not materially rewritten;
* run relevant repository formatting or validation checks when available;
* run `git diff --check` when working in a Git repository.

Report briefly:

* what ADR was created or changed;
* why the decision qualified for an ADR;
* its resulting lifecycle status;
* any supersession, rejection, or deprecation relationship.

If the candidate did not qualify, report why and where the information belongs instead.
