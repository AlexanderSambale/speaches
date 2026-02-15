# Current Context

## Current work focus
- Finalising the memory‑bank documentation to capture the project's architecture, technology stack, and recent changes.
- Preparing the repository for upcoming feature work on **real‑time voice chat** enhancements and **model discovery** UI.

## Recent changes
- Added comprehensive documentation under `docs/usage/` for dynamic model loading and realtime API usage.
- Refactored the executor layer to standardise model manager interfaces (`BaseModelManager`).
- Integrated OpenTelemetry tracing for FastAPI and model execution paths.
- Updated Dockerfile to support both CPU and GPU base images and added caching layers for faster builds.

## Immediate next steps
1. Review and validate the newly created memory‑bank files (`product.md`, `context.md`, `architecture.md`, `tech.md`).
2. Optionally create a `tasks.md` file to capture repetitive workflows (e.g., adding a new model, updating Docker builds).
3. Perform a consistency check across all memory‑bank files and update any missing details.