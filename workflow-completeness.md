All generated code MUST produce complete workflows with no dead ends, no swallowed errors, and no undocumented behavior — from backend handlers through user-facing flows.

Completeness: every user-facing route, endpoint, or UI action MUST have a defined entry point and at least one success exit point. Every decision branch (conditional paths based on user input, permissions, feature flags, or state) MUST lead to a handled outcome. Every route or endpoint MUST have a full implementation — no stubs, no empty bodies, no TODO placeholders. Multi-step workflows MUST handle partial completion with user feedback and a recovery path.

Error Handling: every try/catch block MUST either log the error, notify the user, or re-throw — never silently discard. External service calls MUST include a timeout and handle timeout/failure with a fallback or user-facing error message. Multi-step operations MUST handle partial failure by rolling back prior steps or leaving the system in a documented, recoverable state. Concurrent operations MUST account for race conditions with appropriate locking or conflict resolution.

Documentation: complex branching logic MUST include an inline comment explaining the intent of each branch. Integration points with external services MUST document expected error responses and handling. Configuration-driven behavior MUST document valid values and defaults at the configuration site.

When modifying an existing workflow, all existing entry points, branches, and exit paths MUST still function. Shared workflow steps (authentication, authorization, logging) MUST be implemented consistently across all journeys that use them.

Verification: every generated route connects to a complete handler returning meaningful responses for success and error; every catch block handles the error visibly; every external call has a timeout; every multi-step flow handles failure at each step; no dead-end paths or unhandled states exist. Scope: all Blitzy code generation outputs that produce user-facing features or backend handlers.
