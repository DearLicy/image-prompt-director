# Model Parameters And Adapters

Use this file when the user names a target model or asks for generation parameters.

## Universal Defaults

If the user gives no settings:

- aspect ratio: infer from use case
  - portrait, magazine, character: 2:3 or 3:4
  - article cover, hero banner, landscape poster: 3:2, 16:9, or 21:9
  - social square, icon, product catalog: 1:1
  - phone UI: 9:16
- seed: optional; suggest fixed seed only when reproducibility matters
- quality: high, but avoid empty quality spam
- style strength: medium unless the user wants strict realism or a strong art style
- variants: create 2-4 only when the user asks for options

## OpenAI / GPT Image Adapter

Use natural-language instructions with explicit constraints:

- describe the final image, not a tag list
- specify exact text if text is required
- specify "do not add extra text" when no text is desired
- for edits, describe what must stay unchanged and what changes
- for transparent assets, request clean alpha edges and centered composition
- include aspect ratio or size if the tool supports it

Good format:

```text
Create a [format] image of [subject] in [environment]. Use [composition], [lighting], [materials], and [mood]. Include exact text "[text]" at [location] in [font style]. Avoid [failure modes].
```

## Midjourney Adapter

Prefer one concise descriptive paragraph plus parameters. Avoid long JSON.

Useful parameters:

- `--ar 2:3`, `--ar 3:2`, `--ar 16:9`, `--ar 1:1`
- `--style raw` for controllability and less default beautification
- `--stylize 50-250` for moderate stylization; higher for decorative art
- `--chaos 0-20` for stable output; higher for exploration
- `--seed <number>` for repeatability
- `--q 1` normally; higher only when supported and useful

Template:

```text
[subject], [style/medium], [environment], [composition], [lighting], [materials], [color palette], [mood], [rendering finish], [negative phrasing if supported] --ar [ratio] --style raw --stylize [value]
```

## Stable Diffusion / SDXL Adapter

Output:

- positive prompt: comma-separated or sentence/tag hybrid
- negative prompt: anatomy/text/artifact failures
- size: compatible with ratio, often 1024 on the long side for SDXL
- steps: 25-40
- CFG: 4.5-7.5 for SDXL; reduce if output looks overcooked
- sampler: DPM++ 2M Karras or the user's local default
- hires fix: use for photoreal portraits/product detail when needed
- LoRA/controlnet/reference: mention only if the user provides or asks

Keep negative prompts targeted. Overloaded negatives can reduce style quality.

## Flux Adapter

Use natural language more than tag soup.

Defaults:

- steps: 20-35
- guidance: low to medium depending on implementation
- size: infer from target ratio
- prompt: detailed but readable sentences
- negatives: use UI-supported negative field if available; otherwise include "avoid..." naturally

Flux responds well to coherent photographic direction, material specificity, and exact composition.

## Ideogram / Text-Heavy Adapter

Use when the user cares about rendered text, poster typography, logo text, or quote graphics.

Strengthen:

- exact words in quotes
- line breaks
- typography hierarchy
- text placement
- contrast and empty space
- "no extra letters or misspellings"

Keep text blocks short.

## Negative Prompt Building

Choose from these only when relevant:

- anatomy: malformed hands, extra fingers, broken wrists, distorted face, asymmetrical eyes
- text: illegible text, misspelled words, repeated letters, random captions, watermark
- image quality: low resolution, blurry, oversharpened, noisy, compression artifacts
- style: cheap template, plastic skin, waxy face, overprocessed HDR, excessive glow
- composition: cropped subject, cluttered background, tilted horizon, unclear focal point
- material: melted fabric, warped packaging, distorted logo, fake reflections

Do not include negatives that contradict desired stylization.
