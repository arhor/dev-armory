---
name: writing-tests
description: Write and revise automated tests using repository conventions and behavior-focused structure. Use when adding, updating, fixing, or reviewing tests.
---

# Writing Tests

Write focused, deterministic tests that describe observable behavior and fit naturally into the repository's existing test suite.

## Inspect Before Writing

Before choosing test structure, libraries, helpers, or placement:

1. Read repository instructions such as `AGENTS.md`, `CONTRIBUTING.md`, and relevant local documentation.
2. Read the production code under test, including its public contract and relevant callers, collaborators, models, or state.
3. Inspect the closest existing tests for the same unit, feature, package, or module.
4. Inspect the relevant build and test configuration before choosing a test framework, assertion library, mocking library, source set, test environment, or command.
5. Reuse existing fixtures, factories, fakes, mocks, helpers, rules, and test utilities when they express the intended behavior clearly.
6. Do not introduce a new test dependency when the repository already provides an appropriate tool.

Prefer conventions closest to the code under test when repository conventions are inconsistent, unless they conflict with the mandatory test naming and Given/When/Then rules below.

## Test Observable Behavior

Design tests around the behavior visible through the unit's public or meaningful external contract.

Test relevant behaviors such as:

- outputs and returned values;
- externally visible state changes;
- emitted events or messages;
- failures and error behavior;
- state transitions;
- meaningful interactions with collaborators;
- cleanup and lifecycle effects.

Do not couple tests to incidental implementation details.

Do not expose private implementation details solely to make them testable.

Verify interactions with mocks or test doubles only when the interaction itself is part of the behavior being specified.

## Design Focused Coverage

Keep each test focused on one behavioral expectation.

A single behavior may require multiple assertions when those assertions together describe the same outcome.

Cover the happy path together with meaningful:

- boundary conditions;
- failure cases;
- state transitions;
- absence or empty-state behavior;
- cleanup behavior;
- regressions relevant to the change.

Do not add multiple tests that prove effectively the same behavior.

When fixing a bug, prefer adding a regression test that fails without the fix and passes with it.

Do not weaken assertions, broaden timing, or reduce meaningful coverage merely to make a failing test pass.

## Name Tests by Behavior

Name every test using this semantic pattern:

```text
{subject under test} should {expected behavior} when {given context}
```

The subject under test may be a function, method, class, component, service, endpoint, observable property, command, or other behavior owner.

Adapt the syntax to the language and test framework while preserving the semantic pattern.

Examples:

```text
findLesson should return matching lesson when requested lesson exists

loadUser should return cached user when cache contains requested user

submit should show validation error when required field is empty

uiState should become ready when loading succeeds
```

Keep names specific enough that a failing test communicates what behavior broke without requiring the reader to inspect the test body.

## Use Given / When / Then

Divide every test body into exactly three visible sections, once each and in this order:

```text
// Given

// When

// Then
```

Use the comment syntax appropriate for the language while preserving the
literal section names `Given`, `When`, and `Then`.

### Given

Prepare only what is needed for the behavior under test:

* inputs;
* fixtures;
* dependencies;
* test doubles;
* initial state;
* environment or configuration.

### When

Perform the behavior being tested:

* invoke the unit under test;
* perform the user action;
* emit the event;
* advance the state;
* execute the request.

Keep the primary behavior invocation easy to identify.

### Then

Verify the observable outcome.

Assertions, observable state verification, expected failures, and contractually meaningful interaction verification belong here.

Do not replace these sections with alternatives such as `Arrange`, `Act`, or `Assert`.

Do not add additional Given/When/Then section headers inside the same test.

## Keep Tests Deterministic

Tests should produce the same result independently of execution order, machine, time, or unrelated external state.

Avoid relying directly on:

* arbitrary sleeps or delays;
* real network services;
* wall-clock time;
* uncontrolled randomness;
* filesystem or environment state not owned by the test;
* execution order;
* state leaked from other tests.

Use the repository's existing clocks, schedulers, fake timers, fixtures, temporary resources, dispatchers, fakes, or other deterministic mechanisms when available.

Prefer explicit synchronization over increasing timeouts.

## Preserve Repository Conventions

Follow the repository's established conventions for:

* test framework;
* assertion style;
* mocking or faking style;
* file naming;
* test placement;
* source sets;
* fixtures and factories;
* setup and teardown;
* integration-test infrastructure;
* validation commands.

Do not rewrite surrounding tests solely to impose unrelated stylistic changes.

When a repository convention conflicts with the mandatory behavioral naming or Given/When/Then structure in this skill, preserve the repository's tooling and architecture while applying the mandatory semantic structure to tests being added or changed.

## Run the Narrowest Relevant Validation

While iterating, run the smallest available test scope that exercises the changed behavior.

Prefer, when supported:

1. a single test;
2. a single test suite or class;
3. the owning module's test task;
4. a broader repository test suite.

After the focused test passes, run any broader validation required by the repository or warranted by the scope of the change.

Do not assume test commands, task names, source sets, devices, browsers, or other infrastructure exist. Inspect the repository first.

If the relevant tests cannot be executed, perform the narrowest meaningful static or compilation validation available and report the exact limitation. Never claim that tests passed when they were not run.

## Review Before Finishing

Review every added or changed test and confirm that:

* its name follows `{subject} should {behavior} when {context}`;
* it contains exactly one `Given`, one `When`, and one `Then`, in order;
* it describes observable behavior rather than implementation details;
* it has one focused behavioral purpose;
* its setup contains only relevant state;
* its assertions meaningfully prove the expected behavior;
* it does not duplicate equivalent coverage;
* it is deterministic;
* it follows the repository's existing testing tools and placement conventions;
* it introduces no unnecessary test dependency or helper;
* the narrowest relevant validation has been run when possible.
