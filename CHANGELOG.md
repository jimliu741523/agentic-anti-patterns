# CHANGELOG

Newest on top. Each entry corresponds to a meaningful catalog change — new entry, structural reorganization, or scope shift. Cosmetic edits are not logged.

## 2026-05-09
- **AP-26 Sub-agent credential scope overflow** added — anchored to RP-9. Orchestrators forwarding static, fully-scoped tokens to sub-agents create a blast-radius escalation: any sub-agent compromise or MCP hijack (SecurityWeek 2026) can reach every resource the parent token touches. Three confirmed incident vectors: PocketOS production DB wiped in <10 s (Cursor agent + leaked Railway token), Claude Code OAuth theft via MCP tool manipulation, 24,000 MCP-exposed credentials in ~12 months. Entry covers: scope-narrowing + TTL-shortening at issuance, cascade revocation, delegation chain logging, one-credential-per-task minimum-scope issuance; detection: credential cardinality invariant, scope-narrowing audit at spawn, token age at use. Cross-refs AP-04/AP-12/AP-16/AP-23. System/lifecycle nav + catalog table + code-review checklist updated (25→26). References McpAgentAuth Pattern 15.
- **AP-25 Tool-schema wire-format incompatibility** added — anchored to RP-8. Phi-4 14B 0%→84.4% accuracy (TSCG), Ollama streaming-protocol bug. Browse-by-stage nav + catalog table + checklist + Roadmap updated. Cross-ref Pattern 14 (ToolSchemaCompiler).
- **AP-24 Memory write-path accumulation** added — anchored to RP-3. Agents commit every observation without salience gating, contradiction detection, or TTL; long-lived agents accumulate contradictory and stale facts until active-task performance drops to 40–60% (arxiv 2603.07670 MemoryArena empirical gap). Entry covers: AUDN loop pattern, five mitigation layers (salience gate, contradiction resolution strategies, TTL/decay, provenance tagging), four detection methods (contradiction count, active-vs-passive recall gap, memory growth rate, contradiction injection canary). References: 2603.07670, 2603.11768 (SSGM), 2605.05583 (BeliefMem), 2605.06527 (STALE), mem0.ai 2026 report, ossinsight.io practitioner quote. State/memory nav updated; catalog table 23→24.

## 2026-05-07
- **AP-22 Context pollution from raw tool output** added — driven by `mksglu/context-mode` (13,606★, +711 today) reporting “98% reduction in AI coding agent output size across 14 platforms,” which positions the pre-mitigation baseline as this anti-pattern in production. Agents pipe full, unfiltered tool responses verbatim into context; by mid-task, raw output crowds out earlier task constraints; model reasons from recency rather than relevance. Cross-refs AP-05 (cost) / AP-06 (goal drift) / AP-21 (long-horizon). Browse-by-failure-stage nav and code-review checklist updated; references Liu et al. 2023 “Lost in the Middle” on LLM recency bias.
- **AP-21 Long-horizon agent state collapse** added — driven by `bytedance/deer-flow` (65k★) and `cocoindex` (“incremental engine for long-horizon agents”) trending. Lossy compression accumulates into corruption over hour/day timescales; mitigation menu emphasises provenance-tagged rollups, checkpoint/rollback as first-class operations, and liveness-vs-progress dashboards.

## 2026-05-04
- **AP-18 Autonomy creep** added — closes the original 14-entry roadmap (the trajectory-not-event failure mode where agent privilege drifts upward over months).
- **AP-19 Spec-drift on rigid agent specs** added — driven by spec-driven-development tooling (`Fission-AI/OpenSpec`) making the failure visible.
- **AP-20 Multi-agent vertical-domain failure** added — driven by simultaneous trending of `TradingAgents`, `dexter`, `ai-hedge-fund`, `OpenStock` (multi-agent finance vertical).
- Roadmap converted from “AP-N todos” to “demand-driven, PRs welcome”.

## 2026-05-02
- **AP-17 RAG retrieval poisoning** added — covers four scenarios: classic Confluence-edit injection, public-mirror tampering, gradient-tuned embedding poisoning at index time, and citation-as-referrer for downstream AP-11 fetches.
- README intro contrasts catalog with the skills-catalog wave (`openai/skills`, `vercel-labs/skills`, `awesome-codex-skills`, `awesome-agentic-patterns`) — failure-mode and skills catalogs complement, neither subsumes.

## 2026-04-23
- **AP-16 MCP server trust boundary collapse** added — covers tool descriptions, resource bodies, and `sampling/*` prompts as architectural injection paths in MCP-installed servers.

## 2026-04-21
- **AP-15 Tool-description drift** added — agent’s prompt-described view of a tool diverges from the tool’s actual current behaviour.

## 2026-04-20
- **AP-12, AP-13, AP-14** added (agent-to-agent injection, planner/executor divergence, silent retry masking failure).
- “About this catalog” section added: honest framing on AI-assisted authoring + entry quality bar.
- Inline “See also” cross-links between AP-05 / AP-08 / AP-11 and `agent-memory-lab`.

## 2026-04-19
- **AP-08, AP-09, AP-10, AP-11** added (memory poisoning, tool-selection lock-in, confidence inflation on self-verification, exfiltration via agent-initiated fetch).
- Hero Mermaid diagram added above the catalog (AP-01 illustrated injection flow).
- Initial 7-entry catalog committed (AP-01..AP-07).
