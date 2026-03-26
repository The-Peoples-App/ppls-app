# ADR-013: Citizen-Led Data Verification & SSOT Strategy

## Status
Proposed (Revised: Abandoning external API dependency)

## Context
Research indicates a total lack of a reliable, real-time SSOT for food resources in LA County. Existing platforms (211, Food Oasis) rely on manual, asynchronous verification. Relying on these for "Live" data creates a high risk of "Data Decay."

## Decision
The Peoples App will act as a **Primary Source of Truth**. 
1. **The Baseline:** Initial data is ingested from HALA's verified Guide.
2. **The Update Engine:** We will implement a "Suggest an Edit" feature in the **Silver Tier**. 
3. **The Governance:** All community-submitted changes (hours, closures) are staged in a **Verification Queue** for HALA staff approval (ADR-009).
4. **The SSOT:** Verified data in our Firestore becomes the authoritative digital record.

## Consequences
- **Pro:** Total Data Sovereignty. We don't break if a third-party API goes down.
- **Pro:** Grant Magnet. Proving that HALA owns the most accurate *digital* dataset in LA is worth $100k+ in "Innovation" funding.
- **Con:** Increases the "Staged Governance" workload for HALA staff.

