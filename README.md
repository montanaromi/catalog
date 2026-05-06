<!-- Project header -->
<div align="center">
  <h1>Blitzy Rule Catalog</h1>
  <p>Governance rules and prompts for Blitzy's code generation agents</p>
  <a href="https://github.com/montanaromi/catalog"><strong>Browse the catalog</strong></a>
  &middot;
  <a href="https://github.com/montanaromi/catalog/issues/new?labels=bug">Report Bug</a>
  &middot;
  <a href="https://github.com/montanaromi/catalog/issues/new?labels=enhancement">Request Feature</a>
</div>

---

<details>
  <summary>Table of Contents</summary>
  <ol>
    <li><a href="#about">About</a></li>
    <li><a href="#catalog-contents">Catalog Contents</a></li>
    <li><a href="#rule-format">Rule Format</a></li>
    <li><a href="#how-rules-are-consumed">How Rules Are Consumed</a></li>
    <li><a href="#tiered-pairs">Tiered Pairs</a></li>
    <li><a href="#adding-a-rule">Adding a Rule</a></li>
  </ol>
</details>

---

## About

A flat collection of 20 Markdown files that define enforceable constraints, process specifications, and prompts consumed by Blitzy's code generation pipeline. Each rule gates what agents produce — covering security, benchmarking, observability, code review, explainability, writing quality, and presentation standards.

Rules are embedded into Blitzy prompts via the `/z` skill (Section 6: RULES) and validated with `/king` and `/chuck`.

## Catalog Contents

### Rules

| File | Domain | Summary |
|------|--------|---------|
| `architecture.md` | Documentation | Visual documentation via Mermaid diagrams with before/after views |
| `arnold.md` | Performance | Targeted performance enhancement benchmarking — strict improvement, ≥30 samples |
| `cross-fit.md` | Performance | General code modification benchmarking — 10% degradation tolerance |
| `explainability.md` | Documentation | Report-driven decision log as Markdown table |
| `document-code-explainability.md` | Documentation | Inline code documentation — docstrings and "why" comments |
| `GxPeter.md` | Compliance | GxP-regulated analytical deliverables (ALCOA+, V-Model, GAMP 5) |
| `knight.md` | Security | Security assessment execution — 8-tool sequence, localhost only |
| `observability.md` | Operations | Structured logging, tracing, metrics, health checks, dashboard template |
| `rob.md` | Process | Multi-phase isolated code review for Agent Action Plans |
| `tldr.md` | Presentation | Executive summary as self-contained reveal.js HTML (Blitzy brand) |
| `workflow-completeness.md` | Quality | Complete workflows with no dead ends or swallowed errors |
| `prose.md` | Writing | Writing clarity validation — Vonnegut (prose) and Asimov (technical) principles |
| `analyze-performance-impact.md` | Performance | Inline complexity annotations and efficient patterns |
| `assess-change-risks.md` | Risk | Risk documentation for public contract and schema changes |
| `catalog-security-vulnerabilities.md` | Security | Secure coding practices and OWASP prevention |
| `document-api-consumer-paths.md` | Documentation | API endpoint contract and data flow documentation |
| `enforce-code-style-patterns.md` | Quality | Match existing codebase conventions |
| `preserve-backward-compatibility.md` | Compatibility | Backward-compatible changes with deprecation paths |
| `require-test-coverage.md` | Testing | Test coverage contract — test double taxonomy (stubs, mocks, fakes), seed data, tiered coverage, environment parity |

### Prompts

| File | Summary |
|------|---------|
| `snoopy.md` | Development acceleration measurement — 11 metrics, before/after multipliers |

## Rule Format

Two conventions exist in this catalog:

**Native rules** use plain Markdown with RFC 2119 severity keywords (MUST, MUST NOT, SHOULD, SHOULD NOT), a Verification sentence, and a Scope sentence. Example: `architecture.md`.

**Archie-docs templates** use MDX frontmatter (`title`, `description`, `icon`) with a "Rule Definition" section containing the constraint text inside a code fence. Example: `require-test-coverage.md`.

Both formats are validated against the `/king` Phase 3 quality gate:

| Check | Pass Condition |
|-------|---------------|
| Severity keyword | Contains MUST, MUST NOT, SHOULD, or SHOULD NOT |
| Verifiability | Contains a testable assertion (numeric, structural, or behavioral) |
| Scope stated | Names what the rule applies to |
| Length | 3–5 sentences preferred; longer only if inline enumeration requires it |
| Unified concern | Addresses one domain or constraint category |

## How Rules Are Consumed

```
Rule file (.md)
  → embedded in Blitzy prompt via /z (Section 6: RULES)
  → validated with /chuck (prompt quality) and /king (rule quality)
  → consumed by code generation agent during execution
  → agent output constrained by rule requirements
  → rob.md review process validates compliance
```

## Tiered Pairs

Some domains are covered by two rules at different scopes. Each pair cross-references the other in its Scope sentence.

| Domain | Targeted / Strict | General / Broad |
|--------|-------------------|-----------------|
| **Benchmarking** | `arnold.md` — performance runs, strict improvement | `cross-fit.md` — code changes, 10% tolerance |
| **Explainability** | `explainability.md` — decision log report | `document-code-explainability.md` — inline comments |
| **Security** | `knight.md` — tool-based assessment | `catalog-security-vulnerabilities.md` — coding practices |

## Adding a Rule

1. Write the rule following the native format (MUST/MUST NOT, Verification, Scope)
2. Validate with `/king` — all Phase 3 checks must pass
3. Check for overlap with existing rules — merge or define precedence if needed
4. Commit with `/commit`
