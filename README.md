# Adaptive Liquid Glass UI

> A color-aware, Apple-inspired Liquid Glass Skill for Codex.

This repository contains one focused Skill for designing restrained, adaptive glass interfaces. It helps a glass surface respond to its host instead of forcing every screen into the same blue-gray overlay.

## What it does

- Derives tint, fill, edge highlight, shadow, blur, and text contrast from the current color context.
- Adapts across dark, light, warm, cool, saturated, monochrome, and image-based backgrounds.
- Separates canvas, cards, controls, navigation, overlays, and selected states into a material hierarchy.
- Covers responsive layout, keyboard focus, pressed states, reduced transparency, and no-backdrop-filter fallbacks.
- Guards against over-blur, bright full borders, unreadable translucent text, fake refraction, and repetitive glass cards.

## Use with Codex

Copy `skills/adaptive-liquid-glass-ui` into your Codex skills directory, then invoke it with:

```text
Use $adaptive-liquid-glass-ui to refine this interface for a warm image background while keeping the glass restrained and the content readable.
```

It is useful for glass buttons, cards, toolbars, tabs, popovers, modals, and reusable CSS token systems that need to work across multiple brand colors.

## Package structure

```text
skills/
鈹斺攢鈹€ adaptive-liquid-glass-ui/
    鈹溾攢鈹€ SKILL.md
    鈹溾攢鈹€ agents/openai.yaml
    鈹斺攢鈹€ references/adaptive-liquid-glass.md
```

The Skill is intentionally self-contained: no application code, screenshots, product assets, or unrelated project files are included.

## Design principles

1. Read the host background before choosing the glass tint.
2. Use translucency to establish hierarchy, not to decorate every surface.
3. Keep text and controls crisp above the glass treatment.
4. Let edge highlights, depth, and blur stay quiet until the context needs emphasis.
5. Provide an accessible opaque fallback whenever transparency is unavailable or reduced.

## Validation

Run the official Codex Skill validator against the package directory:

```text
python quick_validate.py skills/adaptive-liquid-glass-ui
```
