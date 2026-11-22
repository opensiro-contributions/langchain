# LangChain — source-native independent tool-outcome review technical contract

**Canonical storage:** `opensiro-contributions/langchain@opensiro/meta:.opensiro/issues/langchain-independent-tool-outcome-review-20261122/constructor-sufficiency.md`.
**Level 1 / Human decision Issue:** [issue.md](issue.md).
**Canonical decision receipt:** [roadmap.md](roadmap.md), source for pins, historical Index vector, P0/P1/P2 and status.
**Stage:** PLAN_ONLY / HYPOTHESIS — **DRAFT — NOT PUBLISHED**. This is not shipped software or an accepted Index assessment.

## 1. Function-specific construction boundary and methodology checks

**Source and mode boundary:** Current original `langchain-ai/langchain@master:8ff3cd30eebfe37712a91f11e3f4b61a545e7a37`; maintained Python `libs/langchain_v1/langchain/agents/factory.py` and `agents/middleware/*`, using `langchain_core` tool/message primitives and the dependency LangGraph compiled state graph. Current `AGENTS.md` excludes new features in legacy `langchain_classic`. Developer-chosen agent/middleware is the system; distinct hosted LangSmith, Deep Agents, LangGraph projects and maintainer organization are not inherited. Historical included Index identity and revisions live only in [roadmap.md](roadmap.md).

**Target transition:** S3*=? -> S3*=C

**Six-function dependencies (S1/S2/S3/S3*/S4/S5):** A concrete S1 `create_agent` loop calls an authorized tool and consumes next `ToolMessage`. Existing S2 local middleware ordering and HITL gate must not be bypassed. S3 model/tool limits are existing current controls, not proposed whole-system management. The newly composed S3* reviewer must be genuinely independent of the task model, able to correct release of a false outcome, and return feedback. No S4 future strategy or S5 parent policy rights are transferred.

**Function witness:** A tool produces an actual result after execution. A separate installed reviewer sees bound call ID + result + task criterion and selects lawful `accept`, `quarantine` or `request-correction`; the middleware enforces what becomes agent-visible, with feedback on the next model call. Without the reviewer, ordinary ToolMessage path remains unchanged. Tool external effects that already happened cannot be retrospectively blocked.

**Counterfactual owner test:** Remove the reviewer while retaining `ToolNode`, `wrap_tool_call` and current AutoMode/HITL: task model still consumes the result but no independent result-quality selection occurs. If a simple custom v1 middleware already composes the exact same reviewer/effect/return, that may already be C, and no new code is warranted.

**Possible methodological negative control:** Human `HumanInTheLoopMiddleware` action approval is legitimate parent oversight and not evidence of autonomous S3*. `AutoModeMiddleware` uses a separate decision model to classify pre-execution risk, but does not itself review actual post-execution outcomes as claimed. No inference of S4/S5 deficit from old '?'.

**Contributor / maintainer priorities:** NOT_STATED for adopting independent post-tool review. Source contribution guidance at [AGENTS.md](https://github.com/langchain-ai/langchain/blob/8ff3cd30eebfe37712a91f11e3f4b61a545e7a37/AGENTS.md) requires scoped conventional PRs. No approval or demand is attributed.

## 2. Source-pinned baseline and parallel native Track A / on-top Track B

**Original native workflow:** [`create_agent`](https://github.com/langchain-ai/langchain/blob/8ff3cd30eebfe37712a91f11e3f4b61a545e7a37/libs/langchain_v1/langchain/agents/factory.py) compiles an agent with model/tool nodes; middleware `wrap_tool_call/awrap_tool_call` sees `ToolCallRequest`, invokes a handler, and can return `ToolMessage | Command` for next graph step.

**Closest existing solution:** A developer-defined subclass of [`AgentMiddleware`](https://github.com/langchain-ai/langchain/blob/8ff3cd30eebfe37712a91f11e3f4b61a545e7a37/libs/langchain_v1/langchain/agents/middleware/types.py) can potentially call a separate verifier after invoking the tool, with no new API. Existing [AutoMode](https://github.com/langchain-ai/langchain/blob/8ff3cd30eebfe37712a91f11e3f4b61a545e7a37/libs/langchain_v1/langchain/agents/middleware/auto_mode.py) is before-action risk control; [HITL](https://github.com/langchain-ai/langchain/blob/8ff3cd30eebfe37712a91f11e3f4b61a545e7a37/libs/langchain_v1/langchain/agents/middleware/human_in_the_loop.py) is human approval.

**Relevant original Issues/PRs:** [#40158](https://github.com/langchain-ai/langchain/issues/40158) OPEN before-execution credential verification; [#40492](https://github.com/langchain-ai/langchain/issues/40492) OPEN reported HITL after_model jump/reject bypass; [#40556](https://github.com/langchain-ai/langchain/pull/40556) OPEN risk/model decision middleware; [#41702](https://github.com/langchain-ai/langchain/pull/41702) OPEN experimental nested tool executor. Unmerged code is not shipped. None establishes final maintainer product intent.

| Required C link | Track A — first-party native | Track B — hypothetical delta |
| --- | --- | --- |
| Independent owner | Configurable hook + developer can instantiate separate classifier/reviewer | Explicit callback protocol/identity separation for reviewing actual output |
| Binding | `ToolCallRequest.tool_call`, tool result `ToolMessage` | Bind call ID, output hash or stable result reference and run/version; reject mismatch |
| Action | Middleware may return message or command | Enforce specific accepted/quarantined/correction response before later trust |
| Feedback | Graph returns agent next tool/model step | Recorded result review decision influences subsequent task action, no result laundering |

**On-top distinctness:** The post-execution outcome review is a different evaluation object than pre-tool approval. A second baked-in class is **not** justified if a custom middleware already supplies the complete C path. Merely adding logs, scores or posthoc commentary is not correction.

**Source ambiguity / rights blockers:** Need to test `Command` returns, concurrent tool results, intercept ordering with HITL, persistence/replay and `jump_to=tools`. No original maintainer commitment; public proposal requires separate exact current owner authorization; no external publication permitted here.

## 3. Minimal complete S3* first-party C construction

**Required property:** Support an optionally installed independent post-tool outcome reviewer that owns a distinct lawful `accept/quarantine/request-correction` decision, enforces it on agent-visible output, and returns the effect for later operation.

**Architectural C-sufficiency argument:** Use an opt-in composable `AgentMiddleware` implementation in maintained v1 (or existing custom extension if proven sufficient). On `wrap_tool_call` and `awrap_tool_call`, invoke the original handler exactly once; match returned `ToolMessage` with tool ID, task scope, and result reference; pass bounded evidence to a separately supplied reviewer; validate reviewer output; return either original response, a quarantined error response, or a lawful correction request. Ensure feedback enters the next model step and tests can assert that. No rollback of external tool effects.

**Explicit non-goals:** No generic supervisor; no S5 policies; no controller over all agents, no mandatory second model, no Index reclassification, no invented package adoption, no tool execution rollback, no integration into deprecated `langchain_classic`.

**Implementation dependency graph:** v1 `create_agent` → `ToolNode` / composed `wrap_tool_call` → result binding → isolated reviewer decision → fail-closed release/correction → next graph step. Must preserve current HITL and work across sync/async; unknown result shapes fail closed only when enforce mode is selected.

## 4. Priorities, optional alternative and stopping rules

**P0 and P1:** P0 is optional independent S3* post-tool review with actual enforce/feedback; P1 inspect current wrapper sufficiency, HITL bypass #40492, `Command`, parallel and replay semantics before claiming C.

**P2:** None without new scoped original-native evidence for other functions. No generic extension suite.

**Alternative path:** Use one straightforward user-defined `AgentMiddleware` wrapper and human HITL for risk decisions; compare that native solution under identical tests and cost.

**Stop:** If native custom hook provides complete reviewer ownership or if no lawful downstream corrective effect exists, abandon new first-party module. Stop code or external Issues until separate approval. If reviewer errors can bypass release in enforce mode, structural C sufficiency not established.

## 5. Future source-native acceptance — derive tests, do not copy a matrix

**Native test commands and entry points:** From `libs/langchain_v1`, `uv sync --group test` then `uv run --group test pytest tests/unit_tests/agents/ -q`; target a focused new `tests/unit_tests/agents/middleware/test_independent_tool_outcome_review.py` only if built. Proposed; NOT_RUN. Compare a minimal custom `wrap_tool_call` baseline with the new feature using a fake decision model and fake tools.

**Positive functional closure:** Tool returns a misleading success, independent reviewer decides quarantine, graph's next model call sees quarantined result not fabricated success, with call/output/reviewer correlation. A second accepted result passes through unmodified.

**Independent alternative (where applicable):** A custom wrapper with the same separate reviewer must be measured; if both are functionally identical, prefer no new module.

**Negative authority and compatibility (where applicable):** Missing/stale/forged/rejected reviewer evidence blocks trusted success in enforcing mode; tool effect is not replayed during review, command-shaped returns remain consistent, HITL edit/reject plus `jump_to` does not skip post-result enforcement, parallel requests bind correct identities, no-reviewer behavior stays byte-compatible where feasible.

**Matched native alternative:** Test existing `AutoModeMiddleware` and human HITL separately: they address different timepoints; custom result reviewer is the meaningful baseline, not an unguarded strawman.

## 6. Proposal verdict, falsification, evidence ownership and handoff

**Proposal-stage decision:** GO

**Research disposition:** NEEDS_EVIDENCE

**Primary falsifier:** The native custom wrapper already achieves identical separately owned after-tool review/decision/effect/feedback at lower cost; or first-party entry point cannot prevent invalid outcomes from informing subsequent agent choices.

**Validation state:** NOT_RUN, source-only analysis; neither tests nor original maintainers accepted the proposal.

**Ownership of truth:** Accepted historical assessment is Index-owned; proposal pins and statuses are in [roadmap.md](roadmap.md); original maintainer controls implementation and all upstream adoption; matching fork metadata controls only this OpenSiro research.

**Cost status:** NOT_MEASURED. Additional latency, failures, extra model calls and engineering maintenance to be measured against minimal wrapper.

**Next permitted action:** Retain PLAN_ONLY fork-local draft if branch owner/concurrency gates allow, verify both structural validators and readback. Future code/native tests require separate implementation intent; public fork Issue and third-party communications require exact current owner approval.

**Human backlink:** [issue.md](issue.md).

**case receipt:** [roadmap.md](roadmap.md).

**AI disclosure:** AI-generated architecture proposal grounded in pinned first-party files and current original Issues/PRs. No executed tests, no measured cost, no external publication approval.
