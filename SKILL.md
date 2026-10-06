---
name: word-contrast-card
description: Analyze 2–10 similar or easily confused English words, extract concise semantic contrasts, split them into 2–3-word visual card groups, build consistent 3:4 hand-drawn vocabulary cards, generate the images, and correct small text errors with at most one image edit before falling back to regeneration.
---

# Word Contrast Card

Create a consistent visual learning-card series from 2–10 English words.

## Input

Accept 2–10 English words. Preserve the user's order unless regrouping is clearly needed for semantic clarity.

Optional modes:
- `full` (default): show semantic analysis, grouping, image prompts, and images.
- `compact`: show only the core contrast and images.

Honor explicit user overrides for language, aspect ratio, style, or layout. Otherwise use this skill's defaults.

## Workflow

### 1. Analyze all words together

Read `assets/semantic-template.md`.

Analyze the complete word set in one shared semantic context **before** splitting it into cards.

Do not analyze future card groups independently.

For common words, rely on established usage. If a distinction is genuinely uncertain, niche, regional, or technical, verify it with a reliable dictionary or corpus source when such a tool is available.

Do not force words to be exact synonyms. If they are only related or commonly confused, state the real relationship and extract the most useful contrast.

### 2. Build the semantic map

For every word, produce:
- common Chinese meaning
- core focus
- one-sentence distinction
- best visual scene
- visual keywords
- the situation that most naturally evokes the word

End with one short contrast label per word, 2–6 Chinese characters according to the natural meaning. Do not pad a clear 2- or 3-character label to four characters.

The labels must be mutually differentiating, not paraphrases of one another.

### 3. Plan the cards

Each image contains **2 or 3 words only**.

Grouping rule:
- use groups of 3 where possible;
- if the final remainder would be 1, rebalance the last 4 words as `2 + 2`;
- never create a one-word card.

This yields:
- 2 → `2`
- 3 → `3`
- 4 → `2 + 2`
- 5 → `3 + 2`
- 6 → `3 + 3`
- 7 → `3 + 2 + 2`
- 8 → `3 + 3 + 2`
- 9 → `3 + 3 + 3`
- 10 → `3 + 3 + 2 + 2`

### 4. Reduce each word to a minimal visual scene

Before prompting the image model, compress each word to:

- `核心语义` — the short contrast label
- `核心场景` — one concrete visible action, relation, process, position, direction, or structural difference
- `视觉重点` — what the learner should remember from the scene

Keep each scene minimal:
- 1 core action or relationship
- 1–3 main objects
- only necessary arrows
- sparse black line art and large, simple shapes
- no illustrated background, texture, decoration, secondary example, or realistic shading

Keep an element only when it directly explains that word's semantic difference. Prefer a simple visible action or relationship when it helps; otherwise use the simplest structural contrast.

### 5. Lock the text before image generation

For each card, create a **Text Lock List** containing every string that must appear accurately in the image:

- English headwords
- Chinese core glosses
- `重点是：{2–6字核心短语}` labels
- 1–2 collocations per word

Choose collocations that naturally describe the selected visual scene. If they do not fit, adjust the scene or collocations before locking the text.

These strings are authoritative. Every readable string planned for the card, including any label inside an illustration, must be in the Text Lock List. Prefer text-free illustrations; do not allow the image model to invent extra readable text.

The image-generation step must copy them exactly and must not paraphrase, translate, shorten, expand, or invent replacements.

Keep text minimal. If a card feels crowded, remove nonessential collocations before shrinking text or adding more explanations.

### 6. Build one image prompt per card

Read `assets/image-template.md`.

For each card, inject:
- the 2–3 words on that card
- only their relevant semantic analysis
- their minimal visual scenes
- the Text Lock List

Do not include semantic analysis for words not on that card.

Keep the static visual instructions unchanged across all cards in the same request.

### 7. Generate the images

Use the available image-generation tool.

Default:
- 3:4 portrait
- one image per card
- same visual language across the series

For multi-card requests, keep:
- same background
- same hand-drawn line weight
- same typography feel
- same spacing and margins
- same thin, complete, rounded border around each word section
- same clean editorial grid, marker-swatch word headings, and restrained color treatment
- same information density
- same pastel saturation
- same slot colors:
  - first word = pale blue
  - second word = pale green
  - third word = pale orange

Each word section has its own visible border in its slot color. Keep all four rounded corners inside the canvas, with white space between adjacent borders. A single outline around the whole image or a divider line does not replace the section borders.

Follow the `Color system` in `assets/image-template.md` as visual-generation guidance. Within each word section, use one accent color: the exact same category color for its border, the organic marker swatch behind the headword, and the highlight behind the core semantic phrase. Do not introduce a separate coral or other highlight color. Keep explanatory illustrations as simple near-black line art without additional object colors. Set English headwords in bold lowercase handwritten lettering, Chinese body text in clearly readable handwriting, and English collocations in lighter handwritten lettering.

Keep every visible text line horizontal and front-facing, with its baseline parallel to the card's top and bottom edges. This includes headwords, Chinese glosses, `重点是` labels, collocations, and any necessary illustration labels. Marker swatches may have irregular edges, but the text on them stays level. Do not rotate, curve, arc, skew, or place text in perspective; wrap long text onto additional horizontal lines instead.

If the image tool supports using an earlier generated image as a style reference, use the first successful card as the style reference for later cards without changing their content.

### 8. Text fidelity and visual QC

Inspect each generated card against its Text Lock List.

Check:
- English headwords are spelled correctly
- Chinese glosses and `重点是` labels contain no obvious typo
- collocations are correct
- every readable string, including text inside illustrations or objects, appears in the Text Lock List; there is no extra text
- each collocation matches the action or object shown in its word's scene
- the number of sections matches the number of words
- every section has a complete, visible rounded border in the correct slot color, with no clipped corners
- every section uses the same exact category color for its border, headword swatch, and core-phrase highlight, with no second accent color
- Do not perform numerical color checks.
- Only treat color as a problem when the palette is obviously vivid, neon-like, candy-like, washed out, or inconsistent with the established muted-pastel series style.
- the category-color highlight marks only the core semantic phrase; illustrations remain simple black line art and text hierarchy is readable
- every text line is level and front-facing, including text on marker swatches and any illustration labels
- each word has exactly one distinct minimal scene with 1–3 main objects, sparse line art, and no unrelated visual detail
- scenes are relevant and nonduplicative, with no illustrated background, texture, decoration, secondary example, or realistic shading
- the card is not cluttered
- style and aspect ratio are correct

#### Correction policy

If the image is otherwise good and there are only **1–2 small, localized text errors** (including unwanted extra readable text):
1. If image editing is available, attempt **one** image edit.
2. Instruct the edit to change only the incorrect text and preserve layout, illustration, colors, spacing, and all other text.
3. Recheck the edited image.

If any of the following applies, regenerate the whole card instead:
- more than 2 text errors
- errors appear in multiple regions
- layout or illustration is also wrong
- a collocation and its scene do not match
- image editing is unavailable
- the single edit attempt fails
- the edited image introduces new errors

Do **not** enter repeated edit loops. Maximum image-edit attempts per card: **1**.

After the initial generation, allow at most **2 full-card regeneration attempts per card**, regardless of whether an image edit was tried. If the card still fails QC, stop retrying it. Report the remaining defects and mark any last image as a nonfinal draft; never present a failed card as complete.

### 9. Output

#### `full` mode
1. `语义设定`
2. `分图方案`
3. For each card:
   - `文字锁定清单`
   - `图片提示词`
   - generated image

#### `compact` mode
1. `核心对比`
2. generated images

Do not expose private chain-of-thought. Show only the structured semantic result, grouping, final prompt material, and generated images.
