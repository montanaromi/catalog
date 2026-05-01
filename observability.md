The application is not complete until it is observable. Ship observability with the initial implementation, not as a follow-up.

Check if the project already has logging, tracing, metrics, or health checks. Use what exists. Fill gaps with tooling appropriate to the language and framework. Document what you reused and what you added.

Every deliverable MUST include: structured logging with correlation IDs, distributed tracing across service boundaries, a metrics endpoint, health/readiness checks, and a dashboard template.

Verify all observability works in the local development environment. If you cannot exercise it locally, it is not delivered.
