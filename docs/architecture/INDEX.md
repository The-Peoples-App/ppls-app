# Techinical Governance ("Senior Architect" Layer)
## Architectural Decision Records
[`ADR-000`][ADR-000]: Overview of Core Decisions (Summary of `docs/architecture` files)

[`ADR-001`][ADR-001]: Local-First Sync Architecture (Expo SQLite + Drizzle). Ensuring utility in data-deserts.

[`ADR-002`][ADR-002]: The "Air-Gapped" Integrity Logic (AI cannot modify primary Guide Text)

[`ADR-003`][ADR-003]: Single Source of Truth (SSOT) Data Architecture

[`ADR-004`][ADR-004]: Gov-Level Accessibility (A11y) Standards

[`ADR-005`][ADR-005]: Design Token Management (Material Design 3 / Paper sync)

[`ADR-006`][ADR-006]: Privacy-First Social Telemetry (Anonymous impact tracking)

[`ADR-007`][ADR-007]: Stakeholder Communication & Transparency Framework

[`ADR-008`][ADR-008]: Content Management Strategy (CMS)

[`ADR-009`][ADR-009]: Staged Content Governance & Super-Admin Approval

[`ADR-011`][ADR-011]: Provisional Infrastructure & Module Scaffolding (Forward-Compatibility)

[`ADR-013`][ADR-013]: Data Enrichment & Third-Party API Integration

[`ADR-014`][ADR-014]: Hybrid Content Delivery (Static vs. Semantic)

[`ADR-015`][ADR-015]: SSG Engine Selection (Markdown-to-Native)

[`ADR-016`][ADR-016]: AI Semantic Layer (Redis powered RAG)

[`ADR-017`][ADR-017]: Component Registry & Widget Architecture

[`ADR-018`][ADR-018]: Web Management Layer (Staff Update Pipeline/Ask AI API)

[`ADR-019`][ADR-019]: Gold Tier Impact Intelligence Dashboard (Proof of Impact)

[`ADR-021`][ADR-021]: Resilient Localization (i18next + Locize Fallback)

[`ADR-022`][ADR-022]: Content Update Strategy (Bundled vs. Remote)

[`EXTENSIBILITY_STRATEGY`][EXTENSIBILITY_STRATEGY]: Modular Feature Gating. Architecture for Tiered "Plug-and-Play" scalability.

## Diagrams

[`DGRM-015`][DGRM-015]: Ingestion Flow: Staff Update to Redis/App (Markdown to Searchable AI)

[`DGRM-016`][DGRM-016]: Ask AI Sequence (Native App Digital Guide Queries)



[ADR-000]: ./ADR-000_OVERVIEW.md
[ADR-001]: ./ADR-001_OFFLINE_FIRST.md
[ADR-002]: ./ADR-002_AIR_GAPPED_LOGIC.md
[ADR-003]: ./ADR-003_SSOT_DATA_ARCHITECTURE.md
[ADR-004]: ./ADR-004_GOV_LEVEL_ACCESSIBILITY.md
[ADR-005]: ./ADR-005_DESIGN_TOKENS_MANAGEMENT.md
[ADR-006]: ./ADR-006_PRIVACY_ANALYTICS.md
[ADR-007]: ./ADR-007_STAKEHOLDER_MOMENTUM.md
[ADR-008]: ./ADR-008_CMS_OPTIONS.md
[ADR-009]: ./ADR-009_STAGED_CONTENT_GOVERNANCE.md
[ADR-011]: ./ADR-011_PROVISIONAL_INFRASTRUCTURE.md
[ADR-013]: ./ADR-013_DATA_ENRICHMENT.md
[ADR-014]: ./ADR-014_HYBRID_CONTENT_DELIVERY.md
[ADR-015]: ./ADR-015_SSG_ENGINE_SELECTION.md
[ADR-016]: ./ADR-016_AI_SEMANTIC_LAYER.md
[ADR-017]: ./ADR-017_COMPONENT_REGISTRY.md
[ADR-018]: ./ADR-018_WEB_MGMT_LAYER_API.md
[ADR-019]: ./ADR-019_STAKEHOLDER_DATA_DASHBOARD.md
[ADR-021]: ./ADR-021_RESILIENT_LOCALIZATION.md
[ADR-022]: ./ADR-022_CONTENT_UPDATE_STRATEGY.md
[DGRM-015]: ./DGRM-015_INGESTION_FLOW.md
[DGRM-016]: ./DGRM-016_ASK_AI_SEQUENCE.md
[EXTENSIBILITY_STRATEGY]: ./EXTENSIBILITY_STRATEGY.md
