# Architecture and Product Decisions

Record decisions that affect scope, dependencies, cost, privacy, or future maintenance.

## Decision log

| Date | Decision | Reason | Revisit condition |
|---|---|---|---|
| 2026-11-09 | Start with Live2D as the character-runtime candidate | Best fit for an anime-style 2D character; must be proven in a small test | If runtime compatibility or licensing fails |
| 2026-11-09 | Defer Rive and PixiJS | Avoid multiple rendering systems before a demonstrated need | Add only for a specific interaction/scene requirement |
| 2026-11-09 | Keep AI and voice providers replaceable | Avoid coupling the product to one hosted service | Revisit after benchmark results |

## Proposed technology decisions — not yet verified

- AI gateway/model:
- TTS provider/voice:
- Speech recognition runtime:
- Character model and licence:
- Local storage approach:
