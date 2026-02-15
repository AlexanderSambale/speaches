# Technology Stack

## Languages & Runtime
- **Python 3.12** – core implementation language.
- **Type hints** throughout the codebase for static analysis and IDE support.

## Frameworks & Libraries
- **FastAPI** – HTTP API server, dependency injection, OpenAPI generation.
- **Starlette** – underlying ASGI toolkit.
- **Pydantic & pydantic‑settings** – configuration validation and environment variable parsing.
- **uvicorn** – ASGI server.
- **OpenTelemetry** – tracing and metrics (`opentelemetry‑instrumentation‑fastapi`, etc.).
- **Gradio** – optional UI for interactive demos.
- **faster‑whisper** – speech‑to‑text model inference.
- **piper‑tts** – text‑to‑speech synthesis.
- **Kokoro‑onnx** – additional TTS model.
- **ctranslate2** – backend for Whisper model execution.
- **huggingface‑hub** – model discovery and download.
- **aiortc** – WebRTC support for realtime API.
- **httpx** – async HTTP client (used by OpenAI client wrappers).

## Build & Dependency Management
- **uv** – modern Python package manager, used in Docker builds (`uv sync`).
- **hatchling** – build backend defined in `pyproject.toml`.
- **Docker** – multi‑stage builds with CUDA base images for GPU support.
- **pre‑commit** – linting and formatting hooks (`ruff`, `basedpyright`).

## Observability & Monitoring
- **OpenTelemetry SDK** – traces exported via OTLP endpoint if configured.
- **Prometheus** – optional metrics endpoint (configuration files under `configuration/`).

## Constraints & Considerations
- GPU support requires NVIDIA CUDA base image; CPU fallback is provided.
- Model files are cached under the user’s home directory; permissions must be handled when mounting volumes.
- The `otel_exporter_otlp_endpoint` must be reachable from the container for tracing.
- Environment variables control feature toggles (e.g., `SPEACHES_LOG_LEVEL`, `ALLOW_ORIGINS`).