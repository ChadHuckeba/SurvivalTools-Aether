# Technical Spec | Google API Quota Efficiency

## 1.0 Problem Statement
Aether's real-time ingestion engine frequently encounters `HTTP 429 RESOURCE_EXHAUSTED` errors when interacting with the Google Gemini API. This is primarily caused by:
*   **Fixed Debounce (5s):** Rapid save-bursts trigger syncs faster than the free-tier quota (approx. 15 RPM) can reset.
*   **Concurrent Syncing:** Multiple projects syncing in parallel double or triple the API request volume.
*   **Burst Traffic:** LlamaIndex batch embedding calls are dispatched in rapid succession, exceeding burst limits even if the total RPM is low.

## 2.0 Strategic Research Plan

### Phase 1: Quantitative Baseline
*   **Quota Tracking:** Implement a `QuotaTracker` utility to intercept and log rolling 60-second request counts.
*   **Error Characterization:** Determine if 429s are triggered by RPM (Requests Per Minute) or TPM (Tokens Per Minute).

### Phase 2: Structural Throttling
*   **Leaky Bucket Semaphore:** Wrap the embedding model in a throttler that enforces a mandatory delay (e.g., 4s) between batch requests.
*   **Adaptive Debouncing:** Replace the fixed 5s debounce with an "Activity-Aware" window (e.g., waiting for 20s of silence after a file modification).
*   **Global Ingestion Queue:** Implement a sequential lock to ensure only one project is indexing at any given time.

### Phase 3: Content Optimization
*   **Boilerplate Filtering:** Refine `REQUIRED_EXTS` and exclude standard files (e.g., `LICENSE`, `__init__.py`) that don't require semantic indexing.
*   **Chunk Tuning:** Increase `chunk_size` from 1024 to 2048+ to reduce the total number of API calls per file.

## 3.0 Implementation Roadmap

| Feature | Priority | Impact | Difficulty |
| :--- | :--- | :--- | :--- |
| Sequential Sync Lock | High | High | Low |
| Leaky Bucket Throttler | High | High | Medium |
| Adaptive Debounce | Medium | Medium | Medium |
| Quota Telemetry | Medium | Low | Low |

## 4.0 Observability (Cairn Integration)
All quota-related events must be logged with specific tags for ingestion into health dashboards:
*   `[aether.quota] [WARN] - Approaching 80% limit`
*   `[aether.quota] [ERROR] - 429 Detected; entering cool-down mode`

## 5.0 Future Considerations
*   **Local Fallback:** Explore using `sentence-transformers` for local embeddings if the Google API is consistently saturated.
*   **Diff-Aware Sync:** Explore file-level diffing to avoid re-embedding unchanged functions within a modified file.
