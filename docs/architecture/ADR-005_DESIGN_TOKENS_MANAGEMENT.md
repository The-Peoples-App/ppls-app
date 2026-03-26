# ADR-005: Design Token Management (Material 3 & AAA Contrast)

## Status
Proposed (Epic: Design System)

## Context
To meet WCAG 2.1 AAA standards for our Blind/Low-Vision (BLV) users, we need a deterministic way to manage colors and typography. Manual hex-code management is prone to "A11y drift" where contrast levels fail over time.

## Decision
We will implement a **Tokenized Design System** based on the **Material 3 Tonal Palette**.
1. **The System:** We will use `react-native-paper` to implement M3 "Schemes."
2. **The AAA Constraint:** We will exclusively use specific Tonal Steps (e.g., Tone 0 to Tone 100) that guarantee a 7:1 contrast ratio.
3. **The Sync:** Figma Styles (UX Lead) will map 1:1 to TypeScript Theme Tokens (Lead Dev), ensuring design-to-code parity.

## The HALA AAA Brand Palette (Verification)

| Role | Hex Code | Tone | AAA Contrast Ratio |
| :--- | :--- | :--- | :--- |
| **Primary** | `#1B5E20` | 20 | 7.8:1 on White |
| **On-Surface** | `#121212` | 10 | 18.7:1 on Surface |
| **Error** | `#B00020` | 40 | 7.3:1 on White |

## AAA Typography & Readability Scale

To meet WCAG 2.1 AAA (Success Criterion 1.4.8), our typography is engineered for maximum legibility in high-stress situations.

| Type Role | Font Size | Line Height | Character Limit |
| :--- | :--- | :--- | :--- |
| **Headline** | 32pt | 1.25x | Max 20 chars |
| **Title (Section)** | 22pt | 1.4x | Max 40 chars |
| **Body (Instructions)** | 18pt | 1.5x | Max 80 chars |
| **Label (Buttons)** | 14pt (Bold) | 1.2x | Max 20 chars |

### Structural Constraints:
- **No Justification:** Text is strictly left-aligned to prevent irregular spacing (rivers) which confuses BLV users.
- **Dynamic Scaling:** UI containers are "Flex-Ready" to support system font scaling up to 200% without clipping text.
- **Paragraph Spacing:** Set to 2x the line height to provide clear "Visual Anchors" between instructions.

## The Safe Pairing Matrix
To ensure 100% compliance during high-velocity development, we strictly adhere to these verified pairings:
- **Body Text:** `On-Surface` on `Surface`.
- **Action Buttons:** `On-Primary` on `Primary`.
- **Alerts:** `On-Error` on `Error`.

## The AAA "Safe" Palette (Reference)
To guarantee 7:1 (AAA) contrast, we will prioritize these pairings:
- **Surface:** `Neutral 98` (Near White) | **Text:** `Neutral 10` (Deep Black/Grey).
- **Primary Container:** `Primary 90` (Light Tint) | **On-Primary:** `Primary 10` (Dark Shade).
- **Error:** `Error 40` (Red) | **On-Error:** `Error 100` (Pure White).

## Consequences
- **Pro:** Automated Compliance. The system "prevents" the designer from picking a non-accessible color.
- **Pro:** High Velocity. Changing the brand color updates the entire app (3 tiers) instantly.
- **Advancement:** Proves "Design Systems Engineering" expertise—moving beyond "styling" into "systemic architecture."


