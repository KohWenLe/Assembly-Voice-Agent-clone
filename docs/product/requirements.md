# Drive-thru voice agent — requirements discovery

Status: main interview decisions captured; consolidated draft ready for review. Updated 21 September 2026.

This document records the requirements conversation. Only items explicitly marked confirmed are settled. Recommendations and unanswered questions are not implementation commitments.

## Confirmed context

- The team is participating in the AssemblyAI Voice Agent Hackathon.
- The chosen product direction is a restaurant drive-thru voice agent, using restaurants such as McDonald's as an example.
- The primary objective is **order accuracy with a smooth customer experience**.
- The demo runs in a **browser**, with microphone input, a visible cart, and a **simulated kitchen ticket**.
- The first audience is **English-speaking customers** ordering from a **small fictional fast-food menu**.
- The menu includes **about 10 items, 2–3 meal combos, sizes, drink choices, and common modifiers** such as no onions.
- The customer confirms the total, receives an order number, and sees a simulated kitchen ticket. **Payment happens at the window**, outside the demo.
- The team has **three people**, no assigned roles, limited but unquantified available time, and an expected small but unquantified API/hosting budget.
- The agent asks only for missing or ambiguous choices, briefly acknowledges changes, and reads back the full order before submission.
- After **two unsuccessful clarifications of the same issue**, the agent offers simulated staff handoff. An explicit request for a person triggers handoff immediately; the cart is preserved.
- **Interruptions, mid-order corrections, and moderate background noise are all mandatory acceptance conditions.** Noise resilience is not a stretch goal.
- The current task is to define requirements together.
- Event constraints and supporting sources are in [the hackathon research brief](../research/2026-09-21-hackathon-requirements.md).

No real restaurant partnership, geographic market, exact menu contents/prices, technical stack, or product name has been agreed. The main scope and conversation policies are settled. The consolidated brief below proposes detailed defaults and measurable acceptance conditions for review.

## Round 1 — purpose and demo setting

| Decision | Choices presented | Accepted decision | Status |
| --- | --- | --- | --- |
| Main restaurant problem | Order accuracy; service speed; staff workload | Order accuracy, with smooth customer experience | Confirmed by user |
| Demo setting | Browser simulation; physical hardware; existing restaurant integration | Browser microphone, visible order, simulated kitchen ticket | Confirmed by user |
| Customers and language | General English; Malaysian English with local menu; specified multilingual audience | English and a fictional fast-food menu | Confirmed by user |

The user accepted the demo and audience recommendations and explicitly paired accuracy with smooth customer experience. Round 3 subsequently made moderate-noise operation mandatory; its measurement details remain proposed.

## Product brief

Build an English-language browser demonstration of a voice agent for fictional fast-food drive-thru ordering. Customers speak through a microphone and see their order in a cart; the restaurant side is represented by a simulated kitchen ticket. Prioritize accurate order capture and a smooth customer experience.

The confirmed endpoint is a full order readback and customer confirmation followed by an order number and simulated kitchen ticket, with payment directed to the window. Focused clarification, interruption handling, corrections, moderate-noise operation, and simulated staff handoff are required.

## Round 2 — menu, completion, and capacity

| Decision | Accepted answer | Status |
| --- | --- | --- |
| Menu complexity | About 10 items, 2–3 meal combos, sizes, drink choices, and common modifiers | Confirmed by user |
| Completion boundary | Confirm total; issue an order number and simulated kitchen ticket; payment happens at the window | Confirmed by user |
| Build constraints | Three people; roles unassigned; time limited but unquantified; budget expected to be small, amount unknown | Confirmed as current information |

The demo excludes taking payment, real POS integration, and physical drive-thru hardware. A numerical spending allowance has not been supplied. Plan for a small core scope and establish an operating-cost estimate when evaluating the implementation options.

## Confirmed functional scope

| ID | Customer-visible requirement | Acceptance evidence |
| --- | --- | --- |
| FR-01 | Customers can use a microphone to order in English in the browser. | A live spoken order is demonstrated in the deployed application. |
| FR-02 | A fictional menu offers about 10 items and 2–3 meal combos, with sizes, drink choices, and common modifiers. | The demo supports ordering an individual item and a configured meal. |
| FR-03 | Customers can see their order in a cart while ordering. | The items and options are visible during the conversation. |
| FR-04 | Customers confirm the total before the order is completed. | The completion flow includes customer confirmation. |
| FR-05 | Completion produces an order number and simulated kitchen ticket. | Both outputs are visible after confirmation. |
| FR-06 | The agent directs payment to the window. | The completion message explains where payment happens. |

These are the accepted capabilities. Round 3 below settles the main interaction policies; detailed data-integrity and recovery rules are proposed in the consolidated brief.

## Round 3 — conversation, fallback, and voice priorities

| Decision | Accepted answer | Status |
| --- | --- | --- |
| Clarification and confirmation | Ask only for missing or ambiguous choices; briefly acknowledge changes; give one full final readback before submission | Confirmed by user |
| Unresolved request or request for a person | Offer simulated staff handoff after two failed clarifications of the same issue; hand off immediately when explicitly requested; preserve the cart | Confirmed by user |
| Required voice challenge | Both interruptions/corrections and moderate background noise must pass acceptance tests | Confirmed by user; overrides noise-as-stretch recommendation |

The requirement for moderate noise is settled. The reproducible noise definition and performance thresholds in the consolidated brief are proposed measurement details, not measured capabilities.

## Consolidated brief for review

[MVP requirements brief](mvp-requirements.md) brings the decisions together with proposed detailed behavior, exclusions, acceptance scenarios, and quality targets. Its requirement-status labels distinguish user-confirmed scope from defaults awaiting review. This discovery document preserves how those decisions were reached.

## Concrete menu proposal

[The proposed demo menu](demo-menu-proposal.md) supplies exactly 10 standalone products, three meal bundles, illustrative USD prices, removable ingredients, and worked totals. Only the overall menu complexity is approved; its specific contents and rules await review with the full requirements.

## Remaining review items

The consolidated brief now supplies concrete proposals for the remaining details: menu contents and USD prices; corrections/cancellation after submission; service recovery; customer and ticket views; session data handling; desktop-browser scope; and measurable noise/latency tests.

Review that package to settle these details. No additional product-choice questionnaire is pending. Technical stack, access to services, usage costs, a numerical budget, and task assignments belong to the following design/planning phase. No performance claims have been established.

## Decision log

| Date | Decision | Basis |
| --- | --- | --- |
| 2026-09-21 | Restaurant drive-thru voice agent | User's chosen hackathon concept |
| 2026-09-21 | Define product requirements before implementation | User's current request |
| 2026-09-21 | Prioritize order accuracy with a smooth customer experience | User's Round 1 answer |
| 2026-09-21 | Browser microphone demo, visible cart, simulated kitchen ticket | User accepted recommendation 2 |
| 2026-09-21 | English and a fictional fast-food menu | User accepted recommendation 3 |
| 2026-09-21 | About 10 items, 2–3 combos, sizes, drinks, and common modifiers | User's Round 2 answer |
| 2026-09-21 | Confirm total, issue order number and simulated kitchen ticket; pay at window | User's Round 2 answer |
| 2026-09-21 | Three-person team, no assigned roles, limited time, small expected budget with no stated cap | User's Round 2 answer |
| 2026-09-21 | Focused clarification, brief acknowledgements, one final readback | User's Round 3 answer |
| 2026-09-21 | Offer handoff after two unsuccessful clarifications; immediate handoff on request; preserve cart | User's Round 3 answer |
| 2026-09-21 | Interruptions/corrections AND moderate background noise are mandatory acceptance conditions | User's Round 3 answer |

The consolidated brief distinguishes confirmed scope from proposed details and acceptance targets. This document is the decision history; use the consolidated brief for the current product requirements review.
