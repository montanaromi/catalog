Every non-trivial implementation decision MUST be documented with rationale in a delivered decision log. A decision is non-trivial if a competent engineer could reasonably have chosen differently.

Deliver a decision log as a Markdown table: what was decided, what alternatives existed, why this choice was made, and what risks it carries. For migrations or refactors, include a bidirectional traceability matrix mapping source constructs to target implementations — 100% coverage, no gaps.

Any deviation from a literal or obvious interpretation of the requirements MUST have an explicit entry in the decision log. Unexplained deviations are treated as defects.

The decision log is the authoritative source of truth for "why" decisions. Inline code comments MAY summarize a decision but MUST NOT be the only place rationale is recorded.

Verification: the deliverable contains a decision log with columns (decision, alternatives, rationale, risks) populated for every non-trivial choice; no requirement deviation lacks a corresponding entry. Scope: all Blitzy code generation deliverables that involve implementation choices.
