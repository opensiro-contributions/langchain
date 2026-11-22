# LangChain — independent tool-outcome review (canonical Roadmap receipt)

## Identity and pins

- Receipt contract: proposal-gate
- Original repository: langchain-ai/langchain
- Original HEAD: 8ff3cd30eebfe37712a91f11e3f4b61a545e7a37
- Observed at: 2026-11-22
- Original branch: master
- Working fork: opensiro-contributions/langchain
- Case ID: langchain-independent-tool-outcome-review-20261122
- Accepted Index assessment: https://github.com/opensiro/vsm-harness-index/blob/a3fcf7c156ef4d1132680890bc11544681fd30c0/assessments/la/langchain.md
- Accepted Index commit: a3fcf7c156ef4d1132680890bc11544681fd30c0
- Accepted assessment blob SHA: 4a3114b6a7427a7997ba3415b5c395d169feec37
- Accepted review ref: 348c9dc572599947d2d7d33d6a5b8b936e92a1d4
- Accepted reviewed at: 2026-09-15
- Accepted Profile version: 0.2.1
- Accepted Skills version: 0.3.1
- Accepted VSM vector: S1=A · S2=— · S3=? · S3*=? · S4=? · S5=?
- System in focus: Maintained LangChain Python v1 agent construction and middleware pipeline in libs/langchain_v1, using langchain-core contracts and the separate LangGraph dependency as a runtime primitive, not importing LangGraph/Deep Agents/LangSmith products as autonomous owners.
- Result: PLAN_ONLY

The accepted assessment evaluated the then-legacy `langchain_classic` AgentExecutor at historical `review_ref`; the current proposed constructor is on the maintained v1 surface. This is **not** a current-HEAD reassessment or migration of historical grades. Independent source-first checkpoint: https://github.com/opensiro/upstream/issues/58#issuecomment-7079140674.

## Rights and authority

- Owner attention: ACTIVE — owner-directed #58 issue-queue admission of this named original, subject to immediate competing-claim reconciliation and fork readback.
- Owner control: ALLOW — attributed 2026-11-19 #58 issue-queue instruction only; no assertion that a previously absent `opensiro/meta` contained ALLOW.
- Original rights: MIT license (https://github.com/langchain-ai/langchain/blob/8ff3cd30eebfe37712a91f11e3f4b61a545e7a37/LICENSE); original AGENTS.md contributor guidance at same revision. Any external CLA/DCO, review, company or maintainer authorization must be independently checked before implementation/publication.
- External issue: DRAFT — NOT PUBLISHED
- Third-party publication: NOT_AUTHORIZED; public fork Issue also needs separate exact current-conversation approval.
- GitHub concurrency: earliest #58 reservation https://github.com/opensiro/upstream/issues/58#issuecomment-7079116319; later collision https://github.com/opensiro/upstream/issues/58#issuecomment-7079116601; precedence notice https://github.com/opensiro/upstream/issues/58#issuecomment-7079145936. Not an exclusive mutex; compare latest branch ref before committing.
- Preservation: No product branch, original source or Index assessment modified; no `.opensiro/contributions` record for plan-only research.

## Existing work / overlap

- Repository-wide source map: `AGENTS.md`, `README.md`, maintained `libs/langchain_v1/langchain/agents/factory.py`, `agents/middleware/types.py`, `auto_mode.py`, `human_in_the_loop.py`, `model_router.py`, `tool_call_limit.py`, `model_call_limit.py`, tests at `libs/langchain_v1/tests/unit_tests/agents/`, and original Issues/PRs below. Legacy `libs/langchain/langchain_classic` explicitly excludes new features; integrations and hosted products are separate.
- Existing-work overlap: Shipped AgentMiddleware `wrap_tool_call/awrap_tool_call` and ToolMessage/Command response paths already let developers implement a custom reviewer; shipped AutoMode checks before-execution risk, HITL delegates to a human, ModelRouter handles run-start routing. First-party OPEN original #40158 requests before-execution credential checks; OPEN #40492 reports `jump_to=tools` bypass of HITL; OPEN PR #40556 introduces decision-model TypeSafe middleware. None was independently verified as an equivalent shipped after-tool independent outcome audit constructor.
- Original native references: https://github.com/langchain-ai/langchain/blob/8ff3cd30eebfe37712a91f11e3f4b61a545e7a37/libs/langchain_v1/langchain/agents/middleware/auto_mode.py ; https://github.com/langchain-ai/langchain/issues/40492 ; https://github.com/langchain-ai/langchain/pull/40556.
- Scope caution: Issue/PR labels and code-search excerpts are not complete first-party behavioral acceptance, and original authors may prefer the existing extension mechanism.

## Function ownership

- S1 disposition: Historical A; `create_agent` assembles model/tool/observation loop executing task actions; current owner in maintained v1 surface is the composed agent runtime.
- S2 disposition: Historical —; tool ordering, per-call middleware and HITL provide local safety, not proven independent cross-agent coordination; DEFER absent a scoped multiple-unit witness.
- S3 disposition: Historical ?; model/tool limits enforce bounded current resource decisions and router chooses model per request; no supported whole-fleet current allocation closure established; UNKNOWN/DEFER.
- S3* disposition: Historical ?; decision-model AutoMode classifies intended tool risk *before* action, HITL obtains human intervention; after-tool independent result checking with binding and corrective feedback is a new unproven construction hypothesis, P0.
- S4 disposition: Historical ?; task-based model routing and fallbacks do not establish future-external intelligence feeding autonomous later policy; DEFER.
- S5 disposition: Historical ?; developer and operator set policies and approve sensitive actions, a lawful parent boundary. Do not grant agent ultimate identity/policy authority; NO_TARGET on this evidence.
- Evaluation object: One completed `ToolMessage` after `ToolCallRequest` handling that should be independently assessed before the generating agent trusts it for its next action.
- Scenario basis: HYPOTHETICAL

The scenario is a developer who composes an independent reviewer for a tool execution result. **No deployed demand, runtime failure, independently observed review error or savings is claimed.**

## Capability priority

- Priority rationale: S3* is the most source-native candidate for distinguishing pre-tool authorization from independent post-tool assessment; the v1 middleware already offers a relevant integration seam, but a reusable first-party complete C constructor and its incremental value remain unproven.
- Target transition: S3*=? -> S3*=C
- Proposed C construction: An optional first-party `IndependentToolOutcomeReviewMiddleware` that accepts a developer-provided independent reviewer, binds its verdict to the exact tool call/result and next-step release decision, enforces `accept/quarantine/request-correction` on returned agent feedback and records actual subsequent response, without making the original task model the reviewer. Review after execution never rolls back external side effects.
- P1 dependencies: Verify all `ToolMessage | Command` sync/async paths, replay and parallel tools, ordering versus HITL and OPEN #40492, actual first-party actor separation, and protected no-reviewer/error modes before asserting C.
- P2 optional: No proposed S2/S3/S4/S5 build absent distinct source-backed owner/feedback cases; no generalized controller or all-functions rollout.
- Proposal falsifier: A native custom reviewer already supplies full independently owned review, enforced result and later feedback at lower cost, or middleware cannot lawfully enforce the next-step result.
- C sufficiency falsifier: Native custom `wrap_tool_call` plus supported state/command API already supplies independent result review and enforced feedback with fewer parts, or proposed audit can be bypassed/replayed, lacks a legitimate corrective outcome, or cannot constrain the next model decision.
- Proposal-stage decision: GO
- Research disposition: NEEDS_EVIDENCE

`GO` means a coherent proposed function-specific constructor may be possible, not that new code is needed, that `S3*=C` exists, or that anyone should adopt it.

## Implementation options

- P0: Optional middleware with separate reviewer identity and executable `ToolMessage` result gate, exact call/result/verdict binding, isolated state, lawful corrective outcome and returned next-step feedback; prefer `langchain_v1` existing AgentMiddleware rather than changes to legacy classic or hosted services.
- Option A: No new code; implement and compare a tiny custom `wrap_tool_call/awrap_tool_call` wrapper using current v1 surface.
- Option B: Only if A does not offer the claimed first-party complete C-construction path, make one bounded first-party native opt-in middleware, disabled by default. No assumed new LangGraph runtime semantics.
- Proposed validation: Fake decision model + ToolMessage tool harness using v1 unit tests, sync/async. Positive: reviewer changes next-step decision with a traceable result binding; negative: missing/rejected/stale/forged result, HITL jump/replay/parallel, Command return and reviewer exception do not allow bypass. Native custom wrapper baseline and HITL control must be included.
- Validation state: NOT_RUN
- Incremental benefit: HYPOTHETICAL independent detection/correction before later agent actions, not original tool side-effect rollback; effort/safety against existing user-composed middleware must be measured later.

## Specification and domain alternatives

- Function-specific alternative: Existing AutoMode before-action risk classification protects a *different* decision, not actual result quality. HITL human approval is legitimate parent oversight. LangSmith callback/tracing (separate product) is not automatically independent control at this original boundary.
- Domain-native alternative: Simple custom v1 middleware and per-tool output checks may already be adequate; this is the mandatory cheap comparator and possible reason to drop P0.
- Responsibility: The original maintainer alone can accept/reject code; a developer installs an optional separate reviewer; operator remains S5 parent. No new S5 control inferred.
- Source freshness: Current original HEAD differs materially from the accepted historic review ref and now supports v1; independently reclassifying Index is Index-owned, not a condition to use the recorded included admission.
- Deliberate omissions: No unsupported inference that prior gaps were intentional; no promise to prevent the already-executed external tool action.

## Cost experiment

- Cost status: NOT_MEASURED
- Baseline: Current custom `wrap_tool_call` + existing AutoMode/HITL when appropriate, identical test workload.
- Hypothesis: An opt-in native reviewer constructor may reduce repeated one-off wiring or missed feedback while adding independent model latency/cost; future test should measure both and include unsuccessful cases.
- Demand status: NOT_ESTABLISHED. One demonstration of different lawful decision does not prove practical demand.

## Delivery and publication

- Our on-top contribution: PLAN_ONLY proposal for a source-specific v1 independent outcome-review constructor, with no code implementation.
- Decision scope: GO/NEEDS_EVIDENCE only for S3* post-tool independent corrective feedback; no demand/adoption, current Index C claim, PR or third-party commitment.
- Research outcome: PLAN_ONLY, source-first, future tests NOT_RUN, cost NOT_MEASURED, no external publication.
- Fork issue draft: issue.md is the Human decision layer; constructor-sufficiency.md is the technical developer layer; both depend on this receipt. Separate exact publication approval is still required.
- Next permitted action: Validate four-file metadata case and branch/authority preflight; persist on verified opensiro/meta only if latest concurrency and owner grants permit; otherwise PERSISTENCE_BLOCKED. Future testing is distinct from roadmap completion.

## Parallel contribution-on-top review

- Evaluation object: Source-native independent verification of actual tool outputs in one LangChain v1 composed agent before those outputs inform next action.
- Existing-work overlap: Built-in pre-tool AutoMode, human HITL, task-based ModelRouter, output-capable AgentMiddleware and relevant OPEN original #40158/#40492/#40556.
- Our on-top contribution: Optional reviewer-owned result audit with decision-binding, fail-closed release/correction and future returned feedback using first-party v1 middleware.
- Incremental benefit: HYPOTHETICAL; compare with a plain custom wrapper, avoid duplicating existing native semantics.
- Decision scope: PLAN_ONLY GO + NEEDS_EVIDENCE, never automatic public Issue/PR or new Index grade.
