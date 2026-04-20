# ADR-021: Resilient & Context-Aware Localization

## Status
Proposed (Epic: State Mgmt / Infra)

## Context
The People’s Guide project requires high-precision accuracy for legal and social service terminology (e.g., CalFresh, Redetermination). Per the project requirements, translations must be governed by experts. Technically, we must balance the **Offline Sovereignty** of **ADR-015** with the need to update content without an App Store release.

## Decision
We will implement a **Hybrid Continuous Localization Pipeline** using **i18next** and **Locize**, integrated directly into our existing Markdown build process.

1. **Chained Backend Logic:**
  * **Primary (Locize API):** The app attempts to fetch "Live" translations from Locize on startup to allow for instant hotfixes to eligibility rules or office closures.
  * **Fallback (Local Bundle):** We will bundle English, Spanish, and Korean/Tagalog as static JSON files. This ensures the app remains a "Sovereign" tool (ADR-???) that works with zero connectivity.
  * **Detection:** Utilize `expo-localization` to automatically sync the app's language with the device's system settings.

2. **Integrated Data Pipeline (Ref: ADR-015 & ADR-016):**
  * The `bin/generate-guide.js` script (**ADR-015**) will serve as the "Source of Truth."
  * When the script runs, it generates `bundled-assets.json`, pushes to Redis (**ADR-016**), then syncs new English strings from the Markdown `front-matter` and `content` to Locize via the **Locize CLI**.

3. **Expert Glossary Enforcement:**
  * A mandatory **"Social Services Lexicon"** will be maintained within Locize to be managed by staff (lawyers, social workers, advocates etc.).
  * Technical terms (CalFresh, CalWORKs, EBT) are "locked" to prevent generic machine translation errors. Translators are prompted with vetted terminology used by social workers.

4. **Sync Architecture:**
  * **Source:** `raw_content/*.md` (**ADR-015**)
  * **Step 1:** Build script parses Markdown → Bundled JSON (Static Guide +3 top langs).
  * **Step 2:** Build script pushes text chunks to Redis for AI RAG (**ADR-016**).
  * **Step 3:** Build script pushes new strings to Locize for human translation.
  * **Step 4:** Deployment via **EAS Update** (OTA) refreshes the local fallback bundle.
   
## Technical Implementation
```ts
// i18next configuration supporting the ADR-015 fallback
import i18n from 'i18next';
import ChainedBackend from 'i18next-chained-backend';
import LocizeBackend from 'i18next-locize-backend';
import resourcesToBackend from 'i18next-resources-to-backend';

i18n
  .use(ChainedBackend)
  .init({
    backend: {
      backends: [
        LocizeBackend, // 1. Check for live expert updates
        resourcesToBackend((lng, ns) => import(`./assets/locales/${lng}.json`)) // 2. ADR-015 Local Bundle
      ],
      backendOptions: [{
        projectId: process.env.LOCIZE_PROJECT_ID,
        apiKey: process.env.LOCIZE_API_KEY,
        referenceLng: 'en'
      }]
    },
    // Ensure AI Search (ADR-016) and UI use the same language context
    lng: 'en', 
    fallbackLng: 'en'
  });
```

## Consequences

* **Pro (Consistency):** The AI (ADR-016), the Static Reader (ADR-015), and the Translations all share the same source Markdown files.
* **Pro (Expertise):** Locize provides a UI for social service experts to review and approve terminology without touching code.
* **Pro (Resilience):** If Locize is down or the user is in a "data desert," the app falls back to the local JSON bundle created in ADR-015.
* **Con (Complexity):** The `generate-guide.js` script now has three responsibilities: JSON bundling, Redis indexing, and Locize syncing.


