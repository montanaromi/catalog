---
title: "Require Test Coverage"
description: "Contract for test generation ensuring correct use of mocks, stubs, fakes, and seed data across unit and integration tiers"
icon: "vial-circle-check"
---

## When to Use

Add this rule to any Blitzy project to ensure generated tests form a complete, executable test suite. When a project already has tests, the agent updates the existing suite to conform to this contract rather than generating a parallel suite.

This rule governs both test purity (no reimplemented business logic) and test completeness (seed data, environment readiness, state isolation, and tiered coverage).

## Rule Definition

**Name** — Require Test Coverage

**Description** — paste this into the rule description field on the platform:

```
Generate or update test coverage by importing and testing EXISTING production code. Tests MUST invoke real production functions, use the correct test double strategy, declare data dependencies, and run identically in Blitzy's autonomous pipeline and local developer environments.

─────────────────────────────────────────────
TEST DOUBLE TAXONOMY
─────────────────────────────────────────────

Every test double MUST be identified by its correct type. MUST NOT use "mock" as a generic term.

Stub — Returns predetermined data. No behavior verification. Use when a dependency MUST return a value but the test does not care how it was called.
  Example: A stub HTTP client that always returns { "status": 200 }.

Mock — Records calls and verifies interactions (call count, argument values, call order). Use when the test MUST verify that a dependency was called correctly.
  Example: A mock email service that asserts send() was called once with the correct recipient.

Fake — A lightweight working implementation that behaves realistically but is unsuitable for production. Use when the test needs realistic behavior without external infrastructure.
  Example: An in-memory repository that supports CRUD operations with a dictionary instead of a real database.

Seed Data — Predetermined, representative data loaded into the test environment before test execution. Use to establish a known database state or provide realistic input data.
  Example: A seed script or fixture file that inserts known users, products, and orders before integration tests run.

Rules for applying test doubles:
- MUST name every test double explicitly as stub, mock, or fake in test code (variable names, docstrings, or comments)
- MUST NOT mock the unit under test — only its dependencies
- SHOULD NOT use a mock when a stub suffices (avoid over-specification)
- SHOULD prefer fakes over mocks for complex dependencies with multiple interactions
- MUST use seed data for any test that validates behavior dependent on database state

─────────────────────────────────────────────
TEST TIERS
─────────────────────────────────────────────

Every generated test MUST be classified into exactly one tier. Tier determines the test double strategy and environment requirements.

Unit Tests:
- MUST isolate a single function, method, or class
- MUST replace external dependencies (APIs, databases, file systems, queues) with stubs, mocks, or fakes
- MUST use factories or builders to generate input data — MUST NOT use hardcoded magic values as the sole data source
- MUST NOT perform I/O, network calls, or database connections
- SHOULD complete in under 100ms per test

Integration Tests:
- MUST test interactions between two or more components or between a component and real infrastructure
- MUST use a real database (containerized via docker-compose/testcontainers, or transaction-isolated)
- MUST apply migrations before test execution
- MUST load seed data from fixture files or seed scripts — MUST NOT rely on data left by other tests
- SHOULD mock only truly external third-party services (payment gateways, email providers, external APIs)
- MUST NOT mock the database — the database is the system under test

─────────────────────────────────────────────
SEED DATA AND FIXTURE REQUIREMENTS
─────────────────────────────────────────────

- Every test suite that touches persistent state MUST declare its seed data strategy: factory functions, fixture files (JSON, YAML, SQL), or a seed script
- Seed data MUST be representative of production data shapes, including required relationships and constraints (foreign keys, unique indexes, non-null fields)
- Seed data MUST be committed alongside test files so that any developer or pipeline can reproduce the test environment
- Factories MUST produce unique values per invocation (use sequences, UUIDs, or faker) to avoid collision between tests
- Hardcoded IDs, emails, or names are permitted ONLY when a specific value is the thing being tested (e.g., testing duplicate-email rejection)

─────────────────────────────────────────────
STATE ISOLATION AND ENVIRONMENT
─────────────────────────────────────────────

- Every test that mutates shared state MUST clean up after itself via transaction rollback, truncation, or per-test database provisioning
- Tests MUST NOT depend on execution order — each test MUST set up its own preconditions
- Connection strings, service URLs, and file paths MUST read from environment variables or a test config file with sensible local defaults
- A test environment setup section (README, Makefile target, docker-compose.test.yml, or equivalent) MUST be generated alongside the test suite so that local execution requires at most one command (e.g., `make test`, `npm test`, `docker compose up --abort-on-container-exit`)
- Migrations MUST run as a precondition to integration tests, either in test setup or in the environment bootstrap

─────────────────────────────────────────────
DETERMINISTIC ASSERTIONS
─────────────────────────────────────────────

- MUST NOT assert on auto-increment IDs, timestamps, or random values unless the source of randomness is controlled (seeded RNG, frozen clock)
- MUST assert on stable identifiers: natural keys, slugs, or values the test itself created
- For time-dependent behavior, MUST inject a clock or freeze time rather than asserting on datetime.now()

─────────────────────────────────────────────
TEST PURITY
─────────────────────────────────────────────

- MUST import production functions, methods, and classes directly from source modules
- Test files MUST contain only: imports, test doubles declaration, setup/fixtures, seed data loading, function invocation, and assertions
- MUST NOT recreate algorithms, calculations, or business logic from production code inside test files
- MUST NOT copy or paraphrase function logic into test files
- MUST NOT inline expected output derived from reimplemented logic — call the production function

─────────────────────────────────────────────
MINIMUM COVERAGE EXPECTATIONS
─────────────────────────────────────────────

For every public function or endpoint under test, MUST generate at minimum:
- One happy-path test with representative input
- One error/exception test (invalid input, missing dependency, constraint violation)
- One boundary-condition test (empty input, maximum length, zero quantity, null/undefined where applicable)

─────────────────────────────────────────────
VALIDATION GATES
─────────────────────────────────────────────

Gate 1 — Purity: Flag any test file where business logic appears outside of imports, setup, invocation, or assertions. A test that computes expected values by reimplementing production algorithms instead of calling the production function MUST fail review.

Gate 2 — Completeness: Flag any test suite that lacks:
  - A declared seed data strategy (factories, fixtures, or seed script)
  - Environment configuration (env vars, config file, or docker-compose for integration tests)
  - At least one error-case and one boundary-case test per public function or endpoint

Gate 3 — Double Correctness: Flag any test that:
  - Uses "mock" as a variable name for a test double that is actually a stub or fake
  - Mocks the unit under test rather than its dependencies
  - Mocks the database in an integration test

Verification: A test suite passes this rule when all three gates report zero flags. Scope: Applies to all test generation and test update operations in Blitzy projects.
```

## How It Works

1. Add this rule to your Blitzy project on the platform
2. When the project already has a test suite, the agent updates it to conform — it does not generate a parallel suite
3. Constraints are enforced during test generation across all three validation gates
4. Generated tests include the test code, seed data artifacts (fixtures/factories/seed scripts), and environment setup (docker-compose, Makefile targets, or equivalent)
5. The same test suite runs in Blitzy's autonomous pipeline and on a developer's local machine with identical results
6. Code review validates purity, completeness, and correct test double usage
