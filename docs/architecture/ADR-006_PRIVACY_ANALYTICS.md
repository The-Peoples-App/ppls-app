# ADR-006: Privacy-First Social Telemetry

## Status
Proposed (Tier 1 Baseline; Scaling to Tier 3 Gold)

## Context
HALA serves vulnerable populations, including undocumented Angelenos and individuals in high-stakes legal situations. Any perception of data-sharing with government agencies creates a "Chilling Effect" that prevents people from seeking life-saving food aid.

## Decision: The "Digital Sanctuary" Policy
We will implement a **Zero-PII / Anonymous-Only** data architecture.

1. **No Identifiers:** We will not collect Names, Emails, Phone Numbers, or IP Addresses. 
2. **Local-Only Logic:** All "CalFresh Reward Calculations" happen exclusively on the user's device. No income data is ever transmitted to a server.
3. **Anonymous Telemetry:** The only data collected is aggregate usage metrics (e.g., "1,000 searches for Food Pantries in South LA") used solely for securing private Grant funding.
4. **Transparency:** A clear "Privacy Shield" notice will appear on the first launch, stating: *"This app does not track you. We do not share data with the government."*

## Tier 3 (Gold) Implementation: The "Impact Intelligence" Layer
In the Gold Tier, we will scale this telemetry to provide HALA with high-level advocacy data (e.g., Heatmaps of service demand) while maintaining 100% anonymity. This "Rich Data" is used to prove the app's ROI to major foundations (Rose Hills, Parsons) without compromising a single user's identity.

## Consequences
- **Pro:** Maximum community trust and adoption among vulnerable populations.
- **Pro:** "Grant-Ready" impact data for organizational sustainability.
- **Con:** We cannot "re-market" to users or send personalized emails (a worthwhile trade-off for safety).

