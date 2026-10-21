# One Trip Lang - Assets and Presentation

The graybox uses primitives; production should reuse existing assets instead of commissioning a full art pipeline.

## Minimum inventory

- One trolley visual assembled from a licensed model or primitive frame; keep the physics deck/shape simple and independent.
- Six recognizable groceries: egg carton, milk, rice bag, fruit, cake box and cans. Reuse materials and geometry; readable silhouettes matter more than detail.
- One road, house/finish, curb, bump and sparse environment props.
- Short go, spill, finish and UI sounds, with mute. No soundtrack required.
- Text labels and two persistent player colors, also identified as P1/P2 so color is not the only cue.

## Verified source shortlist (October 21, 2026)

| Need | Source and choice | Status / fallback |
| --- | --- | --- |
| Food silhouettes | [Kenney Food Kit](https://kenney.nl/assets/food-kit), pack page lists CC0 | Shortlisted, not downloaded. Inspect actual contents for eggs/milk/fruit/cake/cans; missing rice or carton uses a labeled primitive package. |
| House/finish props | [Kenney City Kit Suburban](https://kenney.nl/assets/city-kit-suburban), pack page lists CC0 | Shortlisted. Use one house and a few props; primitive course/gates remain valid. |
| Impact/spill cues | [Kenney Impact Sounds](https://kenney.nl/assets/impact-sounds), pack page lists CC0 | Shortlisted. Select short cues and normalize volume; synthesize start/finish tones if needed. |
| Trolley and packages | Existing original code primitives | Keep as baseline. A purchased trolley model is optional only if import saves time; no custom modeling dependency. |
| UI/fonts | HTML/CSS with system sans-serif | No font service, paid UI kit or download required. |

These are pack-level verified sources, not a claim that every required model exists or has been imported. Issue #45 owns per-file selection/license/checksum records; #56 owns game integration and readability. Do not add asset purchases to the critical path. An optional USD 0-30 one-time art allowance is an estimate, not a purchase.

## Acquisition workflow

1. Shortlist free low-poly packs from an established library such as Kenney or Quaternius. Verify each pack's actual license; do not infer rights from a search result or the word free.
2. Record title, author, original URL, license text/version, downloaded file checksum, modifications and required attribution.
3. Convert/optimize only as necessary; use glTF/GLB for scene assets. Keep simple box/capsule collision proxies. Record source files and export settings.
4. Bundle models, textures, fonts and audio with the build; test offline startup on a clean browser profile.
5. Add credits both in the repository and accessible from the game. Reject unknown-license assets.

AI-generated signs/textures are optional. Record tool/model, date, source inputs and applicable usage terms; generation does not replace license review of input material. No new API purchase is needed. No hand-modeled avatar, rig, animation set, realistic vehicle or detailed grocery aisle is required.

## Readability priorities

Make the course direction, upcoming corner, remaining points, lost item and time left legible during play. Keep both colliding trolleys readable, with stable player IDs and restrained impact cues. Avoid camera shake that hides steering or produces motion discomfort. Use a follow camera with restrained smoothing; never tie authoritative movement to camera interpolation. Tutorial text should fit on one compact pre-race panel.
