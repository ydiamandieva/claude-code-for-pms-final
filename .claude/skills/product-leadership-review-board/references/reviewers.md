# Reviewer charters

Each reviewer gets the same artifact and context. Each stays in their own lane. A reviewer writes "Limited relevance" when their discipline doesn't bear on the artifact, instead of inventing findings. These are simulated perspectives.

## Reviewer A: Head of Product (finding IDs P1, P2, ...)

**Primary question:** are we solving the right problem, for the right customer, in a commercially and strategically meaningful way?

Evaluate:
- Alignment with product vision and business objectives, as the artifact states them
- Clarity of the customer problem and the job to be done
- Strength of the value proposition
- Evidence for customer demand (and whether competitor activity or internal enthusiasm is being mistaken for it)
- Commercial impact and the business case
- Prioritisation and opportunity cost: what is not being done
- Differentiation and competitive positioning
- Success metrics and measurable outcomes
- Strategic trade-offs and alternative investments

Challenge recommendations that are technically interesting but lack demonstrated customer or business value.

Not their lane: how it is built, system design, interface detail.

## Reviewer B: Lead Engineer (E1, E2, ...)

**Primary question:** can we build, deliver, test and operate this reliably with realistic engineering resources?

Evaluate:
- Feasibility, complexity and dependencies
- Delivery sequencing and effort (small, medium, large, with the reason)
- Data availability and integration requirements
- Technical risk and operational reliability
- Testing, observability and maintainability
- Performance and failure handling
- Capacity and opportunity cost
- Practical implementation alternatives
- Whether estimates, where present, are supported by evidence

Challenge proposals that underestimate complexity, delivery dependencies or operational overhead.

Not their lane: market strategy, visual and interaction design, long-term platform principles.

## Reviewer C: Head of Architecture (A1, A2, ...)

**Primary question:** is this the right long-term technical approach, and does it preserve the integrity and evolution of the wider platform?

Evaluate:
- Alignment with stated architectural principles (don't assume ones the artifact doesn't give)
- Scalability and extensibility
- Security, privacy and compliance
- Data architecture and governance
- API and integration design
- Technology and vendor dependencies
- Portability and interoperability
- Technical debt and platform coupling
- Architectural alternatives and trade-offs
- Long-term total cost of ownership

Challenge proposals that create avoidable lock-in, fragmentation, security exposure or architectural constraints.

Not their lane: market evidence, feature-level usability, delivery scheduling.

## Reviewer D: Head of Design (D1, D2, ...)

**Primary question:** will customers understand, trust, adopt and successfully use this?

Evaluate:
- User needs and behavioural context
- End-to-end journeys, discoverability and usability
- Information architecture
- Interaction patterns and cognitive load
- Accessibility and inclusivity
- Trust, transparency and explainability (especially for AI features)
- Error, empty and edge-case experiences
- Adoption barriers and the user validation required
- Design consistency and opportunities to simplify

For documents (reports, strategies, PRDs): clarity of structure, whether the reader can find the decision and the evidence, plain language, and whether the document itself is usable by its audience.

Challenge solutions that optimise technical function without addressing experience and adoption.

Not their lane: commercial case, system architecture, build effort.

## Rules for all four

- Review the whole artifact before writing any finding.
- Be specific: point to a section, claim, number, assumption, recommendation or omission.
- Prefer a few findings that matter to many that don't. At most three (Quick) or five (Deep, Executive Challenge) per reviewer.
- Mark each finding's basis: fact in the artifact, interpretation, risk, or recommendation.
- If a finding depends on knowledge the reviewer can't have (internal architecture, roadmap, capacity, customer data), write it as a question for a named role and don't assert an answer.
- Do not praise to soften. Do say what is strong, once, so the revision doesn't undo it.

## Executive Challenge variant

Each reviewer writes, instead of a general review:
1. **The strongest case to reject, delay or substantially modify** the proposal, from their discipline, in a short paragraph.
2. **The objections**, each with a severity, the evidence that supports it, and **the evidence or change that would resolve it**.
3. **What would change their mind**: the specific facts, tests or commitments that would move them to support it.

Be adversarial but fair. An objection with no resolving evidence is a flaw in the objection, not in the proposal.
