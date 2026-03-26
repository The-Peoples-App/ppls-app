# Extensibility & Feature Evolution Strategy

## 1. The "Interface-First" Core
To ensure the Pilot (Bronze) can scale to Gold, we will use **Abstract Interfaces** for all data fetching. 
- **Bronze:** `ResourceService` fetches from a local Firestore cache.
- **Gold:** `ResourceService` is extended to include `AISearchProvider` without changing the UI components.

## 2. Feature Gating & Configuration
We will implement a `src/config/features.ts` manifest.
- **Pilot Mode:** `MAPS_ENABLED: false`, `SNAP_WIZARD: false`.
- **Strategy:** This allows us to keep "Silver" and "Gold" code in the main branch as they are developed, toggling them on only when specific grant funding milestones are met.

## 3. Slot-Based UI Architecture
Using **React Native Paper**, we will build "Compound Components."
- **Example:** The `ResourceCard` will have a `renderActions` slot. 
  - **Bronze:** Slot renders a "Call" button. 
  - **Gold:** Slot renders an "Check SNAP Eligibility" button via a dynamic injection pattern.

## 4. Schema Versioning (Firestore)
- **Pilot Schema:** Focuses on `Identity` (Name, Location, Category).
- **Extensibility Attribute:** Every document includes a `metadata: Map<string, any>` field. 
- **Evolution:** As we move to Gold, we populate `metadata.eligibility_rules` to feed the AI Wizard, requiring **zero** database migrations.

## 5. Module Decoupling (The "Unix" Philosophy)
Following the Unix-centric DX, we will treat the **SNAP Wizard** and **Map Engine** as separate packages within a **Monorepo (Turborepo/Yarn Workspaces)**. 
- **Advancement:** This allows the "Ingestion Engine" to be sold or licensed to other NGOs as a standalone tool.

