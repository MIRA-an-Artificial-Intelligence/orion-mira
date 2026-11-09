# Orion + Mira

A private development repository for integrating Mira, a 2D AI companion, into the Orion desktop browser.

## Project status

**Planning / foundation stage**  
**Planned start:** 16 November 2026  
**Target v0.1:** 3 January 2027 (target only; release depends on acceptance checks)

## Start here

1. Read [`docs/ROADMAP.md`](docs/ROADMAP.md).
2. Review [`docs/PROJECT_STATUS.md`](docs/PROJECT_STATUS.md).
3. On the first development day, inspect the existing Orion application before moving or rewriting files.
4. Track all work through GitHub Issues and Milestones.

## Initial direction

- Character: Live2D Cubism Web SDK (prove compatibility before purchasing assets).
- UI: reuse Orion's existing renderer and UI stack.
- AI: provider-neutral adapter; OpenRouter is the initial gateway to test.
- Voice: provider-neutral adapter; evaluate availability, terms, quality, and cost before committing.
- Speech recognition: evaluate a Whisper-compatible implementation.
- Browser actions: explicit allow-listed Orion functions with validation and confirmation where appropriate.

Rive and PixiJS are deferred until a concrete requirement justifies adding another rendering/animation system.

## Repository structure

```text
.
├── docs/                 # Roadmap, architecture, decisions, progress
├── experiments/          # Isolated technology proofs of concept
├── assets/mira/           # Licensed character assets (do not commit restricted files)
└── .github/               # Issue templates and project workflow
```

This repository is currently the planning and experiment workspace. When the existing Orion source code is inspected, decide whether this repository will contain Orion itself or whether Mira will be developed in Orion's existing repository. Avoid duplicating or relocating a working application without a deliberate decision.

## Security

- Never commit API keys, tokens, private recordings, or credentials.
- Check each model/asset licence before use.
- Keep hosted-provider data retention and privacy terms in mind.
- Do not expose arbitrary shell, filesystem, or unrestricted JavaScript execution to an AI model.
