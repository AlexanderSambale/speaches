# System Architecture

## High‑level components
- **FastAPI application** (`src/speaches/main.py`) – entry point, mounts routers, handles configuration and telemetry.
- **Routers** (`src/speaches/routers/`) – expose OpenAI‑compatible endpoints for chat, STT, TTS, diarisation, VAD, etc.
- **Executors** (`src/speaches/executors/`) – concrete implementations for each model type (e.g., Whisper, Piper, Kokoro). Each executor implements a shared `BaseModelManager` interface for model lifecycle management.
- **Model Registry** (`src/speaches/model_registry.py`) – discovers remote and local models via HuggingFace APIs.
- **Realtime subsystem** (`src/speaches/realtime/`) – WebSocket handling, audio stream tracking, and event routing.
- **UI layer** (`src/speaches/ui/`) – optional Gradio UI mounted on the FastAPI app when `enable_ui` is true.
- **Configuration** (`src/speaches/config.py`) – Pydantic‑based settings loaded from environment variables.
- **Observability** (`src/speaches/tracing.py`) – OpenTelemetry setup for request tracing and metric export.

## File‑path map (selected)
- `src/speaches/main.py` – app creation and router registration.
- `src/speaches/config.py` – settings model.
- `src/speaches/executors/whisper.py` – Whisper transcription/translation executor.
- `src/speaches/executors/piper.py` – TTS executor for Piper models.
- `src/speaches/routers/stt.py` – STT endpoint definitions.
- `src/speaches/realtime/session.py` – session management for realtime API.
- `src/speaches/ui/app.py` – Gradio UI construction.

## Design patterns
- **Dependency injection** via FastAPI dependencies (`ApiKeyDependency`, `get_executor_registry`).
- **Factory pattern** for executor creation based on model type.
- **Strategy pattern** for model loading (`BaseModelManager` with concrete managers).
- **Observer pattern** for realtime event routing (publish/subscribe via `pubsub.py`).

## Data flow (STT request example)
1. HTTP request → FastAPI router (`/v1/audio/transcriptions`).
2. Router validates API key, parses request, forwards to appropriate executor (`WhisperModelManager`).
3. Executor loads model (cached or downloads), runs inference via `faster_whisper`.
4. Result is formatted (`segments_to_transcription_response`) and returned as JSON or streaming events.
5. OpenTelemetry spans are created around each major step for tracing.