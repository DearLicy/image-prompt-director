---
name: image-prompt-director
description: "Transform natural-language image ideas into production-ready image-generation prompts with a two-pass prompt optimization and audit workflow. Use when the user asks to generate an image, optimize/improve/expand an image prompt, create Midjourney/Stable Diffusion/SDXL/Flux/OpenAI image prompts, convert rough ideas into structured prompt packs, or requests 图片生成提示词, 生图提示词, 提示词优化, 文生图, 图生图, 海报, 人像, 产品图, 封面图, 插画, 概念图, UI mockup, logo, icon, or any visual generation brief."
---

# Image Prompt Director

## 中文介绍

这个 skill 用于把用户随口描述的图片想法，先经过对话模型重写成高质量英文生图提示词，再进行查漏补缺和模型适配，最后输出可直接投喂给图像生成模型的 prompt、negative prompt 和建议参数。

## Core Behavior

When this skill is used, act as an image-prompt director before any image-generation step.

Hard language rule: regardless of the user's input language, generate the final image prompt, negative prompt, and model parameters in English. Use non-English text only for exact visible text that must appear inside the generated image, such as a Chinese poster title, Japanese magazine headline, Arabic sign, or any user-specified on-image typography. Do not translate required on-image text unless the user asks.

Always run this pipeline:

1. Parse the user's natural-language request into intent, subject, image type, target use, visual style, constraints, aspect ratio, and target model if stated.
2. Expand the request into an English structured visual brief with clear sections. English is the default prompt language for image-generation models unless the user explicitly asks for another language.
3. Perform a second-pass audit for missing visual anchors, contradictions, weak generic wording, model-risk areas, and output-format gaps.
4. Produce the final model-ready prompt, negative prompt or avoid list, and parameter suggestions.
5. If the user asked to actually generate the image and an image-generation tool is available, feed the final prompt to that tool after optimization.

Ask at most one short clarification only when a missing choice would radically change the image and cannot be reasonably inferred. Otherwise choose a strong default and continue.

## Prompt Construction Rules

Use concrete visual language, not vague praise. Replace weak words like "premium", "beautiful", "realistic", or "cinematic" with visible causes:

- lighting: direction, softness, contrast, rim light, ambient fill, highlight behavior
- composition: crop, subject placement, depth, negative space, hierarchy, scale
- camera: lens, angle, distance, aperture, focus target, motion behavior
- material: fabric, skin, metal, glass, paper, food texture, surface wear, subsurface scattering
- environment: location logic, background density, atmosphere, set design, spatial order
- color: palette, saturation, value contrast, temperature relationship
- output use: cover, poster, product hero, social share, editorial spread, concept sheet, asset

Default final structure:

```text
{
  "description": "...",
  "style": {...},
  "subject": {...},
  "environment": {...},
  "composition": {...},
  "lighting": {...},
  "camera": {...},
  "materials": {...},
  "color": {...},
  "typography": {...},
  "rendering": {...},
  "mood": {...},
  "negative": {...},
  "aspect_ratio": "...",
  "model_parameters": {...}
}
```

Omit irrelevant sections. Add specialized sections when useful, such as `layout`, `brand`, `product`, `character`, `pose`, `skin_texture`, `hair`, `costume`, `environment_story`, `shot_list`, or `text_rendering`.

If the user writes in Chinese or any other language, keep any conversational explanation concise in the user's language when useful, but keep all prompt fields in English. Preserve exact non-English strings only inside fields like `typography.text`, `visible_text`, or quoted on-image copy.

## Reference Selection

Read only the reference files needed for the current request:

- For the required two-pass workflow and audit checklist, read [references/prompt-framework.md](references/prompt-framework.md).
- For type-specific prompt modules such as portrait, product, cover, logo, architecture, food, game asset, or infographic, read [references/domain-modules.md](references/domain-modules.md).
- For target-model adaptation and generation parameters, read [references/model-parameters.md](references/model-parameters.md).
- For final answer formats and reusable templates, read [references/output-templates.md](references/output-templates.md).

## Model Adapter Rule

If the target model is unknown, produce a universal structured prompt plus concise parameter suggestions. If a model is named, adapt:

- Midjourney: compress to a cinematic descriptive prompt with `--ar` and style parameters.
- Stable Diffusion/SDXL/Flux: output positive prompt, negative prompt, size, steps, CFG/guidance, sampler or scheduler when applicable.
- OpenAI image models: use natural-language instructions with explicit spatial, text, and editing requirements.
- Ideogram or text-heavy models: strengthen exact text, typography, layout, and hierarchy.

## Quality Bar

Before finalizing, ensure the prompt contains:

- one dominant subject or visual concept
- a clear image type and output use
- composition and aspect ratio
- light direction and contrast logic
- material or surface detail
- background density control
- mood with visible evidence
- rendering or medium instructions
- negative constraints for common failure modes
- no unresolved placeholders unless the user intentionally provided variables

Never leave the user with only a generic prompt. The output must be ready for image generation.
