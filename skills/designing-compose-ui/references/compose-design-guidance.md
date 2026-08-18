# Compose Design Guidance

## Hierarchy and Composition

Start with the user's next decision or action. Make the primary content visually dominant through position, scale, contrast, or available area. Use no more than one dominant emphasis in a compact viewport.

- Establish a spacing rhythm from repeated values already present nearby. Treat exceptions as design decisions.
- Use alignment and whitespace as the first grouping tools; containers and dividers are secondary tools.
- Keep action labels specific and consistent across control, confirmation, and error states.
- Avoid equal visual weight for title, metadata, instruction, primary action, and secondary action.
- Preserve representative content during design. Placeholder copy hides wrapping, density, and empty-state failures.
- Spend visual character in one or two places. Let the rest of the composition support them quietly.

For image-led composition, decide whether the image is content, identity, or decoration. Content and identity imagery need meaningful space and deliberate cropping. Place legible text over a localized protective surface or gradient only when necessary; avoid large opaque containers that reduce important imagery to background decoration.

## Material Roles and Product Identity

Material 3 is a component and semantic-token foundation, not a complete product identity.

- Prefer the repository's existing theme roles and design tokens over ad hoc values.
- Pair container and content roles such as `primary` / `onPrimary` and `surface` / `onSurface` instead of selecting colors independently.
- Use typography roles for meaning. Do not encode hierarchy solely with arbitrary `fontSize` or weight.
- Use theme shapes and tonal surface differences consistently. Add shadow only when separation from a busy layer or spatial hierarchy requires it.
- Preserve intentional product color schemes. Dynamic color is an option, not a universal requirement.
- Keep contrast valid in every supported scheme and state, including disabled content and image overlays.
- Reuse product-specific components when they encode deliberate interaction or visual language rather than recreating them from raw Material primitives.

## Adaptive Layout and System UI

Design for the available window, which may resize independently of the physical device.

- Branch on repository-standard window-size APIs or measured constraints when the composition must change.
- Reflow before shrinking. Allow text to wrap, actions to stack, grids to change columns, and supporting panes to move.
- Constrain readable content width on expansive windows; do not stretch paragraphs and forms edge to edge without reason.
- Keep critical content away from folds, hinges, display cutouts, and occlusion regions when the application supports those form factors.
- Consume `Scaffold` padding and deliberate `WindowInsets`; verify status bar, navigation bar, IME, and gesture-navigation interactions when relevant.
- Test at least one compact width and every layout class whose composition materially differs.
- Use a large-font variant when text can influence geometry or action reachability.

Do not branch on device model names. Avoid orientation-specific logic when available space expresses the actual requirement more accurately.

## Accessibility Contract

Define accessibility as behavior, not a final checklist.

- Prefer Material and Foundation controls because they provide interaction and semantics defaults.
- Keep effective touch targets at least 48 dp unless a repository-specific control deliberately expands the semantic or hit target around a smaller visual glyph.
- Provide an accessible name for interactive icons. Use `contentDescription = null` for purely decorative icons or images.
- Express selection, toggle, range, progress, error, and disabled state through semantics and visible cues; never color alone.
- Merge descendants only when a group should be announced as one action. Clear semantics only when replacing them with a complete equivalent.
- Keep traversal order aligned with the visual reading path. Recheck sheets, dialogs, pagers, and custom layouts.
- Use scalable text and avoid fixed-height text containers that clip critical content at larger font scales.
- Verify contrast with an appropriate tool when values are uncertain. Screenshot inspection cannot prove a contrast ratio.
- Add Compose semantics assertions for critical custom controls when the repository's tests support them.
- Use automated accessibility checks when available, then reserve manual TalkBack or device review for behavior automation cannot establish.

## Motion and Interaction

Motion should explain cause, state change, or spatial relationship.

- Prefer one coordinated transition over unrelated animation on every element.
- Keep the task possible with animation disabled or reduced.
- Avoid infinite ambient motion near reading or input unless it is intentional, non-distracting, and can be paused where appropriate.
- Preserve input and scroll state across recomposition and configuration changes when users expect continuity.
- Use whole-surface semantics and click handling for rows and cards when the whole surface is one action.
- Avoid competing nested targets unless each target has a clear, distinct purpose.
- Make loading, pressed, selected, success, and failure feedback distinguishable without relying only on color or motion.

## Compose Implementation Review

Check implementation details after the UX and composition are sound:

- modifier order matches the intended hit area, clipping, drawing, padding, and semantics;
- state is hoisted to the appropriate owning layer and saveability matches repository conventions;
- lazy items have stable keys when identity matters;
- preview inputs are stable, representative, and deterministic;
- user-visible strings follow repository localization practice rather than a new ad hoc mechanism;
- custom Canvas, layout, or pointer-input code is justified over semantic components;
- adaptive branches preserve the same underlying state and actions unless the product intentionally changes behavior;
- tests assert behavior and semantics while screenshots or golden tests assert stable visual output.

## Current Guidance

When a platform API, accessibility recommendation, or adaptive-layout recommendation may have changed, verify it against current official Android documentation before relying on remembered behavior.

Useful official documentation areas include:

- Jetpack Compose accessibility and semantics;
- accessibility defaults for Compose components;
- adaptive Android app guidance and window-size APIs;
- support for different display sizes and canonical adaptive layouts;
- Compose preview screenshot testing.
