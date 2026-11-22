# LangChain — optional independent tool-outcome review (Opensiro roadmap)

**PLAN_ONLY · proposal-stage GO · research NEEDS_EVIDENCE · DRAFT — NOT PUBLISHED**

**One-sentence proposal:** Let a LangChain Python v1 developer compose a genuinely separate reviewer of returned tool outcomes before the agent trusts them in its next decision, while keeping existing no-reviewer behavior unchanged.

**Canonical decision receipt:** [roadmap.md](roadmap.md), source of the immutable Index pin, six historical states, proposal status and all priorities.
**Technical companion:** [constructor-sufficiency.md](constructor-sufficiency.md), the source-native developer contract and future tests.
**Working fork:** `opensiro-contributions/langchain`.
**Case:** `.opensiro/issues/langchain-independent-tool-outcome-review-20261122/` on `opensiro/meta`.

## 1. Why Opensiro and central accepted VSM assessment

Opensiro studies whether VSM-informed organizational constructors can make agent development more systematic. This is a research hypothesis, not measured savings, an external maintainer request, or a certification.

### Central accepted historical Index — not proposed after-states

> **ACCEPTED HISTORICAL INDEX — not current-HEAD grades or proposed after-states**
>
> **`S1=A · S2=— · S3=? · S3*=? · S4=? · S5=?`**
>
> [Immutable Index assessment](https://github.com/opensiro/vsm-harness-index/blob/a3fcf7c156ef4d1132680890bc11544681fd30c0/assessments/la/langchain.md), Index `a3fcf7c156ef4d1132680890bc11544681fd30c0`, blob `4a3114b6a7427a7997ba3415b5c395d169feec37`, original `review_ref=348c9dc572599947d2d7d33d6a5b8b936e92a1d4`, reviewed 2026-09-15, Profile 0.2.1 and assessment procedure 0.3.1.

**Repository-wide audit:** Original [master@8ff3cd30](https://github.com/langchain-ai/langchain/commit/8ff3cd30eebfe37712a91f11e3f4b61a545e7a37) 2026-11-22, including `AGENTS.md`, v1 `create_agent`/middleware, core tool/message contracts, model-routing/limits, examples, unit tests, contributor policy, relevant original issues and open PRs. System is the maintained Python agent-construction/runtime surface. LangGraph, Deep Agents and hosted LangSmith remain separate; `langchain_classic` is legacy and expressly accepts no new features.

| Function / plain-language role | Historical Index state | Current source-backed ownership / limits | Candidate and priority |
| --- | --- | --- | --- |
| **S1 · Operations** | A | `create_agent` builds the model/tool execution loop. | NO_TARGET — current task execution exists |
| **S2 · Coordination** | — | Tool/graph ordering and per-call guards, not independent multi-agent interference resolution. | DEFER — distinct organizational closure unverified |
| **S3 · Current management** | ? | Model and tool-call limits, task-dependent model routing; no proven fleet commitments decision. | DEFER — different evaluation object |
| **S3* · Independent review** | ? | `AutoModeMiddleware` reviews intended risk before tool action, while HITL delegates to humans; no evidenced independently owned post-tool outcome correction gate. | P0 — hypothetical optional `C` constructor |
| **S4 · Future adaptation** | ? | Route selection uses present task instructions, no shown external future sensing plus later feedback. | DEFER |
| **S5 · Identity/policy** | ? | Developer/operator policy and human review are legitimate parent authority. | NO_TARGET — do not transfer S5 |

These are **ownership categories**, **not quality ranks**. `A` means agent-closed function, `C` means a first-party developer-composable constructor, `P` legitimate parent mode, `—` bounded no material path, and `?` unresolved historical evidence. A historic `?` is not proof of missing current functionality.

**Priority rationale:** S3* exposes the narrow difference between existing pre-action guard and a separate post-action corrective owner, and maps to maintained first-party tool hooks; rank it only after surveying all six. A pre-existing custom wrapper is an essential counterfactual.

**Deliberate exclusions / methodology challenge:** No inference that historical ungraded functions were intentionally omitted. Do not import external LangGraph, Deep Agents, hosted LangSmith or human organization into this system boundary. Current sources cannot retroactively upgrade the Index's historical review.

## 2. Selected construction hypothesis and operator outcome

**Target transition:** S3*=? -> S3*=C

**Function-specific disturbance:** HYPOTHETICAL tool returns a plausible but incorrect/unsafe claim of completion; the task model would ordinarily consume it.

**Proposed C capability (P0):** A developer may compose a separately supplied outcome verifier with explicit `accept / quarantine / request-correction` rights over the next agent-visible response, independent of the actor that requested the tool. It must bind decision to tool call identity, actual output and version and return the enforced outcome to later task operation.

**Best native operator alternative:** Compose a minimal custom [`AgentMiddleware.wrap_tool_call`](https://github.com/langchain-ai/langchain/blob/8ff3cd30eebfe37712a91f11e3f4b61a545e7a37/libs/langchain_v1/langchain/agents/middleware/types.py), combining current `AutoModeMiddleware` and human HITL where needed. This may already meet the whole scoped goal.

**Expected user benefit:** HYPOTHETICAL reduced false downstream trust and fewer repetitive hand-built review gates; not an observed demand, quantitative saving or reduction of already-executed external side effects.

**Architectural sufficiency argument:** A proposed native opt-in wrapper can intercept a `ToolMessage | Command` result and route it through a distinct reviewer before producing the next response. To qualify as C, an installed developer-composed reviewer must own a lawful materially different decision and the path must enforce it on *all supported relevant* execution/replay flows with returned feedback. Tool side effects are not reversible by an after-tool reviewer. The missing proof is this complete owner/effect/feedback chain compared with a cheaper custom wrapper.

## 3. Existing native work versus missing construction

**Track A — native coverage:** SHIPPED [`AutoModeMiddleware`](https://github.com/langchain-ai/langchain/blob/8ff3cd30eebfe37712a91f11e3f4b61a545e7a37/libs/langchain_v1/langchain/agents/middleware/auto_mode.py) pre-tool risk decisions, SHIPPED [HITL](https://github.com/langchain-ai/langchain/blob/8ff3cd30eebfe37712a91f11e3f4b61a545e7a37/libs/langchain_v1/langchain/agents/middleware/human_in_the_loop.py), SHIPPED `ModelRouterMiddleware` for run selection; OPEN original [#40158](https://github.com/langchain-ai/langchain/issues/40158) pre-tool credential checks and [#40492](https://github.com/langchain-ai/langchain/issues/40492) reported HITL jump bypass; OPEN [PR #40556](https://github.com/langchain-ai/langchain/pull/40556) classifier middleware. None is evidence of a shipped distinct post-tool independent reviewer.

**Track B — independent on-top C construction:** First test developer composition of existing `wrap_tool_call/awrap_tool_call`. Only if incomplete, add a narrowly-scoped optional `IndependentToolOutcomeReviewMiddleware` on maintained v1, returning a bound review decision that can prevent or correct the response before it drives subsequent reasoning.

| C-sufficiency requirement | Already present (A) | Still needed / uncertainty (B) |
| --- | --- | --- |
| Actual tool result and independent choice | `ToolCallRequest`, `ToolMessage`, middleware hook | Bind independent reviewer evidence to call/result and enforce the decision |
| Lawful corrective effect and return | Middleware returns `ToolMessage | Command` into agent control | Prove quarantined result cannot become trusted next action; feedback/replay semantics |
| Stable default, interoperability | Current v1 middleware API, AutoMode, HITL | No-reviewer parity, sync/async, jump, multi-tool, failure and replay tests |

**Distinctness and falsifier:** If the unchanged first-party v1 middleware with a custom reviewer supplies the same independent decision/effect/feedback path, a special new middleware is not justified. Actual returned outcomes, not merely a classifier label or human approval, must control the subsequent decision.

## 4. Priorities and minimum sufficient result

- **P0:** One optional independently composed S3* result reviewer with first-party enforceable release/correct/quarantine and returned next-step feedback; or demonstrate that no added constructor is necessary.
- **P1:** Compare cheapest custom middleware/HITL baseline and investigate `Command`, concurrent tools, stale reviewer decisions, replay and reported `jump_to=tools` behavior before claiming complete C.
- **P2:** No S2/S3/S4/S5 construction, new generic policy engine, Index regrade or product change.

Minimum proof is one lawful positive distinct reviewer outcome and protected negatives within the original's native runtime; proposal GO is **not** implementation.

## 5. Proposed acceptance and stop gates

**Proposed C-sufficiency verdict:** GO — architecturally plausible source-native S3*=C construction hypothesis, distinct from shipping or utility.

**Future positive test:** Under same tool outcome, reviewer chooses a different authorized release/quarantine decision, observable in the *next* agent step and with a checkable call/result/reviewer link; compare native custom middleware.

**Future negative test:** Missing/forged/stale/error reviewer evidence fails closed when enforce mode selected. No-reviewer mode remains unchanged; no false claims for tool side effects already executed; `Command`/parallel/replay/HITL controls are verified.

**Proposed falsifier:** Existing custom wrapper passes same complete S3* ownership tests at lower cost or first-party hook cannot enforce post-tool result decision across supported flow paths.

**Validation state:** NOT_RUN — native code and tests not executed; cost NOT_MEASURED; all proposed acceptance is future work.

## 6. Independent paths

**Original-native contribution:** Optional module only after cheapest supported middleware path compared; independent feature construction remains the original maintainers' design/adoption decision, not a required OpenSiro dependency.

**Profile / Skills:** Use historical Profile 0.2.1 / procedure 0.3.1 as provenance only, never current grade or claimed autonomy score.

**Domain fork:** Matching [opensiro-contributions/langchain](https://github.com/opensiro-contributions/langchain); metadata belongs on `opensiro/meta` only; no changes to source/default branch.

## 7. Cost hypothesis

Incremental implementation, latency and reviewer model tokens all **NOT_MEASURED**. Compare original native custom wrapper with proposal on same tasks including failures and human review, avoiding fabricated return on investment.

## 8. Decision / handoff

**Proposal-stage decision:** GO

**Research disposition:** NEEDS_EVIDENCE

**Decision reason / next permitted step:** Preserve this untested hypothesis as a bounded fork-local PLAN_ONLY proposal with initial reservation and source-first receipt. Demonstrate independent result owner and correction outcome against a native custom wrapper; do not claim maintainer need or publication approval.

**Agent/developer handoff:** Inspect the [AI technical contract](constructor-sufficiency.md) for exact seams, test cases, alternatives and stop conditions. The source of truth for this proposal is [roadmap.md](roadmap.md).

**Rights and publication:** DRAFT — NOT PUBLISHED. No original/fork public GitHub Issue, comment, PR, or product code. Separate exact current-conversation owner approval is mandatory for each outward action. Another agent's later competing #58 reservation must be checked before a fork write.

**AI disclosure:** AI-assisted source analysis and proposed plan; no verified native tests, production metrics or maintainer decision.

**Public fork Issue title (draft only):** LangChain — optional independent tool-outcome review (Opensiro roadmap)

**Public fork Issue body (draft only):** The eight-section Human proposal above is the exact canonical draft body; public rendering replaces draft status and freezes internal case links. It is NOT permission to publish.
