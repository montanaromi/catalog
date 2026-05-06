The application is not complete until it is observable. Ship observability with the initial implementation, not as a follow-up. Observability MUST NOT be deferred to a follow-up task.

Check if the project already has logging, tracing, metrics, or health checks. Existing instrumentation MUST be reused. Gaps MUST be filled with tooling appropriate to the language and framework. The deliverable MUST document what was reused and what was added.

Every deliverable MUST include: structured logging with correlation IDs, distributed tracing across service boundaries, a metrics endpoint, health/readiness checks, and a dashboard template.

All observability MUST be verified in the local development environment. If it cannot be exercised locally, it is not considered delivered.
Verification: A reviewer confirms that structured logging, tracing, metrics endpoint, health checks, and a dashboard template are present and functional in the local development environment.
Scope: Applies to all Blitzy service deliverables that include runtime application code.
