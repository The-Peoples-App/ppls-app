# ADR-021: Resilient Localization (i18next + Locize Fallback)

## Status
Proposed (Epic: State Mgmt / Infra)

## Context
HALA serves a multilingual population. We need the ability to update translations without a full App Store release (Locize), but we cannot allow a third-party service failure to render the app unusable.

## Decision
We will implement a **Chained Backend Strategy**:
1. **Primary (Locize):** Fetch "Live" translations via the Locize API for real-time updates.
2. **Fallback (Local):** Bundle the three highest-priority languages (English, Spanish, Korean/Tagalog) as static JSON files within the App binary.
3. **Detection:** Utilize `expo-localization` to automatically sync the app's language with the device's system settings.

## Consequences
- **Pro:** 100% Uptime. The app works even with zero data or expired API keys.
- **Pro:** High Velocity. You can fix a typo in Locize and it updates on users' phones instantly.
- **Advancement:** Proves "High-Availability (HA) Architecture" expertise.

