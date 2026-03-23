# Katagami Prompt — Illustration Generation

> Universal template for generating consistent illustrations for any design system.
> Pick a style preset, plug in your brand colors, generate a batch.

---

## How To Use

1. Pick a **Style Preset** from the table below (or define your own)
2. Copy the **Master Template**
3. Replace `[PLACEHOLDERS]` with your specifics
4. Generate with Midjourney, DALL-E, Recraft, or any image AI
5. Review batch for consistency → re-generate outliers → vectorize

**Recommended tool:** Recraft V3 produces the cleanest vector-ready output. Midjourney is better for mood/concept exploration but often needs post-processing.

**Recommended workflow:** Use **Antigravity** (Google AI IDE) or Claude Projects for design concept exploration and illustration generation. Long-context conversational AI holds visual direction better across a session than coding-focused tools.

---

## Style Presets

Pick the one closest to your brand, then customize:

| Preset | Style Anchor | Best For | Character Style |
|--------|-------------|----------|-----------------|
| **Corporate Flat** | "Katerina Limpitsouni (unDraw)" | B2B SaaS, enterprise, dashboards | Elongated, minimal faces, no outlines |
| **Friendly Outline** | "Pablo Stanley (Open Peeps)" | Consumer apps, social, community | Hand-drawn feel, expressive faces, outline strokes |
| **Minimal Abstract** | "Streamline illustrations" | Fintech, productivity, developer tools | Geometric shapes, thin lines, no characters |
| **Isometric Tech** | "Isometric illustration style, clean vectors" | Infrastructure, DevOps, architecture | 3D-angled objects, no characters or tiny figures |
| **Organic Soft** | "Blush illustrations by Pablo Stanley" | Health, wellness, education | Rounded shapes, warm colors, soft faces |
| **Bold Geometric** | "Bauhaus poster style, flat geometric shapes" | Marketing, creative agencies, portfolios | Abstract human forms, strong shapes, high contrast |

---

## Master Template

```
[SCENE DESCRIPTION]: A [character/object] [doing action] in [environment/context].
[OBJECTS]: Include [specific items relevant to the scene].

STYLE: [YOUR STYLE DESCRIPTION — use a Style Anchor from presets above, or describe your own].
[LIST 4-6 STYLE RULES — what defines the visual language]

Example style rules for Corporate Flat:
- Zero outlines, zero shading, zero gradients
- Solid flat color fills exclusively
- Clean geometric shapes for all objects
- Minimal environmental detail (1-2 background elements max)
- White or transparent background

CHARACTER PROPORTIONS (include ONLY if scene has human figures):
[DESCRIBE YOUR CHARACTER STYLE — proportions, face detail level, limb style]

Example for Corporate Flat:
- Elongated thin body, legs = 50% of height
- Small head, thin limbs, dot-style hands
- Minimal facial features (dots for eyes, optional thin smile)
- Hair as simple geometric shapes

COLOR PALETTE (STRICT — use ONLY these colors):
- Primary: [YOUR BRAND HEX] (dominant, 40-50% of illustration)
- Accent: [YOUR ACCENT HEX] (tiny accents only, 2-3 small elements)
- Secondary: [YOUR SECONDARY HEX] (backgrounds, large surfaces)
- Tertiary: [YOUR TERTIARY HEX] (secondary objects)
- White: #FFFFFF (highlights, negative space)

NEGATIVE PROMPT: [LIST STYLES YOU DO NOT WANT]

Base negative prompt (works for most styles):
cute, kawaii, mascot, 3D render, gradient, drop shadow, clipart, stock photo,
realistic, photographic, watercolor texture

Add style-specific negatives:
- If you want flat: "outline stroke, thick borders, hand-drawn texture"
- If you want clean: "busy background, decorative elements, patterns"
- If you want professional: "chibi, anime, manga, pixar style, cartoon eyes"
- If you want minimal: "detailed faces, complex scenes, many characters"

--ar [YOUR ASPECT RATIO] --iw 0.25

Note: --ar and --iw are Midjourney-specific parameters.
For Recraft V3, set aspect ratio and style strength in the UI directly.
For other tools, adapt these settings to the tool's native controls.
```

---

## Style-Specific Examples

### Corporate Flat (unDraw-like)
```
STYLE: Flat vector illustration in the style of Katerina Limpitsouni (unDraw).
- Zero outlines, zero shading, zero gradients
- Solid flat color fills exclusively
- Clean geometric shapes, minimal environmental detail
- White or transparent background

CHARACTER PROPORTIONS:
- Elongated thin body, legs = 50% of height
- Dot-style hands, minimal facial features
- Hair as simple geometric shapes

NEGATIVE PROMPT: cute, kawaii, mascot, cartoon eyes, hand-drawn texture,
sketch lines, watercolor, 3D render, gradient, drop shadow, outline stroke,
thick borders, chibi proportions, anime, pixar style

--ar 4:3 --iw 0.25
```

### Friendly Outline (Open Peeps-like)
```
STYLE: Hand-drawn outline illustration in the style of Pablo Stanley (Open Peeps).
- Consistent black outline stroke (2-3px)
- Minimal flat color fills inside outlines
- Expressive but simple facial features
- White background, no environmental detail

CHARACTER PROPORTIONS:
- Natural body proportions (not elongated)
- Expressive eyes, simple smile
- Visible fingers (simplified, 4 fingers)
- Hair with flowing lines

NEGATIVE PROMPT: realistic, 3D render, gradient, photographic, detailed shading,
complex background, cute mascot, pixel art, isometric

--ar 1:1 --iw 0.25
```

### Minimal Abstract (Streamline-like)
```
STYLE: Minimal abstract vector illustration in the style of Streamline.
- Thin consistent lines (1-2px)
- Maximum 3-4 colors per illustration
- Geometric shapes, no organic forms
- No human characters (use abstract representations)
- Generous white space

NEGATIVE PROMPT: realistic, detailed, busy, complex, photographic,
hand-drawn, sketch, watercolor, 3D, characters, faces, cute

--ar 16:9 --iw 0.25
```

---

## Prompt Engineering Lessons

Learned through 50+ generation iterations:

| Version | Problem | Fix |
|---------|---------|-----|
| V1 | Generic output, AI ignores specifics | Added explicit object/scene descriptions |
| V2 | Characters looked like mascots | Removed personality traits, added anti-cute negatives |
| V3 | Reference images overrode text style | Dropped `--iw` from 0.5 to 0.25 |
| V4 | Colors drifted from brand palette | Hardcoded ALL hex values, removed color names |
| V5 | Inconsistency across batch | Locked style block, only changed scene description |

### Key Insights

1. **Text instructions > Image references.** Use `--iw 0.25` or lower. Higher image weight makes the model copy the reference instead of following your text.
2. **Name a specific artist or library.** "In the style of Katerina Limpitsouni" works better than "flat vector with elongated proportions." The model has learned specific styles from training data.
3. **Negative prompts are mandatory.** Every image AI defaults toward "friendly/cute." You must explicitly exclude unwanted aesthetics.
4. **Hex codes > color names.** "Navy blue" gives you 50 different navies. "#1E3A5F" gives you one.
5. **Conditional blocks save tokens.** Only include CHARACTER PROPORTIONS when the scene has people. Abstract scenes don't need body proportion rules.
6. **Lock the style block across a batch.** Only change `[SCENE DESCRIPTION]` and `[OBJECTS]` between generations. Everything else stays identical — this is how you get visual consistency.
7. **Recraft V3 > Midjourney for production vectors.** Midjourney produces beautiful raster art but needs vectorization. Recraft outputs cleaner SVG-ready results with fewer artifacts.

---

## Batch Generation Workflow

When generating a set of illustrations (10-20 for a product):

1. **Create a scene list** — one-line descriptions per illustration
2. **Lock your style block** — colors, proportions, negatives stay identical
3. **Generate all** with only scene/object changes
4. **Review for consistency** — compare side by side, flag outliers
5. **Re-generate outliers** with text corrections only (no new references)
6. **Vectorize** final outputs (Recraft native or AI SVG conversion)
7. **Name semantically** and place in `public/illustrations/`

### Example Scene List
```
1. team-collaboration.svg    — Three people around a table with laptops
2. data-analytics.svg        — Person standing next to large bar chart
3. personal-growth.svg       — Person climbing a staircase of blocks
4. survey-completion.svg     — Person with checkmark and clipboard
5. onboarding-welcome.svg    — Person waving next to open door
6. settings-config.svg       — Gears and toggles arrangement (no people)
7. empty-state.svg           — Open box with magnifying glass (no people)
8. error-state.svg           — Warning triangle with tools (no people)
```

---

## Color Palette Ratio Guide

Regardless of style, keep these ratios for visual harmony:

| Role | Coverage | Example |
|------|----------|---------|
| **Primary** | 40-50% | Brand's main color — dominates large shapes |
| **Accent** | 2-5% | Contrast pop — tiny elements, highlights |
| **Secondary** | 25-35% | Neutral — backgrounds, large non-focal areas |
| **Tertiary** | 10-15% | Neutral — secondary objects, shadows |
| **White/Negative** | 10-20% | Breathing room, clothing details |

**Rule:** If your accent color appears on more than 3 small elements, it stops being an accent and becomes visual noise. Keep it rare.
