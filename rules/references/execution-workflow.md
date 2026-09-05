---
trigger: model_decision
description: Load for multi-file, ambiguous, risky, data-affecting, API-affecting, externally mutating, blocked, or verification-heavy technical execution.
---
# Execution Workflow Rules

Use this workflow when coordination prevents missed dependencies or unsafe
sequencing. A focused change can proceed directly; a migration or public
contract change needs explicit phases, compatibility, and rollback reasoning.
Apply the global agent instructions' authorization and completion boundaries;
planning is not a separate approval gate for already authorized work.

## Workflow

1. **Understand**: inspect the applicable instructions, source of truth,
   contracts, relevant user diffs, consumers, and representative tests. Resolve
   discoverable facts before asking the user.
2. **Plan when needed**: identify the outcome, affected files, dependencies,
   verification, and any compatibility, migration, security, data, external
   state, or rollback concern. Keep the plan proportional to risk and update it
   when scope changes.
3. **Implement**: make cohesive edits that follow repository patterns. Avoid
   speculative abstractions and broad formatting; keep affected contracts,
   configuration, generated artifacts, tests, and user documentation aligned.
4. **Verify**: run the smallest check capable of falsifying the changed
   behavior, then broaden according to blast radius. Inspect the final diff for
   accidental scope, secrets, generated noise, and compatibility changes.

## Unresolved Decisions And Blockers

- Ask when an unresolved choice materially changes the requested outcome,
  compatibility, data safety, security, cost, or authorized external effects,
  and cannot be resolved from instructions, evidence, repository conventions,
  or a conservative reversible assumption.
- The existence of multiple reasonable implementations is not itself a blocker.
  Do not interrupt for optional preferences. Ask blocking questions promptly
  after relevant inspection, and continue independent authorized work.
- Exhaust safe, in-scope inspection and local alternatives before declaring a
  blocker. Never bypass approval, sandbox, credential, or environment
  boundaries with a workaround.
- If only part of the task is blocked, finish independently verifiable work and
  separate completed results from assumptions or unavailable evidence.
