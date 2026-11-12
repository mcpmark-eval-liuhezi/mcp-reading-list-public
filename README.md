# MCP Reading List

A curated arXiv reading list for our research project on the **Model Context Protocol (MCP)** — the open standard for wiring LLMs up to tools and data sources.

**Priority focus:** security (threat models, attacks, sandboxing and privilege issues), followed by the broader picture: surveys, architectures, and agent/tool-use work built around MCP.

## What's in here

The full deliverable is [`notes/mcp-papers.md`](notes/mcp-papers.md) — **nine arXiv papers that are genuinely about MCP**, each shortlisted from local arXiv mirror searches and then each opened on its arXiv abstract page for exact title, authors, arXiv ID, submission date, and a fresh 2–3 sentence summary in my own words (not from search snippets).

The list is organized **security first**: Part I has six papers on the threat landscape — a protocol-level secure extension ([SMCP, 2602.01129](https://arxiv.org/abs/2602.01129)), a systematization-of-knowledge SoK separating adversarial threats from epistemic safety hazards ([2512.08290](https://arxiv.org/abs/2512.08290)), an end-to-end empirical attack-vector study ([2506.02040](https://arxiv.org/abs/2506.02040)), a specification-level security analysis with MCPBench ([2601.17549](https://arxiv.org/abs/2601.17549)), a post-hoc logging prompt-injection attack ([2610.36108](https://arxiv.org/abs/2610.36108)), and a principal-hierarchy authorization architecture ([2609.15906](https://arxiv.org/abs/2609.15906)). Part II covers the broader picture: a survey comparing MCP against ACP/A2A/ANP ([2505.02279](https://arxiv.org/abs/2505.02279)), a large-scale ecosystem measurement study ([2509.25292](https://arxiv.org/abs/2509.25292)), and a theoretical martingale analysis of error accumulation in MCP agents ([2602.13320](https://arxiv.org/abs/2602.13320)).

Every entry includes: title, authors, arXiv ID + link, submission date, a 2–3 sentence summary in my own words of what the paper contributes, and a one-line "why it matters" note. The file closes with a **Gaps & next steps** section covering runtime sandboxing inside a running MCP client, in-session privilege escalation, long-horizon multi-turn evaluation, and self-hosted vs. remote server coverage.

## How it was built

- **Searches run:** broad `"Model Context Protocol"` scan (1.37M+ results on arXiv; top 15 reviewed); targeted security query `"Model Context Protocol" AND (security OR attack OR threat OR sandbox OR privilege)` (226 results; top 10 reviewed); targeted broader-picture query `"Model Context Protocol" AND (survey OR "agent architecture" OR "tool use")` (561 results; top 10 reviewed). Candidates were filtered to papers genuinely about MCP before opening each on its abstract page.
- **Verification:** canonical title, authors, ID, and submission date were taken from each paper's own arXiv abstract page (`arxiv.org/abs/<id>`), not from search snippets. Papers that did not survive abstract-page verification were dropped from the shortlist.
- Backup scholarly sanity checks were attempted as a fallback; the arXiv mirror plus each paper's own abstract page remained the source of truth.

## Suggested next steps

1. Read Part I in order — [2602.01129](https://arxiv.org/abs/2602.01129) is the protocol-level hardening blueprint (capability attestation, mutual auth, audit logging), [2506.02040](https://arxiv.org/abs/2506.02040) is the empirical baseline for why aggregator-hosted servers are dangerous, and [2601.17549](https://arxiv.org/abs/2601.17549) proves the fixes (MCPSec) are backward-compatible with low latency overhead.
2. Move to Part II for the ecosystem and theory picture: [2505.02279](https://arxiv.org/abs/2505.02279) for where MCP fits among ACP/A2A/ANP, [2509.25292](https://arxiv.org/abs/2509.25292) for evidence on server quality, and [2602.13320](https://arxiv.org/abs/2602.13320) for theoretical guarantees on error accumulation in sequential tool use.
3. Our biggest gap: no paper proposes *runtime sandboxing inside a running MCP client* as a first-class design goal — the next step is building a containment harness against the MCP-38 attack categories and measuring blast radius in production, informed by the authorization hierarchy in [2609.15906](https://arxiv.org/abs/2609.15906) and the ecosystem risks in [2509.25292](https://arxiv.org/abs/2509.25292).
