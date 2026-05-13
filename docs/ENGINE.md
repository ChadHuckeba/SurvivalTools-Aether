# Aether | Real-Time Ingestion Engine

## Overview
Aether utilizes a native, "Always-on" file watcher system to ensure that the semantic index remains a high-fidelity mirror of your local filesystem.

## 1. The Sentinel (File Watcher)
The `ProjectWatcher` class in `src/aether/core/watcher.py` leverages the `watchdog` library to monitor the active project directory.

### Event Triggers
Aether responds to three primary event types:
*   **Created:** When a new file is added.
*   **Modified:** When an existing file is saved.
*   **Deleted:** When a file is removed.

### Debounce Logic (Quota Preservation)
To prevent rapid-fire indexing and protect Google Gemini API quotas, Aether implements a **5-second debounce period**.
*   **Logic:** Once an event is detected, any subsequent changes within the next 5 seconds are ignored.
*   **Reasoning:** This allows for "save bursts" (like a formatter running or multiple rapid edits) to be processed as a single logical ingestion task.

## 2. Incremental Ingestion (Refresh Pattern)
Aether does not re-index the entire project on every change. Instead, it uses the **incremental refresh** pattern:

1.  **Scan:** The engine performs a shallow scan of file metadata.
2.  **Compare:** It compares the current filesystem hashes with the hashes stored in `docstore.json`.
3.  **Surgical Update:** Only files that have been added or modified since the last sync are embedded via the Google Gemini API.
4.  **Purge:** Any nodes associated with deleted files are automatically removed from the vector index.

Example Flow:
`Syncing /path/to/project -> /path/to/aether/data/storage/project`

## 3. Performance & Lazy Loading
Aether is optimized for a "Zero-Impact" background presence:
*   **Sleep Mode:** The vector index is NOT loaded into RAM upon server start.
*   **Lazy Loading:** The index is only pulled into memory during the first query of a session.
*   **Release API:** The `/release` endpoint allows you to purge the index from RAM without stopping the server.
