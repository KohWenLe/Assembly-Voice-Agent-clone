# Drive-thru voice agent — MVP requirements

Status: **draft for team review**, 21 September 2026. This is a product requirements brief, not a technical implementation plan.

**Confirmed** means the team explicitly selected the requirement. **Proposed** means a concrete default supplied for review. Acceptance targets are desired results, not measured capabilities.

## 1. Purpose and constraints — confirmed

Help customers place an accurate fast-food order through a smooth spoken conversation. Demonstrate the complete ordering journey in a browser using English, a fictional menu, a visible cart, and a simulated kitchen ticket.

The menu has about 10 items and 2–3 meal combos, including sizes, drink choices, and common modifiers. The customer hears a full readback, confirms the total, receives an order number and kitchen ticket, and is directed to pay at the window.

The agent must support customer interruptions, mid-order corrections, and moderate background noise. All three are required for acceptance. It asks only for missing or ambiguous choices, acknowledges changes briefly, and offers simulated staff handoff after two unsuccessful clarifications of the same issue. A direct request for a person triggers immediate handoff with the cart preserved.

There are three team members, no assigned roles, limited but unquantified available hours, and an expected small budget with no numerical cap yet. The hackathon requires meaningful AssemblyAI use and a usable online demonstration. See the [event research](../research/2026-09-21-hackathon-requirements.md) for the deadline and submission requirements.

## 2. Customer journey — confirmed flow, proposed detailed rules

| Stage | Customer experience | Detailed rule proposed for review |
| --- | --- | --- |
| Start | Start a browser voice conversation. | Explain microphone access, show the menu, and give one short greeting. A denied microphone permission produces an actionable message. |
| Order | Speak items, quantities, meals, and modifiers; see the cart update. | Support multiple items in one turn. Preserve every resolved choice while asking for missing details. |
| Correct | Add, remove, replace, or change an item, including while the agent speaks. | Stop the interrupted response, apply only the intended change, and briefly acknowledge it. Clarify ambiguous references before changing the affected item. |
| Review | Hear the complete order and total when finished ordering. | Include quantities, sizes, drink choices, and modifiers. Resolve missing choices before requesting confirmation. |
| Confirm | Approve the order. | Clear approval of the current readback permits submission. An utterance containing a change, such as “yes, but no onions,” is an edit and requires a new readback and confirmation. |
| Complete | Receive an order number and simulated kitchen ticket; pay at the window. | Show the same items and total as the confirmed cart. Repeated approval or retry cannot create a second ticket for the same order. |

During ordering, the cart may show unresolved choices. A draft must not be presented as a submitted order, and its final total must not be claimed until required choices are resolved.

## 3. Menu and order rules — proposed

Use [the sample menu](demo-menu-proposal.md): 10 standalone products, three meal bundles, fictional USD prices, and free removal of listed ingredients. Prices are final displayed demo amounts, with no additional fees or tax calculation. These specific prices and currency have not been selected by the team yet.

- Quantity is a positive whole number. An ordinary singular request implies one; unclear quantities require clarification.
- Meals require a size and a drink. Meal size controls both fries and drink size. Ask only for choices that are missing.
- A meal's price already includes its components. Do not add component prices again.
- Removal of a listed ingredient is allowed and free. Paid extras, ingredient substitutions, and mixed-size meal components are excluded from this proposed menu.
- Keep differently configured copies distinguishable. “Two burgers, no onions on only one” must preserve one standard burger and one modified burger.
- Prices, availability, allowed options, and arithmetic come from the fixed menu. Spoken claims about discounts or prices do not change it.
- An unavailable or unrecognized request produces a clarification or an available alternative. Never silently substitute a different item.
- An ambiguous correction leaves the affected item unchanged until resolved; unrelated items remain intact.

## 4. Recovery and order lifecycle — proposed details

**Clarification and handoff.** An unsuccessful clarification is a targeted question followed by a reply that does not resolve the same issue. Reset the counter when resolved. After two failures, offer staff help; accepting it pauses the agent and shows the retained cart and unresolved issue. If declined, allow another clarification and offer again only after two further failures. An explicit request for a person bypasses the offer and pauses immediately. The screen clearly identifies the handoff as simulated; it does not claim that a real employee has joined. Handoff does not submit an unfinished order.

**Cancellation and restart.** A clear request to cancel the whole order ends it without a ticket. Removing one item affects only that item. “Start over” clears the active order. Starting the next customer's order begins with an empty cart and conversation.

**After completion.** Treat the submitted ticket as fixed. A requested change explains that staff would handle it at the window and shows a simulated handoff state with the existing ticket. Do not silently revise the ticket or submit another one.

**Service failure.** Show a recoverable error, retain the current cart in the open page, and offer retry or simulated handoff. Do not claim that the order was sent when delivery is uncertain. A retry uses the same order identity. Editing the order before retry requires renewed confirmation. Reload recovery is outside this first version's guarantee.

**Inactivity.** After 60 seconds with neither customer nor agent speaking, release the live audio session and offer restart, retaining the unsent cart in the open page. Never submit on silence.

## 5. What the demonstration shows — proposed

- A customer view with the fictional menu, current cart, prices, and visible listening/speaking/review/completed/handoff/error status.
- Start, end, and reset controls. No customer account is required.
- A simulated kitchen ticket after confirmation, containing the order number, item quantities, chosen options, modifiers, total, and pay-at-window instruction.
- A handoff view preserving the order and stating the unresolved issue or the customer's request for staff.

Different browser sessions must have independent carts. Reset removes the previous customer's conversation and cart from that session's view. Keep application conversation state in the current session; do not add accounts, permanent customer histories, or application-side raw-audio storage. Test recordings and diagnostic results may be retained separately for the team's controlled acceptance runs. Provider-side retention and logging need checking during technical design.

## 6. Acceptance contract — proposed measurements for confirmed goals

### Operating conditions

The first supported demo environment is desktop Chrome with a microphone and working internet. Mobile browsers and physical drive-thru hardware are outside the proposed acceptance matrix.

Define **moderate background noise** for this demo as continuous recorded road/engine or restaurant ambience mixed at a **+10 dB speech-to-noise power ratio**, calculated over speech-active portions. Measure this in the prepared audio at the application's audio-ingestion boundary, before speech-service preprocessing. Inject that audio where microphone frames normally enter the agent pipeline; do not infer the ratio from a speaker's volume setting. Exclude a second intelligible foreground speaker from this first test condition. Preserve the speech/noise recordings, mix levels, and input method so tests can be repeated.

Run the scenarios below in quiet and in the fixed moderate-noise condition. Use all three teammates' voices across the suite; each scenario should use the same speaker and utterances in its quiet/noisy pair. Exercise the entire downstream audio/agent pipeline, including spoken responses, order updates, and ticket creation. A transcription-only test is insufficient. Interruptions must occur during actual agent playback. Also perform one live browser-microphone smoke test per teammate with background ambience; record device, browser, and microphone setup. These three live checks cover physical capture and are additional to the 16 controlled runs; they do not establish a measured acoustic SNR.

### Required voice scenarios

| Test | Customer behavior | Pass condition |
| --- | --- | --- |
| V1 | Order standalone items with a size and an ingredient removal. | Correct items, quantities, options, arithmetic, final readback, confirmation, and one ticket. |
| V2 | Order a meal while omitting size and drink. | Ask only for missing choices; retain the selected main and finish with the chosen meal. |
| V3 | Order two identical burgers and remove onions from only one. | Two distinguishable configurations; the other burger retains its normal recipe. |
| V4 | Replace a drink and remove a clearly referenced item. | Only the referenced lines change; the total and readback reflect the current cart. |
| V5 | Interrupt an acknowledgement with a quantity or modifier correction. | Agent playback stops, the correction is handled once, and unrelated choices remain intact. |
| V6 | Interrupt final readback to change the order. | The previous readback cannot authorize submission; the updated order is read back and confirmed. |
| V7 | Leave the same ambiguity unresolved after two targeted questions. | Offer handoff at the defined point; accepting it preserves the cart and creates no ticket. |
| V8 | Ask for a person while the agent is speaking, in both audio conditions. | Stop automated ordering promptly and enter simulated handoff with the current cart retained. |

**Minimum acceptance set:** eight scenarios in two audio conditions, totaling 16 runs. Each must pass its expected behavior. Every V1–V6 run ends in a correctly confirmed ticket matching the scripted customer's intended order. Handoff is a successful result only for V7/V8; using it in V1–V6 does not pass noisy ordering. Record failures and fixes, then rerun affected pairs. Report the final run results and earlier failures; do not present this small suite as proof of production accuracy.

### Correctness and responsiveness

- **Order integrity:** every submitted ticket exactly matches the scripted customer's intended order, the last confirmed cart, and the menu-derived total. Zero unintended substitutions, lost modifiers, unconfirmed submissions, or duplicate tickets in the acceptance suite.
- **Response target:** customer end-of-speech to the first audible task-relevant response has a median at most **2 seconds** and a 95th percentile at most **4 seconds**, measured separately in quiet and moderate noise. Filler used only to mask waiting does not count. This includes the entire speech recognition, response, and audio pipeline; STT latency alone does not satisfy it.
- **Interruption target:** agent playback stops within **500 ms of customer speech onset** in V5, V6, and V8, in both audio conditions.
- **Noise-only check:** ten seconds of the fixed background track without customer speech must not add items, confirm an order, or trigger a customer interruption.

The timing values above are review proposals and have not been benchmarked. Record all measured turns and actual timings. If the initial implementation misses a target, retain the failed result and make the shortfall explicit; do not silently relax a requirement.

### Additional functional checks

- Reject microphone access: explain the problem and allow retry; no fake listening state.
- Request an unavailable item: offer valid alternatives while keeping unrelated cart entries.
- Cancel, start over, and start a new customer: no accidental ticket or leftover customer state.
- Interrupt with “yes, but change the drink”: require confirmation of the revised order.
- Repeat confirmation and simulate a submission failure/retry: produce exactly one final ticket.
- Request an edit after completion: retain the original ticket and show the agreed staff-handoff behavior.
- Simulate a speech/service disconnect: retain the cart and show recovery options.
- Open two sessions: orders remain independent.

## 7. Scope boundaries and delivery

**Confirmed exclusions:** processing payments in the demo, real POS/kitchen integration, and physical drive-thru equipment.

**Proposed exclusions:** multilingual support, a real staff call, mobile-browser guarantees, customer accounts/history, admin dashboards, loyalty/coupons, sales analytics, personalized upselling, and a production reliability claim. These exclusions preserve time for the required voice behavior and acceptance tests.

Prepare the working URL, public repository with setup instructions, MP4 demo presentation, PDF slides, and submission metadata specified in the [event research](../research/2026-09-21-hackathon-requirements.md). The presentation should visibly demonstrate a successful noisy order, an interruption/correction, and the confirmed kitchen ticket. Keep enough time to test the deployed application before recording.

A provisional three-person split is: voice and order behavior; browser/cart/ticket experience; test scenarios and submission materials. Roles can overlap and should be assigned based on actual availability before making an implementation schedule.

## 8. Review items and next phase

The team has settled the main product scope. Review the proposed menu/currency, lifecycle details, desktop/session boundaries, noise definition, and quality thresholds as one package. Change any that do not match the intended demonstration.

After the product brief is agreed, evaluate the smallest technical stack that can meet it, check AssemblyAI access and complementary services, estimate usage costs, select an explicit spend limit, and create the implementation plan. There is currently no application code, performance evidence, selected stack, or authorized spending amount in this brief.
