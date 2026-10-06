# Changelog

All notable changes to this skill are documented here.

## [Unreleased]

### Added
- Replace the partial condiment/seasoning sample with a complete example, including a generated card and visual QC notes.

### Changed
- Replace the placeholder README with an overview, usage guidance, repository map, and license status.

## [3.3.0] - 2026-10-04

### Changed
- Limit each card to two full-card regeneration attempts after its initial generation, then stop and report remaining defects.
- Require every readable string to be in the Text Lock List and reject extra illustration text during QC.
- Require English collocations to match their visual scenes during planning and QC.

## [3.2.0] - 2026-10-04

### Changed
- Use one category accent color per word section: its border, headword swatch, and core-phrase highlight now match exactly.
- Remove the separate coral semantic highlight from generation guidance and visual QC.

## [3.1.0] - 2026-10-04

### Changed
- Require one sparse, minimal explanatory scene per word with 1–3 main objects and only directly relevant elements.
- Exclude illustrated backgrounds, textures, decoration, secondary examples, and realistic shading from scene prompts and QC.

## [3.0.0] - 2026-10-04

### Changed
- Define a warm-white, near-black, muted-pastel color system with HSL limits for category accents, large fills, and coral semantic highlights.
- Provide muted hex references and check representative raster colors when pixel inspection is available.
- Clarify that marker-like swatches describe brush shape, never fluorescent color.
- Allow natural 2–6-character Chinese core phrases without padding them to four characters.

## [2.2.0] - 2026-10-04

### Changed
- Require every visible text line to remain horizontal and front-facing, including headwords on organic marker swatches, Chinese explanations, and English collocations.
- Check text orientation during visual QC; wrap long copy onto horizontal lines instead of rotating it.

## [2.1.0] - 2026-10-04

### Changed
- Use a clean editorial grid, bold lowercase handwritten headwords on organic marker swatches, readable Chinese handwriting, and lighter English collocation labels.
- Limit each word section to its slot pastel for category coding and coral for selective semantic emphasis; keep illustrations in black line art.
- Check the marker swatch, color limit, emphasis placement, and text hierarchy during visual QC.

## [2.0.0] - 2026-10-04

### Changed
- Require a separate, complete rounded border around every word section, colored by slot, with consistent padding and visible gaps.
- Check section borders during visual QC; divider lines and a single page outline no longer satisfy the layout contract.

## [1.1.0] - 2026-10-03

### Added
- Text Lock List before image generation.
- Post-generation text fidelity check.
- One-attempt image-edit correction path for 1–2 localized text errors.
- Automatic fallback to full-card regeneration when editing is unavailable, fails, or is not appropriate.
- Explicit ban on repeated image-edit loops.

### Changed
- Image prompt now treats locked text as authoritative and non-paraphrasable.
- `full` mode now exposes the Text Lock List for each card.
- QC logic now distinguishes small text errors from broader image failures.

## [1.0.0] - 2026-10-03

### Added
- Unified semantic analysis for 2–10 words before card splitting.
- Deterministic 2–3-word grouping with no one-word cards.
- Minimal visual-scene compression step.
- Stable 3:4 hand-drawn visual card template.
- Multi-card style consistency rules.
- Image-generation step and lightweight post-generation QC.
- `full` and `compact` output modes.
