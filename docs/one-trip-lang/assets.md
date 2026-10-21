# One Trip Lang - Assets and Presentation

The graybox uses primitives; production should reuse existing assets instead of commissioning a full art pipeline.

## Minimum inventory

- One trolley visual assembled from a licensed model or primitive frame; keep the physics deck/shape simple and independent.
- Six recognizable groceries: egg carton, milk, rice bag, fruit, cake box and cans. Reuse materials and geometry; readable silhouettes matter more than detail.
- One road, house/finish, curb, bump and sparse environment props.
- Short go, spill, finish and UI sounds, with mute. No soundtrack required.
- Text labels and two persistent player colors, also identified as P1/P2 so color is not the only cue.

## Acquisition workflow

1. Shortlist free low-poly packs from an established library such as Kenney or Quaternius. Verify each pack's actual license; do not infer rights from a search result or the word free.
2. Record title, author, original URL, license text/version, downloaded file checksum, modifications and required attribution.
3. Convert/optimize only as necessary; use glTF/GLB for scene assets. Keep simple box/capsule collision proxies. Record source files and export settings.
4. Bundle models, textures, fonts and audio with the build; test offline startup on a clean browser profile.
5. Add credits both in the repository and accessible from the game. Reject unknown-license assets.

AI-generated signs/textures are optional. Record tool/model, date, source inputs and applicable usage terms; generation does not replace license review of input material. No new API purchase is needed. No hand-modeled avatar, rig, animation set, realistic vehicle or detailed grocery aisle is required.

## Readability priorities

Make the course direction, upcoming corner, remaining points, lost item and time left legible during play. Keep the local trolley opaque and rivals visually quieter when they overlap. Use a follow camera with restrained smoothing; never tie authoritative movement to camera interpolation. Tutorial text should fit on one compact pre-race panel.
