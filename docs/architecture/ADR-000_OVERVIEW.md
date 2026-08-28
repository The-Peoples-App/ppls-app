Summary — Single-page overview of docs/architecture files

Purpose
- These architecture notes define a staff-first, offline-first content pipeline for The Peoples App that combines a static “single source of truth” (SSOT) with an AI-powered semantic query layer. The emphasis is on accuracy, offline reliability, low cost, and safe AI use.

Core decisions
- ADR-001 (OFFLINE-FIRST ARCHITECTURE): Offline data access due to data-deserts/connectivity issues will be implemented using a Timestamp-Based Delta Sync.
- ADR-003 (SSOT): Staff provide canonical guide text in Markdown. The pipeline is “Staff-Led / AI-Augmented” — AI is a query interface only, not the primary ingest mechanism, to prevent data drift and protect editorial control.
- ADR-015 (SSG Engine Selection): Use markdown files with YAML front-matter and a build script (bin/generate-guide.js) to produce a single optimized JSON bundle (assets/bundled-guide.json). Render in-app with react-native-markdown-display. Benefits: minimal runtime parsing, offline operation, tiny latency.
- ADR-014 (Hybrid Content Delivery): Deliver content in two modes — Static Layer (bundled, offline SSOT) and Semantic Layer (RAG-based search over text nodes). Provide a UI toggle allowing users to read the guide or ask the AI.
- ADR-018 (Web Management Layer & API): Use an Astro site + Astro Actions as the server-side bridge to Redis + LLMs. Server actions validate input (Zod), run embeddings/similarity searches in Redis, and call the LLM server-side so API keys remain hidden. Example action shows RedisVectorStore + OpenAIEmbeddings + ChatOpenAI usage.
- ADR-002 (Air-Gapped Logic): Keep a verified read-only layer and an isolated AI sandbox; AI cannot write edits to canonical content. UI explicitly separates contexts to prevent hallucination-led edits.
- ADR-008 (CMS Options): Pilot uses a Git-based repository Markdown workflow to avoid CMS operational costs; later tiers will introduce headless API sync pipelines when funding allows.
- Extensibility Strategy: Interface-first services, feature flags, slot-based UI components, schema versioning (metadata map), monorepo modularity to enable incremental upgrades to richer features.
- Ingestion Flow: The build pipeline parses staff Markdown → bundles JSON for app and sends text chunks to OpenAI for embeddings → stores vectors + metadata in Redis. (Mermaid sequence documented.)
- ADR-019 (Impact Dashboard): Long-term plan for server-side aggregation of anonymized events and an authenticated dashboard to measure program impact.

Consequences & tradeoffs (summary)
- Pros: 100% editorial control, offline-first reliability, 0ms in-app latency for static reads, reduced AI costs (only query-time), safer AI behavior via air-gap and server-side controls.
- Cons: Static content updates require app releases or OTA updates; the AI index must be regenerated on content changes; some hosting cost for SSR Astro Actions.

What this means practically
- Staff edit Markdown; CI/build runs bin/generate-guide.js to produce bundled-guide.json and refresh embeddings into Redis. The mobile app ships the bundled JSON for offline use while querying the server-side Semantic Layer for AI-assisted answers when needed — with safeguards to keep the canonical content immutable.
