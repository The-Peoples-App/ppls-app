# ADR-009: Staged Content Governance

## Status
Proposed (Epic: Backend / Data Strategy)

## Context
HALA staff require the ability to update the "Peoples Guide" content frequently. However, direct, unvetted access to the production app database presents a high risk of data corruption, broken links, or formatting errors that could impact vulnerable users.

## Decision
We will implement a **Staged Approval Pipeline** for all content updates.
1. **The Staging Layer:** Staff updates are first pushed to a "Draft" collection in Firestore or a dedicated Git branch (`content-staging`).
2. **The Review Logic:** A simple internal dashboard or PR (Pull Request) process allows the Technical Lead to review changes against the **A11y/AAA Standards (ADR-004)**.
3. **The Promotion:** Only upon Lead approval is the data "promoted" to the production `bundled-guide.json` or live Firestore environment.

## Consequences
- **Pro:** High Data Integrity. Ensures that no broken tables or unverified numbers reach the community.
- **Pro:** Immutable Audit Trail. Provides a clear history of who changed what and when, ensuring organizational accountability.
- **Con:** Incremental Latency. Content updates are not "instant" and require a 24-hour review window.

