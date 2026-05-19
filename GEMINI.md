# AETHER: ARCHITECTURAL SOURCE OF TRUTH
*Governs project-specific architecture, localized mandates, and strategic intent. Procedural execution is delegated to specialized SKILLS.*

### Architecture at a Glance
| Component | Purpose | Role |
| :--- | :--- | :--- |
| **Policy** | This file (\`GEMINI.md\`) | **Supreme Authority** |
| **Memory** | \`MEMORY.md\` | Persistent State |
| **Docs** | \`/docs/\` | Functional Specs |

### Precedence Statement
**Global Policy (Ecosystem) > Project Policy (Local).** This file may add project-specific specificity but cannot contradict Global mandates. In this repository, \`/docs\` expands upon the architectural truth established in \`GEMINI.md\`, but \`GEMINI.md\` retains highest precedence for autonomous mandates.

---

## 1. Project Architecture & Constraints

### 1.1 Aether Supremacy (RAG-First)
The \`/docs\` directory contains the authoritative internal mechanics and engine specifications for Aether. These documents govern implementation detail. \`GEMINI.md\` governs autonomous agent behavior and mandate compliance.
- **RAG-First Mandate**: AI Agents MUST prioritize semantic codebase intelligence. Before manually exploring files via \`read_file\` or \`grep_search\` to understand architecture, the agent MUST execute the \`query_codebase\` MCP tool.

## 2.0 OPERATIONAL MANDATES

### 2.1 Documentation Impact Assessment (DIA)
*   **Mandate**: Any modification to \`src/aether/core/watcher.py\` or \`src/aether/core/ingest.py\` REQUIRES a sibling update to \`docs/ENGINE.md\`.
*   **Enforcement**: Code changes are considered "behaviorally incomplete" without documentation alignment.

### 2.2 Telemetry Discipline
*   **Mandate**: All new modules MUST initialize a hierarchical logger via \`logging.getLogger("aether.<module>")\`.
*   **Standard**: Use of the raw \`print()\` function for telemetry is strictly prohibited.

## 3.0 TROUBLESHOOTING PROTOCOL
*   If ingestion appears stalled, the agent MUST:
    1. Check \`logs/aether.log\` for \`[ERROR]\` or \`429 RESOURCE_EXHAUSTED\`.
    2. Consult \`docs/OBSERVABILITY.md\` for functional hierarchy mapping.
    3. Verify \`SAFE_ROOT\` settings in \`.env\`.
