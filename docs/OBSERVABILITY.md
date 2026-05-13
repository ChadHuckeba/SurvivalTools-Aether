# Aether | Observability & Troubleshooting

## Overview
Aether uses a professional telemetry stack to ensure that all background activities are auditable. This system is managed by the **[Cairn](https://github.com/ChadHuckeba/SurvivalStack-Cairn)® Logging Authority**.

## 1. Log Locations
*   **Primary Log:** `logs/aether.log`
    *   Captured by Cairn®. Contains all ingestion events, API calls, and errors.
*   **Startup Log:** `logs/startup.log`
    *   Captured by `session.sh`. Contains initial environment checks and Uvicorn server logs.

## 2. Functional Hierarchy
Cairn® prefixes each log line with the project name and the functional module to provide instant context.

*   `[aether] [aether.watcher]` - Events from the filesystem sentinel.
*   `[aether] [aether.ingest]` - Metadata scans and embedding tasks.
*   `[aether] [aether.api]` - Server lifecycles and endpoint requests.
*   `[aether] [aether.stats]` - Logical index reporting.

Example:
`[INFO] [aether] [aether.watcher] - Watching <ProjectName> at <Path>`

## 3. Common Troubleshooting

### `429 RESOURCE_EXHAUSTED` (Google API Quota)
**The Problem:** The Google Gemini API free tier limits embeddings to 15 requests per minute. Rapid-fire file changes can exceed this.
*   **Evidence:** `[ERROR] [aether.api] - Ingestion error: 429 RESOURCE_EXHAUSTED`
*   **Solution:** Aether handles this gracefully via its 5-second debounce. If you hit this, wait 60 seconds for the quota to reset.

### `package not found: llama-index-readers-file`
**The Problem:** Missing optional dependency for optimized file reading.
*   **Evidence:** Recurring warnings in `aether.log` during ingestion.
*   **Solution:** Execute `uv add llama-index-readers-file` in the Aether root.

### `Access Denied: Path outside safe root`
**The Problem:** Security boundary enforcement.
*   **Solution:** Ensure the project path you are adding is a subdirectory of the path defined in your `.env` as `AETHER_SAFE_ROOT`.
