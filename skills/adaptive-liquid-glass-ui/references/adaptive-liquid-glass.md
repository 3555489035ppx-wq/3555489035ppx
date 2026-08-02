# Adaptive Liquid Glass Reference

Use this reference when a task needs concrete token derivation or CSS structure. Keep the values as starting points; tune them against the real host background and content contrast.

## Token derivation

Represent the context with a base surface, a contextual tint, and a mode. The tint may come from a brand token, a known image accent, or a neutral fallback. Do not sample pixels during every render unless the product already has a reliable color extraction path.

```js
function getGlassTokens({ surface, tint, mode = "auto" }) {
  const light = mode === "light" || (mode === "auto" && relativeLuminance(surface) > 0.42);
  return {
    "--glass-tint": tint,
    "--glass-fill": light
      ? `color-mix(in srgb, ${tint} 10%, rgba(255,255,255,.72))`
      : `color-mix(in srgb, ${tint} 13%, rgba(16,22,28,.62))`,
    "--glass-border": light ? "rgba(40,52,62,.16)" : "rgba(235,244,250,.18)",
    "--glass-highlight": light ? "rgba(255,255,255,.78)" : "rgba(255,255,255,.30)",
    "--glass-shadow": light ? "rgba(24,32,38,.16)" : "rgba(0,0,0,.30)",
    "--glass-ink": light ? "#172027" : "#f3f7f8",
    "--glass-ink-muted": light ? "#59666d" : "#aebbc1",
    "--glass-blur": light ? "18px" : "22px"
  };
}
```

If `color-mix()` is unavailable, provide an explicit fallback before the modern declaration:

```css
.glass-surface {
  background: rgba(24, 31, 36, .82);
  background: var(--glass-fill);
}
```

Prefer semantic context selectors over page-specific selectors:

```css
[data-glass-context="warm"] { --glass-tint: #c98262; }
[data-glass-context="cool"] { --glass-tint: #719bc7; }
[data-glass-context="green"] { --glass-tint: #7ba78d; }
[data-glass-context="neutral"] { --glass-tint: #b7c4cc; }
```

## Surface anatomy

Use one material class with tokens, then compose role modifiers. Keep content in normal flow above the decorative layers.

```css
.glass-surface {
  position: relative;
  isolation: isolate;
  overflow: clip;
  color: var(--glass-ink);
  background: rgba(24, 31, 36, .82);
  background: linear-gradient(145deg,
    color-mix(in srgb, var(--glass-highlight) 9%, transparent),
    transparent 42%), var(--glass-fill);
  border: 1px solid var(--glass-border);
  box-shadow:
    inset 0 1px 0 color-mix(in srgb, var(--glass-highlight) 34%, transparent),
    0 18px 42px var(--glass-shadow);
  -webkit-backdrop-filter: blur(var(--glass-blur)) saturate(125%);
  backdrop-filter: blur(var(--glass-blur)) saturate(125%);
}

.glass-surface::before {
  position: absolute;
  inset: 0;
  z-index: -1;
  pointer-events: none;
  content: "";
  border-radius: inherit;
  background: linear-gradient(112deg,
    color-mix(in srgb, var(--glass-highlight) 26%, transparent),
    transparent 24% 72%,
    color-mix(in srgb, var(--glass-tint) 12%, transparent));
  opacity: .72;
}

.glass-surface > * { position: relative; z-index: 1; }
```

If the surface should look flatter, reduce fill and shadow before removing the edge light. The edge is usually the most efficient cue for thickness.

## Role modifiers

```css
.glass-surface--control {
  min-height: 44px;
  border-radius: 14px;
  background: color-mix(in srgb, var(--glass-fill) 88%, var(--glass-tint));
}

.glass-surface--selected {
  border-color: color-mix(in srgb, var(--glass-tint) 58%, var(--glass-highlight));
  box-shadow:
    inset 0 1px 0 var(--glass-highlight),
    inset 0 0 0 1px color-mix(in srgb, var(--glass-tint) 18%, transparent),
    0 12px 30px var(--glass-shadow);
}

.glass-surface--overlay {
  background: color-mix(in srgb, var(--glass-fill) 92%, var(--glass-tint));
  box-shadow: 0 24px 70px color-mix(in srgb, var(--glass-shadow) 130%, transparent);
}
```

Do not make every role selected. If multiple controls are selected, use one local tint and distinguish the active state with a small tonal lift, icon, underline, or label weight.

## Interaction and fallback

```css
.glass-surface:focus-visible,
.glass-surface[data-focus-visible="true"] {
  outline: 2px solid color-mix(in srgb, var(--glass-tint) 72%, var(--glass-highlight));
  outline-offset: 3px;
}

.glass-surface:active,
.glass-surface[data-pressed="true"] {
  transform: translateY(1px);
  box-shadow: inset 0 1px 0 color-mix(in srgb, var(--glass-highlight) 20%, transparent),
    0 8px 18px var(--glass-shadow);
}

@media (prefers-reduced-transparency: reduce) {
  .glass-surface {
    background: color-mix(in srgb, var(--glass-fill) 94%, var(--glass-tint));
    -webkit-backdrop-filter: none;
    backdrop-filter: none;
  }
}
```

When the page has a photo behind a panel, add a scrim or increase `--glass-fill` before increasing blur. More blur is not a substitute for contrast.

## Responsive rules

- Keep touch targets at least 44px high.
- On narrow screens, reduce blur and shadow before shrinking text or controls.
- Prefer one glass plane for a mobile toolbar instead of multiple overlapping capsules.
- Let images keep their aspect ratio; use `object-fit: cover` only when cropping is intentional.
- When a card's content column becomes too narrow, stack the supporting meaning below the main copy rather than accepting one-character wrapping.
