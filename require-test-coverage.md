---
title: "Require Test Coverage"
description: "Ensure tests import and invoke production code rather than reimplementing business logic"
icon: "vial-circle-check"
---

## When to Use

Add this when requesting test generation or adding test coverage to ensure tests import and invoke real production functions instead of reimplementing business logic.

## Rule Definition

**Name** — Require Test Coverage

**Description** — paste this into the rule description field on the platform:

```
Generate test coverage by importing and testing EXISTING production code. Tests must invoke real production functions, not reimplement business logic.

Requirements:
- Import production functions, methods, and classes directly from source modules
- Test structure must contain only: imports, test setup/fixtures, function invocation, and assertions
- Mock or stub ONLY external dependencies (APIs, databases, file systems, network services)
- Test assertions must validate return values and side effects of actual production code execution
- Do not recreate algorithms, calculations, or business logic from production code inside test files

Forbidden Patterns:
- Copying or paraphrasing function logic into test files
- Creating test-local implementations that duplicate production behavior
- Mocking the internal function or method under test
- Inlining expected output derived from reimplemented logic instead of calling the production function

Validation Gate: Flag any test file where business logic appears outside of imports, setup, invocation, or assertions. A test that computes expected values by reimplementing production algorithms instead of calling the production function fails review.
```

## How It Works

1. Add this rule to your project on the platform
2. Constraints are enforced during test generation
3. Generated tests import real production functions and test actual behavior
4. Tests contain only imports, setup, invocation, and assertions
5. Code review validates that test files do not contain reimplemented business logic
