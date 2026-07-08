# Prompt Optimization Framework

Use this file when applying `image-prompt-director` to any image-generation request.

## Language Rule

Always write the final generation prompt, negative prompt, and model parameters in English, no matter what language the user used. Preserve non-English only when it is exact visible text that must appear inside the image. Examples:

- User asks in Chinese for a cyberpunk cat poster -> final prompt is English.
- User asks for a poster with the title "未来已来" -> final prompt is English, but the visible title remains `"未来已来"`.
- User asks for a Japanese magazine cover with the headline "春の記憶" -> final prompt is English, but that headline remains Japanese.

Do not translate required on-image text unless explicitly requested.

## Two-Pass Pipeline

### Pass 1: Director Expansion

Extract:

- user intent: generate image, optimize prompt, create variants, adapt to a model, or prepare a prompt pack
- image type: portrait, cover, poster, product, illustration, logo, UI, architecture, food, landscape, game asset, infographic, etc.
- subject: who or what is visible, identity constraints, count, age category if human, pose/action
- output use: social cover, article hero, ad, editorial, concept art, asset sheet, print, app UI, icon
- style target: photographic, cinematic, editorial, anime, 3D, vector, oil painting, documentary, luxury, brutalist, minimal, etc.
- scene logic: location, time, weather, background density, props, spatial relationship
- composition: aspect ratio, crop, camera distance, angle, focal point, text-safe area
- lighting: key light, fill, rim, contrast, color temperature, shadow quality
- materials: skin, hair, fabric, metal, plastic, glass, paper, food, stone, smoke, water
- color: palette, contrast, saturation, temperature pairing
- typography: only when image includes visible text or graphic layout
- visible text language: preserve exact strings and language only for text that appears in the image
- technical: target model, aspect ratio, size, seed, reference image handling
- hard negatives: must-not-show items, anatomy risks, text risks, style drift risks

Convert vague input into a visual production brief. Preserve the user's core idea; do not overwrite it with unrelated spectacle.

### Pass 2: Auditor Repair

Check the draft prompt with this audit:

- Subject: Is the main subject specific and visually inspectable?
- Relevance: Does every major visual choice serve the user's intent?
- Focus: Is there one dominant focal point?
- Composition: Are crop, placement, depth, and aspect ratio clear?
- Lighting: Is the light physically plausible and style-appropriate?
- Materials: Are texture, surface behavior, and realism cues specified?
- Background: Is it rich enough but controlled?
- Style: Are style anchors coherent rather than contradictory?
- Text: If text appears, are exact words, font style, placement, and legibility specified?
- Model risks: Are hands, faces, text, logos, transparent edges, repeating patterns, or tiny details protected?
- Negatives: Are common failure modes constrained without overloading the model?
- Parameters: Are aspect ratio and model settings compatible with the requested use?

Repair all missing or weak areas before final output.

## Prompt Density Levels

Choose density from the task:

- Minimal: icons, simple objects, logo concepts, clean assets. Use fewer details and strong shape/color constraints.
- Medium: product shots, portraits, covers, UI mockups. Use complete light/composition/material directions.
- High: cinematic scenes, concept art, editorial posters, fantasy/scifi worlds. Use environment story, atmosphere, lens, layered composition, and controlled details.

Do not make every prompt maximal. Too much detail can dilute simple tasks.

## High-Impact Prompt Anchors

Prefer these anchors because image models respond strongly to them:

- medium: editorial photograph, commercial product photography, cinematic still, magazine cover, concept art, vector mark, 3D render
- lens: 35mm environmental, 50mm natural perspective, 85mm portrait, 100mm macro, tilt-shift, orthographic
- light: softbox key light, window light, rim light, volumetric backlight, overcast diffuse light, hard noon sun, neon practicals
- composition: rule of thirds, central symmetry, low-angle hero shot, top-down flat lay, negative space for title, close crop, wide establishing shot
- material: brushed metal, frosted glass, matte ceramic, satin fabric, leather grain, paper fiber, condensation, micro-scratches
- post: film grain, HDR but natural, restrained color grade, print editorial contrast, shallow depth of field

## Conflict Cleanup

Remove or resolve contradictions:

- "minimalist but extremely detailed background" -> minimalist subject with one controlled background detail
- "soft low contrast and high contrast harsh noir" -> choose one or split subject/background contrast
- "photorealistic vector logo" -> choose photorealistic emblem render or flat vector logo
- "wide full-body close-up" -> choose full-body medium-wide or close-up portrait
- "no text but magazine cover typography" -> decide whether typography is included

## Text-In-Image Handling

Text is fragile in most image models. If text must appear:

- quote the exact text
- specify language, casing, line breaks, and hierarchy
- reserve enough blank space
- request clean vector-like lettering or editorial typography
- avoid more than 1-3 text blocks unless using a text-strong model

For production covers, prefer generating a clean image base and adding final typography in design software unless the user explicitly wants rendered text.
