# ADR-004: Gov-Level Accessibility (A11y) Standards

## Status
Proposed (Epic: Design System / UX/UI)

## Context
HALA serves a diverse demographic, including a significant population of Blind and Low-Vision (BLV) users. To qualify for federal grants and ensure equitable food access, the app must meet or exceed WCAG 2.1 Level AA (with AAA targets for contrast and typography).

## Decision: The "A11y-First" Architecture
We will implement a design system that treats screen readers and high-contrast visuals as the primary interface, not an afterthought.

1. **Semantic Structure:** Every component will utilize `accessible={true}` and `accessibilityRole` (header, button, link) to ensure Screen Readers (VoiceOver/TalkBack) provide a logical mental map of the CalFresh guide.
2. **Visual Equity (AAA Standards):**
   - **Contrast:** Minimum 7:1 ratio for all body text (exceeding the standard 4.5:1).
   - **Scale:** Support for system-level dynamic font scaling without UI breakage.
3. **Screen Reader Optimization:**
   - **Custom Hints:** Every action (e.g., "Call DPSS") will include an `accessibilityHint` explaining exactly what happens when tapped.
   - **Focus Management:** Logic to ensure the screen reader focus moves predictably through the CalFresh "Next Steps" checklist.
4. **Blind/Low-Vision Specifics:**
   - **Haptic Feedback:** Physical vibrations to confirm successful "Reward Calculations."
   - **Alternative Text:** 100% coverage for all iconography and "Static Guide" imagery.
5. **Hardware & Connectivity Resilience (Low-End Devices):**
   - **Performance Budget:** We will prioritize "Passive Scaffolding" (ADR-017 Widget Registry) to ensure the app remains performant on devices with limited RAM/CPU (older Android/iOS).
   - **Binary Size Optimization:** By utilizing a "Static-First" SSG engine (ADR-015), we keep the initial download size minimal, respecting users with limited data plans.
   - **Offline Sovereignty:** Full functionality of the "Static Reader" and "Reward Calculator" without a network connection, ensuring the app is not a "brick" in data deserts.


## Consequences
- **Pro:** "Grant-Ready" status for high-level government and private foundation funding.
- **Pro:** Total inclusivity for HALA’s most vulnerable BLV users.
- **Con:** Incremental design/dev overhead (approx. 15-20%) for testing on physical devices with screen readers.

