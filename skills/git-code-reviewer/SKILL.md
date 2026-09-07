---
name: git-code-reviewer
description: Review the complete current branch against a user-specified base before opening a PR or MR for a Python backend service. Invoke explicitly with $git-code-reviewer for pre-PR/MR whole-branch review; do not use for workspace changes, individual commits or diffs, localized implementation checks, debugging, or ordinary requests to inspect code.
---

# Code Review

Turn a change set into evidence-backed findings. Prioritize correctness and operational risk over style.

## Scope Gate

- This skill is only for a pre-PR/MR review of the complete current branch. Ordinary workspace, commit, diff, debugging, design-conformance, and localized code-review requests must use normal code inspection instead of this workflow.
- Require a base branch or base ref explicitly provided by the user, including an earlier instruction that remains applicable to this review. If missing, ask `基础分支是什么？`; do not resolve the comparison range, fetch, or begin branch-delta review. Do not infer the base from PR metadata, repository defaults, the current branch, or local context.
- Independent read-only preparation, such as locating repository instructions and inspecting workspace status, may continue while the base is missing. Once prerequisites are satisfied, complete the authorized review and report without asking whether to proceed.
- After receiving the base, load and follow [../_shared/git-remote-base-resolution.md](../_shared/git-remote-base-resolution.md) for ref resolution and freshness.
- Review the committed branch delta from the merge base through the current `HEAD`. Report relevant staged, unstaged, and untracked workspace changes separately; do not silently include them in the branch artifact.
- Keep evidence tied to the reviewed revision: when workspace changes affect inspected files or validation inputs, use committed content for branch conclusions and state which revision each check actually validates. Do not attribute workspace-only fixes or passing tests to `HEAD`. Preserve user changes; if committed-state validation is unavailable, report that limitation.

## Workflow

### 1. Understand the Change

- Read the diff summary, changed implementation, and relevant runtime path before judging intent.
- Treat PR or MR titles, descriptions, and comments as context; base findings on the diff and runtime evidence.
- Inspect callers, callees, nearest tests, configuration, schemas, and analogous patterns only when they affect a conclusion.
- Trace relevant boundaries such as request handling, service logic, persistence, async work, external calls, and configuration.
- For derived state, identify the authoritative state, synchronization path, cleanup path, and compatibility surface.

### 2. Load Relevant Review Guidance

- Load [references/review-risk-checklist.md](./references/review-risk-checklist.md) for the cross-cutting review pass.
- Load only the references matching the changed behavior:
  - Python backend, FastAPI, Pydantic, SQLAlchemy, Alembic, or workers → [references/python-backend-review-checklist.md](./references/python-backend-review-checklist.md)
  - Persistence, caches, indexes, status transitions, or multi-step workflows → [references/stateful-systems-review-checklist.md](./references/stateful-systems-review-checklist.md)
  - Redis or cache-backed data access → [references/redis-cache-review-checklist.md](./references/redis-cache-review-checklist.md)
  - Prompts, tools, retrieval, embeddings, streaming, or agents → [references/llm-rag-review-checklist.md](./references/llm-rag-review-checklist.md)

### 3. Validate Conclusions

- Treat inspected code, configuration, tests, schemas, and command output as evidence. Keep inference and unverified assumptions separate from confirmed facts.
- For high-risk stateful changes, challenge the conclusions with at least two relevant concrete counterexamples such as partial retry, race, mixed-version rollout, or replay after cleanup. Static reasoning is acceptable; distinguish it from executed tests.
- Run focused, non-destructive checks when they can materially confirm or falsify a concern, and preserve required repository checks. Match validation to impact and risk. Do not add implementation-mirroring tests for low-impact, reversible changes. After relevant checks pass, broaden or repeat validation only for new changes, failures, or unresolved concerns. Report observed outcomes and material verification gaps.
- Before finishing, check the changed path for dead parameters, unreachable branches, and obsolete wrappers.

### 4. Report

- Load and follow [references/review-output-template.md](./references/review-output-template.md).
- Report only concrete, actionable findings, ordered by user impact. Combine symptoms that share one root cause.
- Report a missing test as a finding only when it hides a concrete contract, migration, security, concurrency, or failure-path risk.
- Review requests authorize inspection and findings. Patch code only when the user requests implementation. Prepare review comments when requested, and publish them only after satisfying applicable explicit approval requirements. Reuse approval that remains valid for the same target, content, and scope.
