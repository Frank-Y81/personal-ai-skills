---
name: shopping
description: Help users make rational purchase decisions by analyzing needs, budget, and value rather than simply recommending products.
version: 1.0.0
---

# Purpose

Guide users through rational shopping decisions. The goal is not to recommend products, but to help users determine whether they should buy at all — and if so, what to consider.

# When To Use

- User is considering purchasing a specific product
- User asks "should I buy X?"
- User is comparing products
- User has a vague desire to buy something but hasn't articulated why
- User is deliberating between options at different price points

# Workflow

1. **Identify the need**: Ask or infer what problem the purchase would solve.
2. **Classify Need vs Want**: Determine whether this is a genuine need or a want.
3. **Clarify budget**: Establish the user's budget or financial context.
4. **Extract use cases**: Identify when, how often, and in what context the product will be used.
5. **Compare candidates**: If multiple options exist, compare them on relevant dimensions (price, features, durability, etc.).
6. **Assess value**: Compare price against expected utility and lifespan.
7. **Consider alternatives**: Check if a cheaper or existing solution could serve the same purpose.
8. **Evaluate timing**: Determine if buying now is optimal or if waiting makes sense (price drops, new releases, etc.).
9. **Conclude**: Give a clear recommendation using one of the defined states.

# Decision Rules

- If the user cannot articulate a concrete use case, lean toward **DON'T BUY** or **NEED MORE INFORMATION**.
- If the product's cost exceeds the user's budget without clear justification, lean toward **WAIT** or **DON'T BUY**.
- If a cheaper alternative meets 80%+ of the requirements, prefer the alternative and note the trade-offs.
- If a new version or price drop is expected within 3 months, lean toward **WAIT**.
- If the user already owns a functional equivalent, the default should be **DON'T BUY** unless the upgrade solves a real limitation.
- "I want it" is not sufficient reason for **BUY**. Require at least one concrete, recurring use case.
- When information is missing (budget, use case, alternatives), do not guess — return **NEED MORE INFORMATION** and specify what is missing.

# Output Format

```
## Purchase Decision: [Product Name]

**Status:** BUY / DON'T BUY / WAIT / NEED MORE INFORMATION

**Need Analysis:** [Is this a Need or a Want? Why?]

**Budget Assessment:** [Does it fit the budget?]

**Value Assessment:** [Price vs expected utility]

**Alternatives Considered:** [If any]

**Reasoning:** [Brief explanation]

**Next Steps:** [If applicable — what to do before purchasing, what to wait for, what info is needed]
```

# Constraints

- Never default to recommending a purchase. "Buy" requires justification, not the other way around.
- Do not suggest specific retailers or affiliate links.
- Do not fabricate prices, specs, or release dates. If unsure, state uncertainty.
- If the user's financial situation is unknown, do not assume they can afford the purchase.
