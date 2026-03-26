# ADR-008: Content Management Strategy (CMS)

## Status
Proposed (Tier 2 Silver Milestone)

## Context
HALA staff are non-technical and comfortable with NationBuilder's WYSIWYG editor. However, the current "Founding Leader" plan does not provide API access, blocking an automated sync for the Pilot.

## Decision: The "Manual-to-Modular" Pivot
1. **Bronze (Pilot):** We will utilize a "Manual Firestore CMS." Staff will provide a text version of the guide, which we bundle via the [SSG Engine Selection (ADR-015)](./ADR-015_SSG_ENGINE_SELECTION.md).
2. **Silver (Interactive):** Once funding is secured for a NationBuilder plan upgrade, we will implement the [Headless Sync Engine](./ADR-021_RESILIENT_LOCALIZATION.md).
3. **Architecture:** The app is being built "API-Ready." We are using a JSON-driven [Component Registry (ADR-017)](./ADR-017_COMPONENT_REGISTRY.md) so that switching from manual text to an automated CMS requires zero code changes to the app's UI.

## Consequences
- **Pro:** $0 monthly software increase for the Pilot.
- **Pro:** Clean separation of concerns; no "spaghetti code" linking the app to a legacy CRM prematurely.
- **Con:** Requires a one-time manual "Content Migration" from staff-provided text to the app's internal schema.

