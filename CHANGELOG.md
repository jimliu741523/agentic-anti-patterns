# CHANGELOG

Newest on top. Each entry corresponds to a meaningful catalog change — new entry, structural reorganization, or scope shift. Cosmetic edits are not logged.

## 2026-05-04
- **AP-18 Autonomy creep** added — closes the original 14-entry roadmap (the trajectory-not-event failure mode where agent privilege drifts upward over months).
- **AP-19 Spec-drift on rigid agent specs** added — driven by spec-driven-development tooling (`Fission-AI/OpenSpec`) making the failure visible.
- **AP-20 Multi-agent vertical-domain failure** added — driven by simultaneous trending of `TradingAgents`, `dexter`, `ai-hedge-fund`, `OpenStock` (multi-agent finance vertical).
- Roadmap converted from "AP-N todos" to "demand-driven, PRs welcome".

## 2026-05-02
- **AP-17 RAG retrieval poisoning** added — covers four scenarios: classic Confluence-edit injection, public-mirror tampering, gradient-tuned embedding poisoning at index time, and citation-as-referrer for downstream AP-11 fetches.
- README intro contrasts catalog with the skills-catalog wave (`openai/skills`, `vercel-labs/skills`, `awesome-codex-skills`, `awesome-agentic-patterns`) — failure-mode and skills catalogs complement, neither subsumes.

## 2026-04-23
- **AP-16 MCP server trust boundary collapse** added — covers tool descriptions, resource bodies, and `sampling/*` prompts as architectural injection paths in MCP-installed servers.

## 2026-04-21
- **AP-15 Tool-description drift** added — agent's prompt-described view of a tool diverges from the tool's actual current behaviour.

## 2026-04-20
- **AP-12, AP-13, AP-14** added (agent-to-agent injection, planner/executor divergence, silent retry masking failure).
- "About this catalog" section added: honest framing on AI-assisted authoring + entry quality bar.
- Inline "See also" cross-links between AP-05 / AP-08 / AP-11 and `agent-memory-lab`.

## 2026-04-19
- **AP-08, AP-09, AP-10, AP-11** added (memory poisoning, tool-selection lock-in, confidence inflation on self-verification, exfiltration via agent-initiated fetch).
- Hero Mermaid diagram added above the catalog (AP-01 illustrated injection flow).
- Initial 7-entry catalog committed (AP-01..AP-07).
