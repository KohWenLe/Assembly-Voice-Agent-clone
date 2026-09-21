# Restaurant drive-thru ordering

The product is an English-language browser demonstration of a restaurant drive-thru voice agent. It uses a fictional fast-food menu, a visible cart, and a simulated kitchen ticket, with order accuracy and smooth customer experience as the primary goals.

Interruptions, corrections, and moderate background noise are required operating conditions for the demo. The exact noise test definition remains proposed in the requirements brief.

## Language

**Customer**:
The person speaking to the agent to place a food order in the browser demonstration.

**Menu**:
The fictional fast-food items and options offered in the demonstration. Its exact contents and prices remain undecided.

**Meal combo**:
A menu offering that combines items into a meal with selectable sizes and drink choices. The specific bundles and pricing remain undecided.

**Modifier**:
A requested change to a menu item, such as removing onions. The set of allowed changes for each item remains undecided.

**Cart**:
The customer's current order details displayed during the conversation.

**Kitchen ticket**:
The simulated restaurant-facing record produced after the customer confirms the total. It accompanies an order number; payment happens at the window, outside the demonstration.
_Avoid_: Payment receipt, invoice.

**Order number**:
The identifier shown to the customer when the confirmed order produces a simulated kitchen ticket. Its display format remains undecided.

**Clarification**:
A focused question resolving a missing or ambiguous order choice. Two unsuccessful attempts on the same issue trigger an offer of simulated staff handoff.

**Staff handoff**:
A simulated transfer of the ordering interaction to restaurant staff with the current cart retained. It occurs immediately on a customer's explicit request; the prototype does not connect a real employee.

**Interruption**:
Customer speech that takes over while the agent is speaking, including an addition or correction to the order.

Detailed decisions, proposed behavior, and unanswered questions are recorded in [the requirements document](docs/product/requirements.md). The demonstration does not process payments or connect to a real restaurant system.
