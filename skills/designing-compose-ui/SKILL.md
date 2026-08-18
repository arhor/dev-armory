---
name: designing-compose-ui
description: >-
  Design, critique, refine, implement, or visually verify Android UI built with Jetpack Compose. Use for new screens,
  screenshot or mockup implementation, focused visual polish, hierarchy, spacing, typography, color, shape, density,
  adaptive layouts, accessibility, motion, interaction design, and Compose design-system work. Do not use for Compose
  changes limited to state, navigation, business logic, performance, or tests with no visual or interaction-design decision.
---

# Designing Compose UI

Produce focused Compose UI work that respects the product's existing visual language, preserves unrelated behavior, and is judged from rendered evidence when visual quality matters.

## Inspect Before Designing

Before choosing layout, components, styling, or verification strategy:

1. Read repository instructions such as `AGENTS.md`, `CONTRIBUTING.md`, and relevant local documentation.
2. Inspect the target feature's route or entry point, screen, state, components, previews, tests, and nearby UI.
3. Inspect the repository's theme, typography, color roles, shapes, shared components, icons, imagery, and design-system code.
4. Read any repository-specific visual, product, accessibility, or interaction guidance that applies to the feature.
5. Read [Compose design guidance](references/compose-design-guidance.md) for every design or implementation task.
6. Read [Visual verification](references/visual-verification.md) before planning rendered checks or reviewing a supplied image.
7. Read [Provenance and maintenance](references/provenance.md) only when updating this skill or incorporating guidance from external sources.

Repository-specific design rules are authoritative. This skill supplies a reusable design process, not a product identity.

Do not introduce a new UI library, screenshot framework, design token system, navigation pattern, or state-management pattern merely because it is familiar. Discover and reuse the repository's existing choices unless the requested work explicitly changes them.

## Classify the Task

Choose the narrowest matching mode before editing:

- **Critique**: inspect the current render or supplied screenshot first; report strengths and prioritized problems before proposing edits.
- **Focused refinement**: identify the smallest coherent visual or interaction correction and preserve unrelated behavior and product identity.
- **New UI**: establish the user job, hierarchy, states, visual direction, reuse plan, and verification matrix before code.
- **Image-led UI**: treat important imagery as structural content or identity rather than decoration; preserve legibility without burying it under unnecessary surfaces or copy.
- **Reference match**: inspect the supplied image before editing, reproduce its relevant state and viewport as closely as repository constraints permit, then follow the render-compare-iterate workflow in [Visual verification](references/visual-verification.md).

If no render is available, inspect the code but label visual conclusions as hypotheses. Do not claim visual polish from source inspection alone.

## Form the Design Intent

Before editing, establish a compact internal brief containing:

- the user job and primary action;
- the ordered information hierarchy;
- the product-specific visual language or signature that must be preserved;
- existing theme roles and components to reuse;
- clutter or redundant explanation to remove or combine;
- loading, empty, error, disabled, selected, and success states that matter;
- compact, large-font, and wider-window behavior;
- the accessibility contract;
- the exact preview, screenshot, UI, or semantics checks justified by the change.

Prefer subtraction. Every label, chip, divider, surface, instruction, icon, and animation should communicate hierarchy, state, action, grouping, or product character. Remove it when it does none of those jobs.

## Critique Before Changing

Evaluate material UI problems in this order:

1. User job and action clarity.
2. Hierarchy and reading path.
3. Content density and redundant explanation.
4. Composition, spacing rhythm, alignment, and grouping.
5. Typography, color-role pairing, shape, elevation, imagery, and motion.
6. Touch targets, semantics, contrast, font scaling, system insets, and adaptive behavior.
7. Consistency with nearby product UI and the repository's design system.

Separate findings into:

- **UX problem**: the structure, priority, copy, state, or interaction is wrong.
- **Implementation problem**: the intended design is sound but the Compose code, modifier order, semantics, sizing, or state handling is wrong.

For each material finding, cite visible or source evidence, state the user impact, and propose a bounded correction. Preserve what already works. Do not turn a focused request into a broad redesign.

## Implement Idiomatically

- Preserve the repository's navigation, state ownership, event flow, architecture, and public screen contracts unless the requested UX intentionally changes them.
- Prefer existing components and `MaterialTheme` roles. Introduce a reusable component only for a repeated semantic pattern or an intentionally shared design-system primitive.
- Hoist interaction state and callbacks according to repository conventions; keep previews deterministic and free of unnecessary runtime dependencies.
- Prefer semantic Material and Foundation controls over low-level gesture handling. Add custom semantics only when defaults do not express the action, role, value, state, or traversal correctly.
- Keep decorative imagery and icons out of the semantics tree. Describe meaningful imagery by purpose rather than appearance.
- Use scalable text styles and allow content to reflow. Avoid fixed heights around text and actions.
- Make adaptive layout decisions from available window space or repository-standard adaptive APIs rather than device names or orientation checks.
- Use motion to explain state, cause, or spatial continuity. Keep it nonessential and respect reduced-motion behavior when the repository or platform supports it.
- Preserve existing behavior and tests unless the requested design intentionally changes the contract.

## Verify From Rendered Output

Choose evidence according to risk instead of multiplying previews mechanically.

1. Inspect any supplied target image before editing and keep its represented state, viewport, theme, and content explicit.
2. Discover the repository's existing preview, screenshot, golden-image, instrumentation, or UI-test infrastructure before choosing a verification mechanism.
3. Create or update the narrowest deterministic render or test that exercises the changed state.
4. Include only risk-relevant variants such as light/dark theme, large font, compact height, wider window, RTL, or meaningful UI states.
5. Generate or capture rendered output using repository-supported tooling.
6. Inspect the full render first, then inspect details. For a reference match, compare the render directly with the supplied target and record concrete differences before changing code again.
7. Apply related corrections as a batch, render again, and re-inspect. Repeat until no material mismatch remains or a repository, platform, accessibility, or requested-behavior constraint prevents closer matching.
8. Run the narrowest relevant screenshot, UI, semantics, compile, lint, or repository validation proportional to the change.

Never update a screenshot or golden baseline merely to make a failure pass. Review the actual, expected, and diff first and state why any changed baseline is intentional.

If the repository has no practical rendered-verification path, do not invent one casually for a small change. Perform the strongest available static, preview-source, compile, UI, or semantics validation and report the rendering limitation explicitly.

## Review Before Finishing

Confirm that:

- the primary user job and action remain clear;
- hierarchy, spacing, grouping, and density are intentional;
- product-specific visual identity comes from the repository rather than this skill;
- theme roles, shared components, and architecture are reused where appropriate;
- text can scale and reflow without critical clipping;
- controls have appropriate semantics and touch behavior;
- adaptive behavior follows available window space;
- rendered evidence was inspected when visual quality or reference matching mattered;
- visual baselines were not accepted blindly;
- validation claims match the checks that actually ran.

## Hand Off the Result

Report:

- the design outcome and what was deliberately preserved, removed, or changed;
- files and user-visible behavior changed;
- rendered variants inspected and concrete visual observations;
- remaining differences from a supplied reference and the constraint or tradeoff behind each one;
- deterministic checks run and their results;
- known tradeoffs or remaining human-design decisions.

Do not use vague conclusions such as "cleaner" or "more modern" without naming the observable change.
