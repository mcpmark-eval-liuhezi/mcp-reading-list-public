# MCP Reading List

A public, curated arXiv reading list on the **Model Context Protocol (MCP)** — the open standard for wiring LLMs up to tools and data sources. Security is the priority: threat models, attacks, sandboxing, and privilege issues come first, followed by the broader picture (surveys, ecosystem measurement, and agent/tool-use architecture work built around MCP).

## What's in this repo

- **[`notes/mcp-papers.md`](notes/mcp-papers.md)** — the full reading list. It's organized in two sections: **Security papers** first (5 papers: the foundational threat-taxonomy survey [2503.23278], a modern SoK separating adversarial security from epistemic safety [2512.08290], an empirical study of MCP attack vectors with MCPBench/MCPSec [2601.17549] and MCPSecBench [2508.13220], and a context-aware server collaboration architecture [2601.11595]), then **Broader picture** papers (a survey positioning MCP against ACP/A2A/ANP [2505.02279], a large-scale measurement study of the MCP ecosystem [2509.25292], and a production architecture/implementation paper for multi-agent systems on MCP [2504.21030]). Each entry includes title, authors, arXiv ID/link, submission date, a 2–3 sentence summary, and a one-line "why it matters" note. The file closes with a **Gaps & Next Steps** paragraph.

## Quick start

1. Read `notes/mcp-papers.md` top to bottom — security papers (1–5) first, then the broader picture (6–8).
2. Start with [arXiv:2503.23278](https://arxiv.org/abs/2503.23278) (MCP: Landscape, Security Threats, and Future Research Directions) as your single entry point for the threat taxonomy.
3. For empirical evidence that current mitigations are weak, see [arXiv:2508.13220](https://arxiv.org/abs/2508.13220) (MCPSecBench).
4. For a reality check on ecosystem health before trusting any MCP adoption numbers, see [arXiv:2509.25292](https://arxiv.org/abs/2509.25292) (A Measurement Study of the MCP Ecosystem).

## Search terms used

- `"Model Context Protocol"` (broad) — local arXiv mirror
- `"Model Context Protocol" AND (security OR attack OR threat OR sandbox OR privilege)` (security-focused) — local arXiv mirror
- `"Model Context Protocol" AND (survey OR architecture OR "agent tool use" OR "tool calling")` (surveys & architectures) — local arXiv mirror

Papers were shortlisted from those results, and the details (title, authors, arXiv ID, submission date, summary) in `notes/mcp-papers.md` were verified on each paper's own arXiv abstract page (arxiv.org/abs/<id>), not from search snippets.

## Gaps & next steps

- **No runtime sandboxing inside a running MCP client** — we have threat taxonomies and hardening proposals (MCPSec, SMCP) but nothing that runs automated containment harnesses in production.
- **Long-form, multi-day agent evaluations are scarce** — most MCP security work is short-burst benchmark attacks; what's missing is multi-day, multi-server endurance testing with real user tasks.
- **Interop landscape (2505.02279) is only partially mapped to A2A/ANP** — next step is running CA-MCP (2601.11595) on real team workflows and comparing token/cost outcomes against baseline MCP.

## License

Public reading list — feel free to fork and extend.
