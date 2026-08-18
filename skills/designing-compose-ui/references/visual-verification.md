# Visual Verification

Visual claims require rendered evidence when the requested work materially changes composition, styling, imagery, adaptive behavior, or reference matching.

## Discover the Repository's Verification Path

Before creating previews or screenshot tests:

1. Inspect the relevant module build files and source sets.
2. Inspect nearby `@Preview`, screenshot, golden-image, Compose UI, instrumentation, or device-test examples.
3. Inspect repository scripts and CI configuration for existing render or visual-regression commands.
4. Reuse the repository's theme, harness, fixtures, representative state, and naming conventions.
5. Do not assume a particular screenshot library, source set, Gradle task, module name, emulator, or export script exists.

Prefer the narrowest existing mechanism that can produce evidence for the changed visual behavior.

## Choose Evidence by Risk

| Risk | Preferred evidence |
|---|---|
| Hierarchy, spacing, shape, imagery | Deterministic preview or screenshot at the target state and size |
| Theme roles and contrast | Light and dark renders when both are supported; calculate uncertain contrast ratios separately |
| Wrapping and action reachability | Large-font render when text can affect geometry |
| Compact-height overflow or IME | Short-height render plus device or instrumentation evidence when runtime insets matter |
| Adaptive composition | Explicit renders around the repository's actual layout transitions |
| RTL or directional controls | RTL render and semantics review when supported |
| Interaction and state | Compose UI or instrumentation test; screenshots for stable key states |
| Visual regression | Existing screenshot or golden validation against reviewed baselines |

Do not multiply variants mechanically. Select variants that could falsify the design.

## Create Deterministic Render States

When the repository supports preview or screenshot fixtures:

- use the real product theme and relevant shared components;
- use representative content and explicit state rather than random or network-backed data;
- keep callbacks deterministic;
- isolate the state being reviewed from unrelated runtime dependencies when repository conventions permit it;
- add theme, locale, font scale, width, height, or UI-state variants only when they exercise an identified risk.

Do not redesign production APIs solely to make a screenshot fixture convenient.

## Inspect the Render

Review the full image before zooming into details:

1. Is the user job and primary action obvious at first glance?
2. Does the reading path match importance?
3. Is density intentional, with redundant copy and containers removed?
4. Are groups expressed consistently through alignment, spacing, surface, and type?
5. Do artwork, text, and controls cooperate rather than compete?
6. Are content and actions clipped, crowded, or unreachable in risk variants?
7. Do disabled, selected, loading, empty, error, and success states remain understandable when relevant?
8. Does the result still look like the surrounding product rather than a generic Material sample?

A successful build or screenshot task is not visual review. Inspect the produced render or diff before claiming the UI is correct.

## Match a Supplied Image

Keep these artifacts conceptually separate:

- **Target**: the screenshot, mockup, or image supplied by the user. It expresses the desired visual result.
- **Render**: output produced from the current Compose implementation for the matched state.
- **Baseline**: an optional repository-owned screenshot or golden reference used for regression testing. It is not automatically the user's target.

Use this loop:

1. Inspect the target before editing. Identify its state, content, viewport or aspect ratio, theme, system chrome, and ambiguity that affects implementation.
2. Match the render's logical viewport, content, theme, and state as closely as practical. Do not require identical raw pixel dimensions when renderers, densities, font rasterization, or capture chrome differ.
3. Exclude status bars, navigation bars, device frames, and other capture chrome unless they are product UI or the request explicitly includes them.
4. Compare target and render at full-image scale first, then inspect concrete differences in this order:
   - composition and bounds;
   - alignment and spacing;
   - text wrapping, role, size, and weight;
   - color and contrast;
   - shape and elevation;
   - imagery and crop;
   - icon geometry;
   - missing or extra elements;
   - clipping and touch affordance.
5. Record material deltas rather than saying the result merely "looks off".
6. Group related corrections into one pass, implement them, rerender, and compare again.
7. Repeat until no material mismatch remains or a repository, platform, accessibility, or requested-behavior constraint prevents closer matching.
8. Report any remaining deviation together with the constraint that justifies it.

Do not introduce a numeric similarity threshold for targets captured with a different renderer, density, font rasterizer, crop, or system chrome unless the repository already defines an appropriate metric.

## Review Visual Baselines Safely

When a screenshot or golden test changes:

1. inspect the actual render;
2. inspect the expected baseline;
3. inspect the generated diff when the tool provides one;
4. determine whether the change is intentional;
5. only then update or accept the baseline.

Never update a reference image merely to make validation pass.

A passing visual-regression test proves similarity to its accepted baseline. It does not prove usability, accessibility, correctness relative to a user-supplied target, or correctness of runtime behavior.

## Understand Verification Boundaries

Preview and screenshot rendering may not exercise:

- runtime system bars and inset behavior;
- IME interactions;
- TalkBack traversal;
- gestures and pointer arbitration;
- lifecycle and saved-state behavior;
- device-specific rendering differences;
- animation timing or reduced-motion behavior.

Use Compose UI, instrumentation, device, semantics, accessibility, or manual checks when those behaviors are material to the request.

## When No Render Path Exists

If the repository has no practical automated or agent-accessible way to render the changed UI:

1. do not silently introduce a screenshot framework for a small unrelated request;
2. keep or add deterministic Compose previews when that fits repository conventions;
3. run the strongest available compile, lint, Compose UI, semantics, or instrumentation checks;
4. review source-level layout risks explicitly;
5. report that visual conclusions remain hypotheses until rendered evidence is inspected.

Introduce new visual-regression infrastructure only when the requested work or repository-level need justifies that separate engineering change.
