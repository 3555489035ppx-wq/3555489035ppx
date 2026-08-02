---
name: adaptive-liquid-glass-ui
description: Create and refine Apple-inspired liquid glass interfaces that adapt their tint, contrast, edge light, shadow, blur, and material hierarchy to different backgrounds, brand colors, images, and UI contexts. Use when designing or implementing glassmorphism, Liquid Glass, frosted controls, translucent cards, glass navigation, modal surfaces, or color-aware Apple-like UI in web products.
---

# Adaptive Liquid Glass UI

## Purpose

Build restrained, content-first liquid glass surfaces that feel physical without turning the interface into a collection of identical translucent rectangles. Treat glass as a relationship between the surface, its background, the content above it, and the local light direction.

Use this skill for frontend implementation, visual redesign, component systems, screenshot-based refinement, and responsive UI review. Preserve the product's information hierarchy and brand character; borrow the material behavior, not Apple's exact screens, copy, icons, or proprietary assets.

## Operating principles

1. **Derive, do not hardcode.** Infer the glass tint from the current canvas, nearby image, brand accent, and light/dark mode. Never force the same blue-gray overlay onto every page.
2. **Keep content dominant.** Text, icons, controls, and images stay crisp. Blur belongs behind content and should not be used to hide weak hierarchy.
3. **Use material hierarchy.** Separate canvas, elevated glass, interactive glass, and temporary overlays by opacity, blur, border energy, and shadow - not by adding more gradients.
4. **Make the edge do the work.** A thin asymmetric rim highlight, a soft inner highlight, and a low-contrast contact shadow create more realism than a bright outline.
5. **Respect the host color.** Warm, cool, saturated, monochrome, light, dark, and photographic backgrounds should produce visibly different but coherent glass surfaces.
6. **Use restraint.** Apply glass to surfaces that benefit from depth or context. Keep long-form reading areas and dense tables mostly opaque.
7. **Design the fallback.** When blur or transparency is unavailable, the surface must remain legible and still belong to the same color system.

## Workflow

### 1. Inspect the host before styling

- Read the existing design tokens, layout, typography, interaction states, and target breakpoints.
- Identify the surface behind each candidate glass element: flat color, gradient, image, video, or another glass layer.
- Record the dominant background color and one contextual accent for each major region.
- Check whether the element is content, navigation, action, selection, or transient feedback. Do not give every role the same material.

### 2. Classify the color context

Choose the closest context, then refine from the actual page:

- `dark-neutral`: near-black or charcoal canvas; use low-alpha neutral glass and brighter edge light.
- `light-neutral`: white or pale canvas; use darker text, lower shadow, and a subtle gray/colored tint.
- `chromatic`: a brand color or saturated gradient is present; sample a restrained tint from it and reduce saturation in the glass layer.
- `image`: a photo or illustration sits behind the surface; use a translucent neutral or sampled tint, preserve enough image contrast, and avoid a heavy color wash.
- `high-contrast`: accessibility or dense data needs priority; reduce transparency and increase surface opacity before adding effects.

Expose the context through semantic tokens or a data attribute such as `data-glass-context="dark-neutral"`. Keep the component API independent of raw color values.

### 3. Derive adaptive tokens

Define tokens per surface, not one global magic color. At minimum derive:

- `--glass-tint`: contextual hue used sparingly in the fill and rim.
- `--glass-fill`: translucent fill that separates the surface from its host.
- `--glass-border`: low-contrast boundary; brighten only on focus or selection.
- `--glass-highlight`: top/leading edge light aligned with the chosen light direction.
- `--glass-shadow`: contact shadow that anchors the element without making it float excessively.
- `--glass-blur`: blur and saturation appropriate for the host and performance budget.
- `--glass-ink` and `--glass-ink-muted`: text colors selected against the resulting fill, not the raw page background.

Use `color-mix()` or a small runtime token resolver when supported. Otherwise provide explicit light/dark/chromatic values. For photos, use a known accent or a deliberately neutral fallback instead of pretending CSS can reliably extract a dominant image color on its own.

Read [references/adaptive-liquid-glass.md](references/adaptive-liquid-glass.md) for the token resolver, CSS anatomy, and context examples.

### 4. Build the material in layers

Implement the surface in this order:

1. Base fill and color-mix fallback.
2. Backdrop blur and saturation, only where it improves separation.
3. A thin border with an asymmetric highlight rather than a full white stroke.
4. A soft contact shadow and optional inner highlight.
5. Crisp content above the material layer.

Prefer pseudo-elements or dedicated layers for highlights so content opacity is never reduced. Set `isolation: isolate` when blending or pseudo-elements could leak into neighboring surfaces.

### 5. Map material to UI roles

- **Canvas:** mostly opaque; use atmospheric gradients or blurred background art sparingly.
- **Card/panel:** medium fill, 12-24px blur, quiet border, restrained shadow. Let the underlying color remain perceptible.
- **Primary action:** higher opacity and contrast than a card; use glass only if the label remains immediately readable.
- **Secondary action/pill:** lighter fill and lower shadow; focus/pressed states should change edge light and elevation, not only color.
- **Navigation/tab bar:** one coherent glass plane with selected items expressed by a local capsule or tonal lift.
- **Modal/popover:** highest separation; increase fill opacity, shadow, and backdrop scrim before increasing blur.
- **Dense content:** prefer an opaque or near-opaque surface and reserve glass for headers, toolbars, and controls.

### 6. Add interaction and accessibility states

Define default, hover, focus-visible, pressed, selected, disabled, loading, and reduced-transparency states. Keep the state change local and legible:

- hover: small luminance lift or rim shift;
- focus-visible: clear 2px-equivalent focus indicator with sufficient contrast;
- pressed: reduce elevation and slightly increase fill opacity;
- selected: persistent local tint or inner highlight;
- disabled: reduce contrast carefully, never below the product's minimum readable contrast;
- reduced transparency: remove blur, increase opacity, preserve borders and text contrast.

Respect `prefers-reduced-motion` and `prefers-reduced-transparency`. Avoid animated refraction, shimmer, or noise unless the user explicitly needs a demonstrative prototype.

### 7. Verify the result

Check the implementation at the actual target widths and with at least three host contexts: dark neutral, light neutral, and one chromatic/image background.

- Confirm headings, labels, and body copy remain readable over the strongest background region.
- Confirm images are not covered by glass overlays or pseudo-elements.
- Confirm cards do not become a repetitive grid of equal translucent boxes.
- Confirm controls remain keyboard reachable and focus-visible.
- Confirm the layout does not overflow when copy becomes longer or images use different aspect ratios.
- Confirm the reduced-transparency fallback and mobile layout.
- Capture one before/after screenshot when the material is a portfolio-significant decision.

## Anti-patterns

- Do not use a fixed blue-gray overlay as the definition of liquid glass.
- Do not stack blur on top of blur until the background becomes unreadable.
- Do not use bright white borders around every edge.
- Do not make text translucent to imitate glass.
- Do not put important controls on top of a busy photo without a contrast surface.
- Do not use glass for every section, table row, or paragraph block.
- Do not claim real refraction when the implementation is only a CSS blur; label advanced rendering as a prototype boundary when relevant.

## Delivery expectations

When changing an existing product, first preserve its data flow and component contracts, then add the smallest token and component changes that create the material. Explain which host colors were detected, which tokens were derived, where glass was intentionally not used, and what responsive/fallback checks passed.
