# ADR-014: Hybrid Content Delivery (Static vs. Semantic)

## Status
Proposed (Bronze Pilot Baseline)

## Context
HALA requires a "Static Version" for reliability but wants "AI Innovation" for accessibility. We need to deliver both without the complexity of a real-time CMS sync in the Pilot phase.

## Decision
We will implement a **Dual-Mode Delivery Engine**:
1. **The Static Layer (Resilience):** Utilizes the **ADR-015/016** pipeline to bundle staff-provided Markdown directly into the app binary. This serves as the "Single Source of Truth" (SSOT).
2. **The Semantic Layer (Discovery):** A Retrieval-Augmented Generation (RAG) implementation that indexes the `text` nodes from our **Component Registry (ADR-017)**.
3. **The UX Toggle:** A high-visibility UI switch (Tier 1) allowing users to move between "Reading the Guide" and "Asking the AI."

## Consequences
- **Pro:** High Performance. Offline reading has 0ms latency.
- **Pro:** High Trust. AI answers are strictly limited to the provided text context.
- **Con:** The AI index must be "re-generated" whenever the staff provides a new text version (handled via the Build Pipeline).

