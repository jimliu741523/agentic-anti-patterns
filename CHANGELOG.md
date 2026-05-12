# CHANGELOG

Newest on top. Each entry corresponds to a meaningful catalog change — new entry, structural reorganization, or scope shift. Cosmetic edits are not logged.

## 2026-05-12
- **AP-43 Coarse-grained tool authorization (binary allow/deny without per-call scope enforcement)** added — anchored to RP-6 (agent runtime guard, per-tool authorization dimension). Agent runtimes authorize tools as binary enabled-or-disabled at configuration time; every call to an enabled tool is automatically passed with no per-call check of caller identity, session scope, required privilege, or action intent. Production deployments require ALLOW/DENY/MODIFY/DEFER/STEP_UP verdict granularity that no current framework provides as composable middleware. Empirical anchors: GitHub openai-agents-python#2868 (practitioners explicitly requesting non-binary per-tool authorization middleware — ALLOW/DENY/MODIFY/DEFER/STEP_UP — April 2026, open); arxiv 2605.04785 AgentTrust (first released pre-execution interception, 95.0–96.7% verdict accuracy, AGPL, content/command safety only — confirms interception architecture works, leaves MIT/Apache per-call authorization gap open); arxiv 2605.02682 CASA (hybrid task-based access control research, no package); arxiv 2604.16706 AgentProp-Bench (rejection and recovery are independent capabilities, rho=0.126 — binary tool blocking cannot substitute for structured per-call authorization). Distinct from AP-23 (argument-boundary injection — AP-43 is the authorization decision before args are inspected), AP-41 (return-content injection — AP-43 fires before execution, AP-41 fires after), AP-26 (credential blast radius — AP-43 is about tool-call scope, not credential lifecycle).
- **AP-42 Multi-agent failure attribution blackout** added — anchored to RP-5 (multi-agent concurrent state coordination primitives). When a multi-agent pipeline produces wrong output or crashes, no runtime mechanism identifies which agent or step was responsible; teams restart the full pipeline rather than rolling back to the earliest faulty step. Empirical anchors: arxiv 2604.22708 (attribution unsolved in partially-observable traces); MASPrism 2605.07509 (0.6B probe model achieving 89.50% relative improvement over Gemini-2.5-Pro on attribution accuracy); Conformal Agent Error Attribution 2605.06788 (certifiable finite-sample rollback targets via conformal prediction). Key distinction from AP-27 (concurrent state corruption) and AP-31 (hallucinated consensus): AP-42 is the diagnostic failure — wrong output propagated through sequential handoffs with no provenance trail — not a concurrent write conflict or false agreement.
- **AP-41 Tool-return content injection (trusted-channel indirect injection)** added — anchored to RP-6 (agent runtime guard, return-content sanitization dimension). Adversaries embed malicious instructions in a registered tool's *response content* — API response body, database record field, MCP tool output payload, file read result — which the agent incorporates into conversation history as a trusted first-party observation with no data-boundary sanitization applied. Key distinction from AP-01 (direct prompt injection): AP-41 exploits the elevated trust agents place on registered-tool outputs — no `<external_data>` markers or dual-LLM sanitization is applied to structured tool return values. Empirical anchor: arxiv 2604.11790 ClawGuard. Confirmed by AgentTrust (2605.04785) and Reinforced Agent (2604.27233).
- **AP-40 Cooperative intent erosion from unbounded memory accumulation (Memory Curse)** added — anchored to RP-3. Expanding accessible history without write-path content governance degrades multi-agent cooperation in 18/28 model-game settings (arxiv 2605.08060). Memory content (conflict history), not length, is the causal trigger; write-path content filtering restores cooperation substantially.
- **AP-39 Memory control flow hijacking (adversarial retrieval steering)** added — anchored to RP-3. >90% vulnerability across frontier models on real LangChain/LlamaIndex agents (arxiv 2603.15125). Extends write-path gap from data-quality to active attack surface.
- **AP-38 Gradual constraint adherence decay under accumulated structural requirements** added — anchored to RP-6. Agent finishes within budget and step count while violating 2–3 of 5 original requirements; no standard circuit breaker fires (arxiv 2605.06445 Constraint Decay).

## 2026-05-11
- **AP-37 Overconfident single-belief memory commit (under partial observability)** added — anchored to RP-3. Agents commit exactly one definite conclusion per observation; ambiguous observations resolved prematurely into overconfident beliefs (arxiv 2605.05583 BeliefMem, 2605.06527 STALE, 2605.03675 MemTier).
- **AP-36 Agent capacity overload cascade (absent backpressure primitives)** added — anchored to RP-5. No standard mechanism for a downstream agent to declare saturation; upstream retries compound load (GitHub autogen#7321, arxiv 2605.03310).
- **AP-35 Long-horizon tool-attack chain (sequential stealth exploitation)** added — anchored to RP-6. Multi-step adversarial sequence distributes payload across N tool outputs; shadow memory reduces success from 100% to 8.3% (arxiv 2605.03228 MAGE).
- **AP-34 Cross-session slow-drip memory injection** added — anchored to RP-9. One innocuous fragment per session assembles a jailbreak across 50+ sessions; cross-session detection near zero (arxiv 2604.21131).
- **AP-33 Non-functional tool description bias** added — anchored to RP-8. Assertive description text shifts selection probability 10× without changing tool functionality (arxiv 2505.18135).
- **AP-32 Flat multi-agent memory (absent memory scope isolation)** added — anchored to RP-3. All agents write to shared unsegmented namespace; no owner, scope, or provenance isolation (arxiv 2605.04264, 2604.16548).

## 2026-05-10
- **AP-31 Hallucinated multi-agent consensus** added — anchored to RP-5. Agents report agreement without committing state; coordinator proceeds on verbal signal alone (MAST arxiv 2503.13657, Semantic Consensus 2604.16339).
- **AP-30 MCP marketplace supply chain injection** added — anchored to RP-9. Installation-phase supply chain attack via unverified MCP server registries; escalation to stdio RCE (OX Security April 2026, CVE-2026-30623).
- **AP-29 Unconditional tool invocation (tool-use tax)** added — anchored to RP-8. Full schema catalog transmitted every turn; tool-augmented reasoning underperforms CoT under semantic noise (arxiv 2605.00136).
- **AP-28 Agent runaway budget burn and silent tool-call success** added — anchored to RP-6. 847 API calls for a weather query; $437 overnight spend; no in-process cost ceiling (CrewAI+LangChain taxonomy 2602.21806).
- **AP-27 Multi-agent concurrent state corruption** added — anchored to RP-5. Parallel agents write shared artifacts without locks; production coordination failure rates 41–87% (arxiv 2601.04170, 2604.16339).

## 2026-05-09
- **AP-26 Sub-agent credential scope overflow** added — anchored to RP-9. Static fully-scoped tokens forwarded to sub-agents; PocketBase production DB wiped in <10s (Cursor agent + leaked Railway token).
- **AP-25 Tool-schema wire-format incompatibility** added — anchored to RP-8. Phi-4 14B 0%→84.4% accuracy with schema compilation (TSCG).
- **AP-24 Memory write-path accumulation** added — anchored to RP-3. Agents commit every observation without salience gating; active-task performance drops to 40–60% (arxiv 2603.07670 MemoryArena).

## 2026-05-07
- **AP-22 Context pollution from raw tool output** added. `mksglu/context-mode` 98% output-size reduction confirms pre-mitigation baseline is this anti-pattern in production.
- **AP-21 Long-horizon agent state collapse** added. `bytedance/deer-flow` (65k★) and `cocoindex` trending; lossy compression accumulates into corruption over hour/day timescales.

## 2026-05-04
- **AP-18 Autonomy creep** added — closes the original 14-entry roadmap.
- **AP-19 Spec-drift on rigid agent specs** added.
- **AP-20 Multi-agent vertical-domain failure** added.
- Roadmap converted from "AP-N todos" to "demand-driven, PRs welcome".

## 2026-05-02
- **AP-17 RAG retrieval poisoning** added. Four scenarios: Confluence-edit injection, public-mirror tampering, embedding-poisoning at index time, citation-as-referrer for downstream AP-11.
- README intro contrasts catalog with skills-catalog wave.

## 2026-04-23
- **AP-16 MCP server trust boundary collapse** added.

## 2026-04-21
- **AP-15 Tool-description drift** added.

## 2026-04-20
- **AP-12, AP-13, AP-14** added. "About this catalog" section added. Inline cross-links added.

## 2026-04-19
- **AP-08, AP-09, AP-10, AP-11** added. Hero Mermaid diagram added. Initial 7-entry catalog committed (AP-01..AP-07).
