# MCP Reading List

A public, curated arXiv reading list on the **Model Context Protocol (MCP)** — the open standard for wiring LLMs up to tools and data sources. Security is the priority: threat models, attacks, sandboxing, and privilege issues come first, followed by the broader picture (surveys, ecosystem measurement, and agent/tool-use architecture work built around MCP).

## What's in this repo

- **[`notes/mcp-papers.md`](notes/mcp-papers.md)** — the full reading list. It's organized in two sections: **Security papers** first (4 papers: the foundational threat-taxonomy survey, a modern SoK on security & safety, an empirical study of MCP attack vectors, and the MCPSecBench evaluation framework), then **Broader picture** papers (a survey positioning MCP against ACP/A2A/ANP, a large-scale measurement study of the MCP ecosystem, and a production deployment playbook). Each entry includes title, authors, arXiv ID/link, submission date, a 2–3 sentence summary, and a one-line "why it matters" note. The file closes with a **Gaps & Next Steps** paragraph.

## Quick start

1. Read `notes/mcp-papers.md` top to bottom — security papers (1–4) first, then the broader picture (5–7).
2. Start with [arXiv:2503.23278](https://arxiv.org/abs/2503.23278) (MCP: Landscape, Security Threats, and Future Research Directions) as your single entry point for the threat taxonomy.
3. For empirical evidence that current mitigations are weak, see [arXiv:2508.13220](https://arxiv.org/abs/2508.13220) (MCPSecBench).
4. For a reality check on ecosystem health before信任 any MCP adoption numbers, see [arXiv:2509.25292](https://arxiv.org/abs/2509.25292) (A Measurement Study of the MCP Ecosystem).

## Search terms used

- `"Model Context Protocol"` (broad)
- `"Model Context Protocol" AND (security OR attack OR threat OR sandbox OR privilege)` (security-focused)
- `"Model Context Protocol" AND (survey OR "agent architecture" OR "tool use" OR "LLM agents")` (surveys & architectures)

 papers were shortlisted from those results and their details (title, authors, arXiv ID, submission date, summary) were verified on their arXiv abstract pages.

## License

Public reading list — feel free to fork and extend.
