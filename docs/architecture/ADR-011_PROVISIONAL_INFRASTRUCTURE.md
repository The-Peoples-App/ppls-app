# ADR-011: Provisional Infrastructure & Module Scaffolding

## Status
Proposed (Epic: Infra/DX)

## Context
HALA’s roadmap requires complex features (Maps, Wizards) in future tiers. Developing these in isolation later would require costly refactoring of the Pilot (Bronze) code. We need to ensure the $10k investment creates a "Forward-Compatible" foundation.

## Decision: The "Pluggable" Architecture
We will implement **Provisional Scaffolding** for all Tier 2/3 features during the Pilot phase.
1. **Structural Placeholders:** We will architect the "Module Hooks" (e.g., Navigation Stacks and Data Resolvers) for Maps and Wizards now. 
2. **Logical Continuity:** Where Pilot development naturally intersects with future requirements (e.g., the CalFresh Reward Logic), we will build the underlying engine to be "Wizard-Ready," ensuring no work is duplicated.
3. **Budget Stewardship:** Full-scale development of "Silver/Gold" features remains deferred until funding is secured. The Pilot focus remains on the "To-the-Point" Static Reader and the CalFresh Calculator.

## Consequences
- **Pro: Reduced Technical Debt.** Prevents the need to "tear down walls" to add new rooms later.
- **Pro: Strategic Value.** HALA can demonstrate "Technical Readiness" to donors, proving the project is ready for immediate scaling once a grant is awarded.
- **Con:** Requires slightly higher initial design effort to ensure the "Chassis" is strong enough for future modules.

