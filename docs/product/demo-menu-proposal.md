# Fictional demo menu — proposal

Status: proposed, not yet accepted. The team agreed to about 10 items and 2–3 meal combos; the specific products, recipes, currency, and prices below are a concrete example for review.

All prices are invented **USD demo prices** and represent the final displayed amount. This proposal uses no additional tax, fees, discounts, or payment processing.

## Standalone products

Size variants count as one product. Meal combos below are bundles of these products rather than additional standalone products.

| Product | Price | Allowed free removals |
| --- | --- | --- |
| Classic Burger | $4.50 | Lettuce, onions, pickles, signature sauce |
| Cheeseburger | $5.00 | Cheese, onions, pickles, signature sauce |
| Crispy Chicken Burger | $5.50 | Lettuce, tomato, mayo |
| Veggie Burger | $5.00 | Lettuce, tomato, onions, signature sauce |
| Fries | Medium $2.50; large $3.25 | None |
| Six-Piece Chicken Nuggets | $4.00 | None |
| Cola | Medium $2.00; large $2.75 | None |
| Lemon-Lime Soda | Medium $2.00; large $2.75 | None |
| Iced Tea | Medium $2.00; large $2.75 | None |
| Apple Pie | $1.75 | None |

Each listed removable ingredient is present in that product's default recipe. Burgers, nuggets, and pie do not have size variants. Paid additions, ingredient substitutions, and custom nugget counts are outside this proposed menu.

## Meal combos

Every meal contains its named main, fries, and one of the three listed drinks. Meal size sets both fries and drink size.

| Meal | Medium | Large |
| --- | --- | --- |
| Classic Burger Meal | $8.00 | $9.00 |
| Crispy Chicken Meal | $9.00 | $10.00 |
| Nuggets Meal | $7.50 | $8.50 |

The bundle price includes the main, fries, and drink; component prices are not added again. Burger removals remain free in meals. Mixed fries/drink sizes and side substitutions are excluded from this proposal.

## Proposed ordering rules

- Require a positive whole-number quantity.
- If quantity is omitted, propose treating an ordinary singular request as one item; clarify an unclear quantity.
- Ask for an unspecified size on fries, drinks, and meals. Ask for a drink choice on meals. Do not ask again for choices the customer already supplied.
- Apply modifiers only to the specified product or meal main.
- Keep differently configured copies distinguishable in the visible cart and kitchen ticket. For example, two burgers with onions removed from only one have separate configurations.
- Derive prices and totals from this fixed menu. The customer or language model cannot redefine them by speaking a price.
- If a requested configuration is unavailable, preserve the rest of the cart and resolve the request before final confirmation.

Round 3 settled the policy of asking only for missing or ambiguous choices. The menu-specific defaults and pricing rules here remain proposed until reviewed with the consolidated requirements.

## Worked orders

### Order A — distinct meal configurations

| Line | Amount |
| --- | --- |
| 1 medium Classic Burger Meal, Cola, no onions on burger | $8.00 |
| 1 large Classic Burger Meal, Iced Tea, standard burger | $9.00 |
| 1 Apple Pie | $1.75 |
| **Total** | **$18.75** |

### Order B — quantity and standalone sides

| Line | Amount |
| --- | --- |
| 2 Crispy Chicken Burgers, no mayo on either | $11.00 |
| 1 large Fries | $3.25 |
| 1 medium Lemon-Lime Soda | $2.00 |
| **Total** | **$16.25** |

These examples specify expected menu arithmetic, not application test results. The application has not been implemented.
