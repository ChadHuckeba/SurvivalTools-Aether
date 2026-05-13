# SurvivalStack | Aether®
### Real-Time Semantic Code Oracle

Aether is a high-fidelity context engine built on LlamaIndex and Google Gemini. It serves as a real-time "Code Oracle," providing agents with deep architectural intelligence through automated, real-time ingestion of local source code.

## 🚀 Key Features

*   **Real-Time Ingestion**: A native file watcher mirrors your local filesystem into a semantic index instantly.
*   **Efficiency First**: Lazy-loading and explicit memory release endpoints keep your system fast.
*   **Agent-Native**: Built-in support for the Model Context Protocol (MCP) for seamless integration with AI agents.
*   **Project Agnostic**: Rapid context switching between multiple projects via the Project Registry.

## 🏁 Quick Start

### 1. Prerequisites
*   [uv](https://github.com/astral-sh/uv) (Fast Python package manager)
*   Google Gemini API Key

### 2. Installation
```bash
git clone https://github.com/ChadHuckeba/SurvivalTools-Aether
cd SurvivalTools-Aether
uv sync
```

### 3. Configuration
Create a `.env` file in the root:
```env
GEMINI_API_KEY=your_key_here
AETHER_SAFE_ROOT=/path/to/your-projects-root
```

### 4. Start the Oracle
```bash
./session.sh start
```
Access the Dashboard at **[http://localhost:8000](http://localhost:8000)**.

## 📖 Documentation Index
For detailed technical guides, explore the Aether Vault in `/docs`:

*   **[Ingestion Engine](./docs/ENGINE.md)**: How the real-time watcher and incremental refresh logic works.
*   **[Observability](./docs/OBSERVABILITY.md)**: Guide to Cairn logs, functional hierarchy, and troubleshooting.
*   **[Integrations](./docs/INTEGRATIONS.md)**: How to connect agents via MCP and REST API reference.
*   **[Registry & Security](./docs/REGISTRY.md)**: Managing project contexts and SAFE_ROOT boundaries.

---
© 2026 SurvivalStack
