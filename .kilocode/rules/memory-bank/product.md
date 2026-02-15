# Product Overview

Speaches is an OpenAI‑compatible server that provides streaming speech‑to‑text (STT), text‑to‑speech (TTS), translation, and voice‑activity detection capabilities. It leverages state‑of‑the‑art models such as **faster‑whisper** for transcription, **piper** and **Kokoro** for speech synthesis, and integrates with the OpenAI Realtime API specification.

## Why the project exists
- **Unified API**: Allows existing OpenAI client libraries and tools to work with locally hosted or self‑hosted speech models without code changes.
- **Model flexibility**: Users can dynamically load and unload models, choosing between CPU and GPU execution.
- **Open source & extensible**: Provides a foundation for developers to add new models, custom pipelines, or integrate with other services.

## Problems it solves
- Eliminates reliance on proprietary cloud speech services.
- Reduces latency by running models close to the data source.
- Offers a consistent API surface for both STT and TTS, simplifying client development.

## High‑level goals
1. Provide a stable, well‑documented OpenAI‑compatible endpoint for speech tasks.
2. Support dynamic model loading, off‑loading, and automatic resource management.
3. Enable optional UI via Gradio for interactive testing and demos.
4. Maintain observability through OpenTelemetry integration.