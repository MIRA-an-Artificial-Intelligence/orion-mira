# Architecture

This document records verified architecture decisions. Do not fill it with assumptions before inspecting the existing Orion codebase.

## Current application baseline

- Desktop framework:
- Electron version:
- Main process entry point:
- Renderer entry point:
- UI framework:
- Build command:
- Development command:
- Test command:
- Existing navigation/home-screen location:

## Proposed Mira modules

These are conceptual boundaries, not a mandate to create all folders immediately.

- Character: Live2D loading, resizing, expressions, motions, lifecycle.
- Animation/state: idle, listening, thinking, speaking, error.
- Voice: provider-neutral text-to-speech adapter.
- Speech: microphone permissions and speech-to-text adapter.
- Brain: provider-neutral model interface and conversation orchestration.
- Browser tools: validated, allow-listed actions exposed by Orion.
- Memory: local settings/history, only when required and designed.

## Data flow

User input → speech-to-text (if voice) → conversation/AI adapter → validated browser tool (if requested) → response text → text-to-speech → character speaking state.

## Security boundaries

- AI output is untrusted input.
- Validate every tool name and argument.
- Keep privileged Electron operations out of the renderer.
- Require user confirmation for sensitive or irreversible actions.
- Keep secrets out of Git and avoid unnecessary transmission of private data.
