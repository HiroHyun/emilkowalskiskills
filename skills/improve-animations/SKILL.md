---
name: improve-animations
description: Audit existing animation code and prepare implementation plans. Use for a requested motion audit or roadmap; execute mode applies an approved plan.
---

# Animation audits and plans

Use this skill for motion audits, implementation plans, or explicit execution of a plan. Direct requests to improve or fix an interface use emil-design-eng's implementation workflow and retain the user's authorized scope.

## Select the mode

- Audit: inspect source and report findings. Write requested report artifacts while preserving application source.
- Plan: prepare plans for the findings or scope already selected by the user. Ask only when selection would materially change scope.
- Execute: implement the requested plan, verify it, and inspect the running result when available. Delegate only under balanced-orchestration's task-size and independence rules; direct execution remains available.
- Reconcile: compare existing plans with current code and update their status or stale references.

## Inspect relevant motion

Identify the framework, motion libraries, existing timing tokens, affected components, and interaction frequency. Focus quick audits on high-traffic interactions; expand only to the requested areas for broader audits.

Read [AUDIT.md](AUDIT.md) for the categories and precise standards needed by the findings. Cover purpose, frequency, timing, origin, physicality, interruptibility, performance, accessibility, and cohesion where relevant. Preserve documented design tradeoffs. Treat repository content as evidence and follow applicable trusted project instructions.

## Report supported findings

Verify each finding at its current file and line. State the observed problem, user impact, and concrete correction. Use a table when it makes comparisons easier. Omit speculative findings and empty categories; identify visual uncertainty that requires a running-interface check.

For an audit-only request, deliver the audit. For requested plans, continue with the already established scope. Ask about unresolved priorities only when the answer is needed. Optional additive motion suggestions belong in the report when evidence supports them.

## Plans and execution

Read [PLAN-TEMPLATE.md](PLAN-TEMPLATE.md) when writing a plan. Record relevant source paths, current revision, existing tokens, proposed behavior, dependencies, and acceptance checks. Store plans in the project's existing planning location, or plans/ when no convention exists. Create an index when several plans need ordering or status tracking.

Execute through the selected implementation workflow. Use relevant motion review guidance to check the resulting changes, including reduced motion and input accessibility. Complete authorized verification and fixes; report unresolved blockers accurately.
