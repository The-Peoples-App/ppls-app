# ADR-003: Single Source of Truth (SSOT) Data Architecture

## Status
Proposed (Replaces legacy AI-Extraction model)

## Context
The "Peoples Guide" is frequently updated (every few months) by HALA staff. To prevent "Data Drift" between the Print PDF and the Mobile App, we need a unified pipeline that respects the staff's manual editorial process while enabling modern app functionality.

## Decision
We will implement a **Staff-Led / AI-Augmented** pipeline:
1. **The Source:** HALA staff provides the "Text Version" (Markdown) of the guide (e.g., p37 CalFresh).
2. **The Pipeline:** A Node.js build-script bundles this text into a **Static Site Generation (SSG)** framework within the app.
3. **The Utility:** AI is utilized as a **Semantic Interface** (Search/Query) to answer user questions based on this verified text, rather than a primary data ingestion tool.

## Consequences
- **Pro:** 100% Data Parity. The App and the Print Guide always match.
- **Pro:** Empowered Staff. HALA maintains full editorial control without technical bottlenecks.
- **Pro:** Cost-Efficiency. Eliminates recurring AI API costs for data entry; AI credits are only used for user-facing queries.

## Cross-References
- **See [ADR-015: SSG Engine Selection](./ADR-015_SSG_ENGINE_SELECTION.md)** for the technical implementation of the Markdown-to-Native pipeline.
- **See [ADR-014: Hybrid Content Delivery](./ADR-014_HYBRID_CONTENT_DELIVERY.md)** for how this SSOT data is consumed by the AI Semantic Layer.

