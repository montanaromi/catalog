Every new or modified function, class, and module entry point MUST include a docstring in the language's standard format (JSDoc, Javadoc, Python docstrings, XML comments) specifying purpose, parameters (name, type, description), return values, and exceptions. Trivial accessors may use a single-line docstring.

Every non-obvious implementation decision MUST have an inline comment adjacent to the code explaining WHY that approach was chosen, using at least one of: alternatives considered, refactoring rationale, assumptions about external contracts, or trade-offs accepted. Comments MUST NOT restate what the code does. Vague rationales ("this is better", "for performance") without specific justification are prohibited.

For decisions significant enough to warrant a deliverable-level record, the report-driven decision log (see explainability.md) is the authoritative source — inline comments MAY summarize but SHOULD reference the decision log entry.

Verification: every new or modified function has a docstring with purpose, parameters, and return values; every non-obvious implementation choice has an adjacent inline comment with at least one "why" category. Scope: all Blitzy code generation outputs producing executable application code.
