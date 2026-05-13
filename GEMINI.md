# GEMINI GOVERNANCE ARCHITECTURE
# This file governs the "WHAT" and "WHY" (Policies, Mandates, and Strategic Intent).
# The "HOW" (Procedural Logic, CLI Flags, and Implementation Steps) is strictly reserved for SKILLS.

## Instruction Hierarchy & Paths
- **Global Policy (What/Why):** `~/.gemini/GEMINI.md` (Symlinked to `~/core/dotfiles/gemini/GEMINI.md`)
- **Project Policy (What/Why):** `<project-root>/GEMINI.md`
- **Global Skills Vault (How):** `~/core/dotfiles/gemini/skills-library/` (Canonical source)
- **Active Global Skills:** `~/.gemini/skills/` (Symlinks from vault)
- **Project Skills (How):** `<project-root>/.gemini/skills/` (Project-specific tools)

## Role Distinction
- **Global File:** Ecosystem-wide mandates, security policies, and governance standards.
- **Project File:** Localized architectural truth, specialized mandates, and project-specific strategic guardrails.
- **Skills:** Specialized, on-demand intelligence that provides the technical "How" for specific tools (e.g., gh, git, ruff) to keep the context window lean.

# AETHER: AGENT GOVERNANCE & PROTOCOLS

## 1.0 SUPREMACY & AUTHORITY
*   **Aether Supremacy (RAG-First)**: AI Agents MUST prioritize semantic codebase intelligence. Before manually exploring files via `read_file` or `grep_search` to understand architecture, the agent MUST execute the `query_codebase` MCP tool.
*   **Locational Authority**: The `/docs` directory is the **Supreme Source of Truth** for Aether's internal mechanics. Discrepancies between this file and the vault are resolved in favor of the specialized `.md` files in `/docs`.

## 2.0 OPERATIONAL MANDATES

### 2.1 Documentation Impact Assessment (DIA)
*   **Mandate**: Any modification to `src/aether/core/watcher.py` or `src/aether/core/ingest.py` REQUIRES a sibling update to `docs/ENGINE.md`.
*   **Enforcement**: Code changes are considered "behaviorally incomplete" without documentation alignment.

### 2.2 Telemetry Discipline
*   **Mandate**: All new modules MUST initialize a hierarchical logger via `logging.getLogger("aether.<module>")`.
*   **Standard**: Use of the raw `print()` function for telemetry is strictly prohibited.

## 3.0 TROUBLESHOOTING PROTOCOL
*   If ingestion appears stalled, the agent MUST:
    1. Check `logs/aether.log` for `[ERROR]` or `429 RESOURCE_EXHAUSTED`.
    2. Consult `docs/OBSERVABILITY.md` for functional hierarchy mapping.
    3. Verify `SAFE_ROOT` settings in `.env`.
