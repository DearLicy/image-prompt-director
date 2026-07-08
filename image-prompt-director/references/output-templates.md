# Output Templates

Use these templates for final answers. The generation prompt, negative prompt, and parameters must be English regardless of the user's input language. The only exception is exact visible text that must appear inside the generated image; keep that string in its requested language inside quotes.

## When User Wants A Prompt Only

Use this answer shape:

```text
Final image prompt:
[structured prompt or target-model prompt in English]

Negative prompt:
[targeted avoid list in English]

Suggested parameters:
[aspect ratio, size, style strength, steps/CFG/seed if relevant]

Second-pass audit:
[1-4 short notes about what was strengthened or repaired]
```

## Universal Structured Prompt

```json
{
  "description": "Define the image type, subject, use case, and overall visual direction in one precise sentence.",
  "style": {
    "visual_style": "medium + aesthetic direction + quality target",
    "features": ["visible style evidence", "composition or material traits"]
  },
  "subject": {
    "main_subject": "the primary visible subject",
    "action_or_pose": ["specific posture, motion, or behavior"],
    "details": ["identity constraints, shape, expression, props, design details"]
  },
  "environment": {
    "setting": "where the image takes place",
    "background_design": ["background density", "spatial layers", "prop logic"]
  },
  "composition": {
    "layout": ["aspect/crop", "camera distance", "subject placement", "negative space or crop safety"]
  },
  "lighting": {
    "light_setup": ["key light", "fill light", "rim light", "shadow quality"],
    "color_temperature": ["warm/cool relationship", "highlight behavior"]
  },
  "camera": {
    "shot": ["focal length", "aperture/depth of field", "angle", "focus target"]
  },
  "materials": {
    "texture": ["skin, fabric, metal, glass, paper, food, stone, water, smoke, or other relevant surfaces"]
  },
  "typography": {
    "text": "keep only when visible text is required",
    "hierarchy": ["title", "subtitle", "small labels"],
    "requirements": ["clean spelling", "legible layout", "no extra text"]
  },
  "rendering": {
    "finish": ["photorealistic / illustration / 3D / vector", "post-processing style"]
  },
  "mood": {
    "atmosphere": ["emotion", "visible evidence that creates the emotion"]
  },
  "negative": {
    "avoid": ["common failure modes", "type-specific failure modes"]
  },
  "aspect_ratio": "...",
  "model_parameters": {
    "size": "...",
    "style_strength": "...",
    "seed": "optional"
  }
}
```

## Midjourney Final Format

```text
[subject], [medium/style], [environment], [composition], [lighting], [materials], [color palette], [mood], [rendering finish], clean focal hierarchy, premium production design, no cheap template look --ar [ratio] --style raw --stylize [value]
```

## SDXL / Flux Final Format

```text
Positive prompt:
[model-ready positive prompt in English]

Negative prompt:
[focused negative prompt in English]

Parameters:
size: [width]x[height]
steps: [number]
CFG/guidance: [number]
sampler/scheduler: [if relevant]
seed: [optional]
```

## OpenAI Image Final Format

```text
Create a [ratio/use-case] image of [subject]. The image should show [specific visible details]. Use [composition]. Lighting: [specific light]. Materials and textures: [specific surfaces]. Mood: [emotion with visible evidence]. Text requirements: [exact text or "no text"]. Avoid [failure modes].
```

## If Also Generating The Image

Before invoking the image tool, silently finish the audit. Then use only the final model-ready English prompt and relevant parameters for generation. In the response, include the generated image and the final prompt used.
