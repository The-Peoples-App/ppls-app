# ADR-002: Modular Navigation & Feature Isolation

## Status
Proposed (Epic: UX/UI & Infra/DX)

## Context
The Peoples App is a 3-tiered product. We need a navigation architecture that allows "Bronze" features (Static Reader) to exist standalone, while providing "Plugs" for "Silver" (Maps) and "Gold" (Wizards) without refactoring the core codebase.

## Decision
We will implement a **Stack-per-Feature** pattern using **React Navigation**.
1. **Isolation:** Each Tier/Feature (e.g., `features/calfresh`, `features/directory`) will export its own Navigation Stack.
2. **Feature Gating:** A central `RootNavigator` will use a configuration file (`features.config.ts`) to conditionally inject these stacks based on the current Tier/Funding milestone.
3. **The Pilot Toggle:** For Bronze, the primary navigation will be a **Bottom Tab** or **Top Toggle** specifically isolating the "Static Reader" and the "AI Search" modules.

## Consequences
- **Pro:** Clean Architecture. Adding the "Gold" SNAP Wizard later is as simple as adding one line to the `RootNavigator`.
- **Pro:** High Velocity. You and your partner can work on separate "Feature Stacks" without merge conflicts in the main navigation file.
