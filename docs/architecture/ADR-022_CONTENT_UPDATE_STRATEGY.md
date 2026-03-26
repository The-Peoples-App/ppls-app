# ADR-022: Content Update Strategy (Bundled vs. Remote)

## Status
Proposed (Bronze: Bundled | Silver: Remote)

## Context
HALA staff updates the guide frequently. We need to balance "Update Speed" with the "Offline Sovereignty" and "Zero-Cost" requirements of ADR-004.

## Decision
1. **Bronze Pilot:** Utilize **Static Bundling**. Content is updated via EAS Updates (OTA) which replaces the local JSON bundle. This keeps costs at $0 and ensures 100% offline availability.
2. **Silver Tier:** Transition to a **Remote-Fetch Model**. The app will check Firestore for "Delta Updates" (changes only) to the p37-44 text, allowing for minute-by-minute accuracy.

## Operational Release Cadence
### Bronze Pilot (Scheduled Batches): 
- **Workflow:** Staff provides "Text Version" updates every 2–4 weeks. 
- **Deployment:** Lead Dev runs the `bin/generate-guide.js` script and pushes an **EAS Update (Over-The-Air)**. 
- **Effect:** Users receive the new "Static Bundle" the next time they open the app on Wi-Fi. This ensures 100% data parity with HALA's internal print cycles.

## Technical Update Boundaries (EAS vs. App Store)
To ensure maximum uptime and security, we distinguish between "Content" and "Infrastructure" updates:
- **Over-The-Air (OTA) Updates:** Utilizing Expo EAS, we can push critical "to-the-point" text changes (p37-44) and Calculator logic updates instantly to users. This bypasses standard App Store review wait times.
- **Native Store Releases:** Major infrastructure changes (e.g., adding New Hardware sensors or Biometric security) require a full App Store submission. 
- **Governance:** All OTA updates are subject to the same "Staged Approval" (ADR-009) as standard code, ensuring HALA's data integrity is never bypassed for speed.

### Silver/Gold Tier (On-Demand Remote):
- **Workflow:** Staff makes an update in the **Headless CMS (ADR-008)**. 
- **Deployment:** The CMS triggers a **Firestore Sync Event**. 
- **Effect:** The app "presents" the update to the user within seconds. This is reserved for high-volatility data like "Emergency Pop-up Pantries" or "Temporary Office Closures."

## Consequences
- **Security:** Static bundling prevents "Man-in-the-Middle" attacks on advocacy data.
- **Performance:** Local-first ensures the BLV screen-reader experience is never interrupted by "Loading..." states.

