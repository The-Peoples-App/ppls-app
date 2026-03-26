# ADR-017: Component Registry & Widget Architecture

## Status
Proposed (Epic: Infra/DX & Backend)

## Context
HALA requires a system that is "to-the-point" but expandable. We need to transition from a static print guide to a dynamic mobile experience where interactive tools (Calculators, Maps) are embedded within advocacy text. A hard-coded UI would require developer intervention for every update, creating a bottleneck.

## Decision
We will implement a **JSON-Driven Component Registry**. The application will not render "Pages," but rather "Manifests" that resolve to specific React Native components.

### 1. The Manifest Schema
Each resource or guide section will be defined by a JSON array of "nodes":
- **Type: `text`** -> Renders high-contrast Markdown (ADR-015).
- **Type: `widget`** -> Renders a functional logic engine (e.g., CalFresh Calculator).
- **Type: `action`** -> Renders a high-visibility button (e.g., "Call DPSS").

### 2. The Widget Registry
We will maintain a central `WidgetRegistry.ts` that maps string keys to functional components.
- `name: "CalFreshCalc"` -> References the `src/components/widgets/CalFreshCalculator.tsx` module.
- This allows staff to "invoke" complex logic simply by referencing the widget name in their content updates.
- **Passive Scaffolding (Hardware Resilience):** To support the low-end hardware standards in **ADR-004**, the Registry utilizes "Lazy Loading." Widgets are only initialized and consumed by the CPU/RAM when explicitly called by a Page Manifest, ensuring the "Static Reader" remains high-performance on older devices.

### 3. The "Silver" Migration Path
While Bronze uses manual JSON/Markdown files, this architecture is "CMS-Ready." In the Silver Tier, the WYSIWYG editor will simply output this same JSON schema, requiring **zero refactoring** of the mobile client's rendering logic.

## Consequences
- **Pro: Modular Scalability.** New widgets (e.g., SNAP Wizard, Map Search) can be added to the registry and inserted into any page without changing the navigation or screen logic.
- **Pro: Clean AI Ingestion.** Because content is separated from logic in the JSON manifest, the **AI Search Engine (ADR-014)** can parse the `text` nodes with 100% accuracy.
- **Con:** Requires initial overhead to build the "Manifest Resolver" component during the Bronze Pilot.

