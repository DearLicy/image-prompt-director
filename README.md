# Image Prompt Director

Image Prompt Director is a Codex skill that turns rough natural-language image ideas into production-ready image-generation prompts.

It runs a two-pass workflow:

1. Expand the user's idea into a structured visual production brief.
2. Audit and repair missing visual anchors, contradictions, weak wording, model-risk areas, and parameter gaps.

The final prompt, negative prompt, and model parameters are always generated in English, regardless of the user's input language. Non-English is preserved only when it is exact visible text that must appear inside the generated image.

## What It Optimizes

- subject and focal concept
- composition and aspect ratio
- lighting direction and contrast
- camera language
- material and texture detail
- environment density
- color palette
- typography and visible text handling
- negative prompt constraints
- model-specific parameters

## Supported Image Types

- editorial posters and article covers
- magazine covers
- portraits, fashion, cosplay
- commercial product images
- architecture and interiors
- food and beverage
- landscape and travel
- anime, illustration, concept art
- game assets and icons
- logos and brand marks
- infographics and diagrams
- UI mockups and app screens

## Supported Model Adapters

- OpenAI / GPT Image
- Midjourney
- Stable Diffusion / SDXL
- Flux
- Ideogram and text-heavy image models

## Installation

Copy the skill folder into your Codex skills directory:

```powershell
Copy-Item -Recurse .\image-prompt-director "$env:USERPROFILE\.codex\skills\image-prompt-director"
```

Then use it in Codex:

```text
Use $image-prompt-director to optimize this image idea: a futuristic Chinese teahouse poster, cyberpunk but restrained and premium
```

## Repository Structure

```text
image-prompt-director/
  SKILL.md
  agents/
    openai.yaml
  references/
    prompt-framework.md
    domain-modules.md
    model-parameters.md
    output-templates.md
```

## License

MIT
