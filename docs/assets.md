# Asset plan and inventory

## Visual direction

One coherent low-poly sala with an unobstructed central floor, four colored throwing stations and a large readable cockroach silhouette. Lighting suggests 2 a.m. without obscuring the target. Filipino context comes from a small number of props and wall details, not an entire modeled house.

No full player avatars, rigged characters or walking animations. Show names, station colors and slippers. Cockroach motion can use simple transform animation; a complex skeleton is unnecessary. Aim and Court overlays are ordinary UI and simple scene geometry.

## Sourcing order

1. Search a single CC0 pack for furniture and props, starting with Kenney. Its asset pages are CC0; verify the included license of each downloaded pack.
2. Find a recognizable slipper and cockroach from compatible licensed libraries. These are procurement targets, not assets we have already found.
3. Use generated 2D posters/textures only where they improve the scene. Do not let generated 3D become a dependency until import, silhouette and performance pass.
4. If the two hero models cannot be sourced, consider licensed alternatives or a generated asset only after verifying event rules and usage rights. Escalate before abandoning the no-hand-modeling policy.

## Inventory

| ID | Need | Candidate source | Format | Status |
|---|---|---|---|---|
| A01 | Floor, walls, sofa, table, simple props | Kenney or another compatible CC0 pack | GLB/glTF | Not selected |
| A02 | Slipper with visible flat/edge orientation | Licensed free model library | GLB/glTF | Not selected; early gate |
| A03 | Readable cockroach silhouette | Licensed free model library | GLB/glTF | Not selected; early gate |
| A04 | Wall art and room details | Licensed assets or generated 2D | PNG/WebP | Optional |
| A05 | Impact, skitter, hit and reveal sounds | CC0 audio library | OGG/WAV | Not selected |
| A06 | Icons and UI symbols | One permissive icon set | SVG | Not selected |
| A07 | Court evidence/replay overlay | Code-built UI and lines | Runtime | Planned |

For every selected file record: exact source URL, author, license text/file, modifications, attribution wording, original and optimized paths, dimensions/scale, byte size, texture counts and checksum. Retain source license evidence. AI-generated assets record provider, date, relevant usage terms and generation provenance. Do not assume free download means reusable.

## Import acceptance

At development start, validate each chosen model in the actual client: scale and facing direction, texture paths, no external URL, consistent shading, silhouette at the gameplay camera, and simple collision proxy alignment. Optimize copies, retain originals separately from the shipped bundle. Budget initial scene delivery to 15 MiB compressed as a tuning target, then measure on the demo machines.

Pre-development work is an inventory and license review; importing into a coded game waits for the development gate. Shipping an asset requires both provenance and runtime validation.

## Fallbacks

Use a smaller prop set before mixing styles. Remove optional wall art before compromising target visibility. Basic temporary test shapes are allowed during development, but the final slipper and cockroach must be recognizable. Asset quality may be simplified; licensing and offline availability may not.
