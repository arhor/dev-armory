# Provenance and Maintenance

This skill is reusable Dev Armory guidance informed by public agent skills and official Android documentation. It does not vendor executable code, third-party assets, or substantial copied passages from those sources.

## Conceptual influences

The design and verification workflow was shaped by ideas found in:

- Anthropic `frontend-design` (Apache-2.0): deliberate hierarchy, visual restraint, product-specific direction, and screenshot-based critique. Web-, CSS-, and DOM-specific guidance was not carried over.
- `wshobson/agents` `mobile-android-design` (MIT): Jetpack Compose, Material 3, adaptive-layout, preview, and touch-target coverage.
- `mdrmuhaimin/agentic-skills` `mobile-ui-ux-designer` (MIT): user-goal-first briefs, state completeness, accessibility contracts, and rendered verification. Its broad cross-platform output format was not adopted.
- `aldefy/compose-skill` (MIT, with Apache-2.0 AndroidX excerpts in the upstream project): progressive Compose references and source-grounded implementation checks. No AndroidX source excerpts are included here.
- `hamen/material-3-skill` (MIT): Compose-oriented Material role and UI-audit concepts. Cross-platform and volatile API claims were excluded.
- `android/skills` and official Android developer documentation (Apache-2.0 or documentation/content terms as applicable): Android platform, Compose, accessibility, adaptive-layout, and screenshot-testing guidance.

The resulting skill intentionally combines these ideas into repository-aware guidance rather than importing one upstream skill wholesale. Product identity, architecture, tooling, and local conventions are expected to come from the repository where the skill is used.

Representative positive activations include requests to design a Compose screen, match a screenshot or mockup, critique an existing render, refine hierarchy or spacing, improve accessibility, or visually verify a Compose UI change.

Representative negative activations include state-only ViewModel changes, navigation-only changes, performance work with no visual impact, business-logic changes, and test-only work with no visual or interaction-design decision.

## Maintenance

Review this skill when any of the following materially change:

- Jetpack Compose or Material 3 design and implementation guidance;
- Android accessibility or semantics recommendations;
- adaptive-layout, window-size, large-screen, foldable, or system-inset guidance;
- official Compose preview, screenshot, golden-image, or related visual-verification tooling;
- the skill's activation boundary or its assumptions about repository-owned design systems and architecture.

Keep the reusable guidance independent of any one application's theme, navigation model, state-management pattern, module layout, screenshot framework, Gradle task, or test harness.

Prefer current official Android documentation for platform-sensitive guidance. When remembered APIs or recommendations may be stale, verify them before updating the skill.

Before incorporating material from another agent skill or repository:

1. identify the upstream source and license;
2. distinguish conceptual influence from copied or vendored material;
3. prefer rewriting reusable principles in Dev Armory's own words;
4. if content is substantially copied or vendored, record the exact upstream source or commit and preserve applicable license or attribution requirements;
5. review imported instructions and scripts for network access, shell execution, credential requests, destructive behavior, and prompt-injection risk before adopting them.

Do not let provenance documentation become an operational dependency. The skill should remain understandable and usable without reading this file during ordinary UI work.