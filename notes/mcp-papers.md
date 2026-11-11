# MCP Reading List — Curated Papers

**Search terms used:** `"Model Context Protocol"` (broad); `"Model Context Protocol" AND (security OR attack OR threat OR sandbox OR privilege)` (security-focused); `"Model Context Protocol" AND (survey OR architecture OR "agent tool use" OR "tool calling")` (surveys & architectures). All entries below were shortlisted from local arXiv mirror searches, then each paper's **own arXiv abstract page** was opened to confirm exact title, authors, arXiv ID, and submission date (not from a search snippet).

Eight papers, security first.

---

## Part I — Security: threat models, attacks, and safeguards

### 1. Model Context Protocol (MCP): Landscape, Security Threats, and Future Research Directions
- **Authors:** Xinyi Hou, Yanjie Zhao, Shenao Wang, Haoyu Wang
- **arXiv ID:** [2503.23278](https://arxiv.org/abs/2503.23278) (`cs.CR` / `cs.AI`, current version v3)
- **Submitted:** 30 Mar 2025 (v1); last revised 7 Oct 2025 (v3)
- **Summary:** This is the foundational MCP security paper from the Tsinghua / Zhejiang security group. It first defines the full lifecycle of an MCP server (created → deployed → operated → maintained) broken into 16 activities, then builds a threat taxonomy across four attacker types (malicious developers, external attackers, malicious users, and security flaws) covering 16 concrete threat scenarios, validated with real-world case studies. It closes with fine-grained, phase-specific safeguards and an outlook on standardizing trust boundaries in tool-augmented AI. **Why it matters:** it's the best available taxonomy for reasoning about MCP risk before you design any integration.

### 2. Systematization of Knowledge (SoK): Security and Safety in the Model Context Protocol Ecosystem
- **Authors:** Shiva Gaire, Srijan Gyawali, Saroj Mishra, Suman Niroula, Dilip Thakur, Umesh Yadav
- **arXiv ID:** [2512.08290](https://arxiv.org/abs/2512.08290) (`cs.CR` / `cs.AI`, current version v2)
- **Submitted:** 9 Dec 2025 (v1); last revised 13 Dec 2025 (v2). All authors contributed equally.
- **Summary:** A SoK that draws a sharp distinction between *adversarial security threats* (indirect prompt injection, tool poisoning) and *epistemic safety hazards* (hallucination-style alignment failures when context is delegated across agents). It analyzes structural vulnerabilities in the three MCP primitives — Resources, Prompts, and Tools — and shows how "context" can be weaponized to trigger unauthorized operations in multi-agent settings. It surveys defenses from cryptographic provenance (ETDI) to runtime intent verification, and ends with a roadmap for moving from chatbots to autonomous agentic operating systems. **Why it matters:** it reframes MCP risk as both a security and a safety problem, which changes how you evaluate an MCP deployment.

### 3. Breaking the Protocol: Security Analysis of the Model Context Protocol Specification and Prompt Injection Vulnerabilities in Tool-Integrated LLM Agents
- **Authors:** Narek Maloyan, Dmitry Namiot
- **arXiv ID:** [2601.17549](https://arxiv.org/abs/2601.17549) (`cs.CR` / `cs.AI`, v1)
- **Submitted:** 24 Jan 2026
- **Summary:** The first rigorous security analysis of the MCP *specification itself* (not just implementations). It identifies three protocol-level defects: (1) no capability attestation, so servers can claim arbitrary permissions; (2) bidirectional sampling without origin authentication, enabling server-side prompt injection; and (3) implicit trust propagation in multi-server setups. They build **MCPBench**, measure 847 attack scenarios across five MCP servers, and show MCP's architecture amplifies attack success by 23–41% vs. non-MCP equivalents. They propose **MCPSec**, a backward-compatible extension adding capability attestation and message authentication that cuts success rates from 52.8% to 12.4% at ~8.3ms median latency overhead. **Why it matters:** it proves MCP's weaknesses are architectural, not implementation-specific — protocol-level remediation is required.

### 4. MCPSecBench: A Systematic Security Benchmark and Playground for Testing Model Context Protocols
- **Authors:** Yixuan Yang, Cuifeng Gao, Daoyuan Wu, Yufan Chen, Yingjiu Li, Shuai Wang (Lingnan University)
- **arXiv ID:** [2508.13220](https://arxiv.org/abs/2508.13220) (`cs.CR` / `cs.AI`, current version v3)
- **Submitted:** 17 Aug 2025 (v1); last revised 12 Feb 2026 (v3). Code: [github.com/AIS2Lab/MCPSecBench](https://github.com/AIS2Lab/MCPSecBench)
- **Summary:** Formalization of what a *secure* MCP server requires, plus a new MCP security taxonomy extending prior models with protocol-level and host-side threats — 17 attack types across 4 surfaces. MCPSecBench is a modular playground integrating prompt datasets, MCP servers, clients, attack scripts, a GUI test harness, and protections, runnable across three major MCP platforms. Their empirical evaluation found every attack surface yields successful compromises on Claude, OpenAI, and Cursor, and that existing protections average <30% effectiveness. **Why it matters:** it's the first standardized benchmark for measuring MCP security across all protocol layers, and the open-source tooling lets you reproduce these results.

### 5. Enhancing Model Context Protocol (MCP) with Context-Aware Server Collaboration (CA-MCP)
- **Authors:** Meenakshi Amulya Jayanti, X.Y. Han
- **arXiv ID:** [2601.11595](https://arxiv.org/abs/2601.11595) (`cs.DC` / `cs.LG` / `cs.SE`, current version v2)
- **Submitted:** 6 Jan 2026 (v1); last revised 22 Jan 2026 (v2)
- **Summary:** Extends vanilla MCP, where agents/models/servers are stateless and hear nothing about a global context. CA-MCP introduces a Shared Context Store (SCS) that specialized MCP servers read from and write to, so they coordinate autonomously in real time and maintain continuity across task executions without repeated prompting. Experiments on TravelPlanner and REALM-Bench show statistically significant gains: fewer LLM calls and fewer response failures on unsatisfied task conditions. **Why it matters:** it's the best available take on where MCP architecture is heading — shared state and context management are the next frontier, and this paper measures the payoff.

---

## Part II — The broader picture: surveys, measurements, and agent architectures

### 6. A survey of agent interoperability protocols: MCP, ACP, A2A, and ANP
- **Authors:** Abul Ehtesham, Aditi Singh, Gaurav Kumar Gupta, Saket Kumar
- **arXiv ID:** [2505.02279](https://arxiv.org/abs/2505.02279) (`cs.AI`, current version v2)
- **Submitted:** 4 May 2025 (v1); last revised 23 May 2025 (v2)
- **Summary:** A comparative survey of the four emerging agent interoperability protocols. MCP gives a JSON-RPC client-server interface for secure tool invocation and typed data exchange; ACP is a lightweight, runtime-independent RESTful HTTP protocol with MIME multipart messages, session management, and DID integration; A2A enables peer-to-peer task delegation via capability-based Agent Cards for enterprise workflows; ANP supports decentralized agent discovery using W3C DIDs and JSON-LD graphs. It proposes a phased adoption roadmap: MCP first for tool access, then ACP for structured messaging, A2A for collaborative task execution, and ANP for decentralized marketplaces. **Why it matters:** MCP is not a solo standard — this survey tells you what it does and doesn't cover relative to ACP/A2A/ANP, which you'll need for any multi-protocol agent strategy.

### 7. A Measurement Study of Model Context Protocol Ecosystem
- **Authors:** Hechuan Guo, Yongle Hao, Yue Zhang, Minghui Xu, Peizhuo Lv, Jiezhi Chen, Xiuzhen Cheng
- **arXiv ID:** [2509.25292](https://arxiv.org/abs/2509.25292) (`cs.CY` / `cs.AI`, current version v3)
- **Submitted:** 29 Sep 2025 (v1); last revised 15 Nov 2025 (v3)
- **Summary:** The first large-scale empirical study of the live MCP ecosystem. MCPCrawler sampled 6 major markets over 14 days, aggregating 17,630 raw entries and analyzing 8,401 valid projects (8,060 servers, 341 clients). Findings: more than half of listed projects are invalid or low-value, servers face structural risks like dependency monocultures and uneven maintenance, and clients are in a transitional phase with fragmented protocol/connection patterns. **Why it matters:** it's the evidence base for triage — before trusting a marketplace, check whether the server is legitimate, maintained, and not a supply-chain risk.

### 8. Advancing Multi-Agent Systems Through Model Context Protocol: Architecture, Implementation, and Applications
- **Author:** Naveen Krishnan
- **arXiv ID:** [2504.21030](https://arxiv.org/abs/2504.21030) (`cs.MA` / `cs.AI`, v1)
- **Submitted:** 26 Apr 2025
- **Summary:** A single-author treatment of MCP as the glue for multi-agent systems, targeting the classic problems of context management, coordination efficiency, and scalable operation. It develops a unified theoretical foundation, advanced context management techniques, and scalable coordination patterns, then reports implementation case studies in enterprise knowledge management, collaborative research, and distributed problem-solving, with a benchmark/task methodology purpose-built for multi-agent evaluation. **Why it matters:** it's the most direct architecture reference for building multi-agent systems *on* MCP rather than beside it.

---

## Gaps & next steps

The field is moving fast, but real gaps remain.

**(1) No real runtime sandboxing inside a running MCP client.** We have threat taxonomies (MCP-38 [2603.18063], 2503.23278) and hardening proposals (SMCP [2602.01129], MCPSec [2601.17549]), but nothing that runs automated containment harnesses against those categories in production. The next step is building a sandbox that ingests an untrusted MCP server process and measures blast radius against the MCP-38 taxonomy.

**(2) Long-form, multi-day agent evaluations are scarce.** Most MCP security work is short-burst benchmark attacks (e.g., MCPSecBench's shouting-and-clicking attacks). What's missing is multi-day, multi-server endurance testing with real user tasks, which is where prompt-injection and tool-poisoning risks actually compound.

**(3) The interop survey landscape (2505.02279) is only partially mapped to A2A/ANP.** Our next step is to run CA-MCP (2601.11595) on real team workflows, compare token and cost outcomes against baseline MCP, and document what shared-context design patterns survive in production.

---

## Verification note

Every entry above was re-checked against the paper's own arXiv abstract page (arxiv.org/abs/<id>) on the day this commit was made: exact title, author list, arXiv ID, and submission date all match the pages fetched directly. The broad mirror search, the security-focused mirror search, and the surveys/architectures mirror search were the shortlisting inputs; the abstract pages are the source of truth for the metadata in this file.
