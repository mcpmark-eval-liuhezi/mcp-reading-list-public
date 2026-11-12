# MCP Papers — Curated Reading List

> **Source of truth:** All titles, authors, arXiv IDs, and submission dates below were taken from each paper's own arXiv abstract page (`arxiv.org/abs/<id>`), not from search snippets.

**Search terms used:** broad `"Model Context Protocol"` scan; targeted security query `"Model Context Protocol" AND (security OR attack OR threat OR sandbox OR privilege)`; targeted broader-picture query `"Model Context Protocol" AND (survey OR "agent architecture" OR "tool use")`. Candidates were filtered to papers genuinely about MCP before opening each on its abstract page.

**Organization:** Security first (6 papers), then the broader picture — surveys, measurement studies, and agent/tool-use architecture (3 papers). Each entry has title, authors, arXiv ID + link, submission date, a 2–3 sentence summary in my own words, and a one-line "why it matters" note. The file closes with a **Gaps & next steps** section.

---

## Part I — Security: Threat Models, Attacks, Sandboxing & Privilege Issues

### 1. SMCP: Secure Model Context Protocol
- **Authors:** Xinyi Hou, Shenao Wang, Yifan Zhang, Ziluo Xue, Yanjie Zhao, Cai Fu, Haoyu Wang
- **arXiv ID:** [arXiv:2602.01129](https://arxiv.org/abs/2602.01129) (cs.CR) — submitted 1 Feb 2026 (v1)
- **Why it matters:** MCP's adoption brings unauthorized access, tool poisoning, prompt injection, privilege escalation, and supply-chain risks that existing targeted countermeasures don't address at a protocol level; SMCP is a concrete design proposal (unified identity management, mutual authentication, security context propagation, fine-grained policy enforcement, audit logging) for closing those gaps.
- **Summary:** This paper introduces SMCP, a protocol-level extension of MCP that adds unified identity management, robust mutual authentication, ongoing security context propagation, fine-grained policy enforcement, and comprehensive audit logging on top of standard MCP. The authors frame MCP's rise as moving agentic LLM systems toward open ecosystems connecting diverse agents, tools, and resources, while flagging new security and privacy risks (unauthorized access, tool poisoning, prompt injection, privilege escalation, supply-chain attacks) that existing research has only touched piecemeal. They present SMCP's main components, show how each reduces risk across the protocol workflow, and illustrate practical examples — arguing for a protocol-level secure foundation rather than per-deployment hacks.

### 2. Systematization of Knowledge: Security and Safety in the Model Context Protocol Ecosystem
- **Authors:** Shiva Gaire, Srijan Gyawali, Saroj Mishra, Suman Niroula, Dilip Thakur, Umesh Yadav
- **arXiv ID:** [arXiv:2512.08290](https://arxiv.org/abs/2512.08290) (cs.CR, cs.AI; v2, last revised 13 Dec 2025; v1 submitted 9 Dec 2025)
- **Why it matters:** It's a SoK that draws the line between *adversarial security threats* (indirect prompt injection, tool poisoning) and *epistemic safety hazards* (alignment failures in distributed tool delegation) — the boundary that's blurring as MCP decouples context from execution.
- **Summary:** This SoK provides a comprehensive taxonomy of risks in the MCP ecosystem, distinguishing adversarial security threats (indirect prompt injection, tool poisoning) from epistemic safety hazards (alignment failures in distributed tool delegation). It analyzes structural vulnerabilities in MCP's core primitives — Resources, Prompts, and Tools — and shows how "context" can be weaponized to trigger unauthorized operations in multi-agent environments. It also surveys state-of-the-art defenses (cryptographic provenance like ETDI, runtime intent verification) and closes with a roadmap for securing the transition from conversational chatbots to autonomous agentic operating systems.

### 3. Beyond the Protocol: Unveiling Attack Vectors in the Model Context Protocol (MCP) Ecosystem
- **Authors:** Hao Song, Yiming Shen, Wenxuan Luo, Leixin Guo, Ting Chen, Jiashui Wang, Beibei Li, Xiaosong Zhang, Jiachi Chen
- **arXiv ID:** [arXiv:2506.02040](https://arxiv.org/abs/2506.02040) (cs.CR, cs.SE; v4, last revised 14 Sep 2025; v1 submitted 31 May 2025)
- **Why it matters:** It's the first end-to-end empirical evaluation of MCP attack vectors, and it shows current audit mechanisms on aggregator platforms are insufficient — malicious servers get uploaded and users struggle to identify them.
- **Summary:** This paper presents the first end-to-end empirical evaluation of attack vectors targeting the MCP ecosystem, identifying four categories: Tool Poisoning Attacks, Puppet Attacks, Rug Pull Attacks, and Exploitation via Malicious External Resources. The authors construct malicious MCP servers, upload them to three widely used MCP aggregation platforms, run a user study with 20 participants, and demonstrate that attacks can trigger harmful actions in the user's local environment (accessing private files, controlling devices to transfer assets). They also lay out four key challenges for the current MCP security ecosystem, underscoring the need for robust mechanisms against malicious MCP servers.

### 4. Breaking the Protocol: Security Analysis of the Model Context Protocol Specification and Prompt Injection Vulnerabilities in Tool-Integrated LLM Agents
- **Authors:** Narek Maloyan, Dmitry Namiot
- **arXiv ID:** [arXiv:2601.17549](https://arxiv.org/abs/2601.17549) (cs.CR, cs.AI; submitted 24 Jan 2026, v1)
- **Why it matters:** It's the first rigorous security analysis of MCP's architectural design itself, proving the weaknesses are structural (not implementation-specific) and proposing a backward-compatible MCPSec extension that cuts attack success from 52.8% to 12.4%.
- **Summary:** This paper delivers the first rigorous security analysis of MCP's architectural design, identifying three fundamental protocol-level vulnerabilities: (1) absence of capability attestation lets servers claim arbitrary permissions, (2) bidirectional sampling without origin authentication enables server-side prompt injection, and (3) implicit trust propagation in multi-server configurations. They implement MCPBench, measuring protocol-specific attack surfaces across 847 attack scenarios on five MCP server implementations, and show MCP's design amplifies attack success by 23–41% vs. non-MCP equivalents. They propose MCPSec, a backward-compatible extension adding capability attestation and message authentication, reducing attack success from 52.8% to 12.4% with median latency overhead of just 8.3ms per message.

### 5. Log-To-Leak: Prompt Injection Attacks on Tool-Using LLM Agents via the Model Context Protocol
- **Authors:** Yuepeng Hu, Chongyu Fan, Sirat Samyoun, Jian Du
- **arXiv ID:** [arXiv:2610.36108](https://arxiv.org/abs/2610.36108) (cs.CR, cs.AI; submitted 26 Oct 2026, v1)
- **Why it matters:** It targets a surface many overlook — natural-language tool descriptions and post-hoc logging metadata — showing ASR of 62.64–100% and arguing for host-controlled authorization on secondary tool calls.
- **Summary:** This paper studies Log-To-Leak, an additive post-hoc logging attack on MCP tool use where an attacker-controlled call is induced after the final legitimate call, with a payload targeting the user query, MCP server name, server response, and agent response. They operationalize the injection via Trigger, Tool Binding, Justification, and Pressure, and evaluate five MCP servers and four LLM agents: Log-To-Leak achieves 62.64–100% attack success rate and 76.55–95.64% conditional logging accuracy, while three evaluated defenses still leave residual ASR above 55% on GitHub MCP with GPT-4o, and an instruction detector flags 85.53% of benign descriptions. The authors conclude that successful task completion can coexist with unauthorized post-hoc disclosure, motivating host-controlled authorization for secondary tool calls.

### 6. Authorization Architectures for Tool-Using AI Agents
- **Authors:** Rakesh Kumar Surapani, Pradeep Kumar Dolabehera Kakitapelli, Arun Morampudi, Praveena Padi
- **arXiv ID:** [arXiv:2609.15906](https://arxiv.org/abs/2609.15906) (cs.CR; submitted 14 Sep 2026, v1; 70 pages, 8 figures, 10 tables)
- **Why it matters:** It proposes a principal hierarchy (human user → operator/deployer → orchestrator agent → sub-agent → tool endpoint) and five layers (identity/credential lifecycle, delegation/scope propagation, runtime enforcement at PEPs, prompt-injection-as-authorization-bypass, and auditability/provenance) — a reference architecture for MCP-era authorization that's missing today.
- **Summary:** This review introduces a principal hierarchy spanning human user, operator/deployer, orchestrator agent, sub-agent, and tool endpoint as an organizing framework, and examines five interdependent layers: agent identity and credential lifecycle; delegation and scope propagation across multi-hop chains; runtime enforcement and just-in-time authorization at policy enforcement points; prompt injection as an authorization bypass that breaks the principal hierarchy; and auditability, provenance, and non-repudiation. Drawing on a structured narrative review of 89 primary sources screened from ~180 candidates (2023–2026), it proposes seven structural requirements, derives a four-layer reference architecture, applies requirements to three deployable reference configurations, and names runtime enforcement and aggregation bounds as the principal unresolved gaps.

---

## Part II — The Broader Picture: Surveys, Measurement, and Agent/Architecture Work

### 7. A survey of agent interoperability protocols: Model Context Protocol (MCP), Agent Communication Protocol (ACP), Agent-to-Agent Protocol (A2A), and Agent Network Protocol (ANP)
- **Authors:** Abul Ehtesham, Aditi Singh, Gaurav Kumar Gupta, Saket Kumar
- **arXiv ID:** [arXiv:2505.02279](https://arxiv.org/abs/2505.02279) (cs.AI; v2, last revised 23 May 2025; v1 submitted 4 May 2025)
- **Why it matters:** It positions MCP against its main peer protocols (ACP, A2A, ANP) and gives a phased adoption roadmap: MCP first for tool access, then ACP for structured messaging, A2A for collaborative task execution, and ANP for decentralized marketplaces.
- **Summary:** This survey examines four emerging agent communication protocols — MCP, ACP, A2A, and ANP — each addressing interoperability in different deployment contexts. MCP provides a JSON-RPC client-server interface for secure tool invocation and typed data exchange; ACP defines a general-purpose RESTful-HTTP protocol with MIME-typed multipart messages, session management, routing, and DID integration; A2A enables peer-to-peer task delegation via capability-based Agent Cards; and ANP supports open network agent discovery using W3C DIDs and JSON-LD graphs. The protocols are compared across interaction modes, discovery mechanisms, communication patterns, and security models, and the authors propose a phased adoption roadmap beginning with MCP for tool access and extending to ANP for decentralized agent marketplaces.

### 8. A Measurement Study of Model Context Protocol Ecosystem
- **Authors:** Hechuan Guo, Yongle Hao, Yue Zhang, Minghui Xu, Peizhuo Lv, Jiezhi Chen, Xiuzhen Cheng
- **arXiv ID:** [arXiv:2509.25292](https://arxiv.org/abs/2509.25292) (cs.CY, cs.AI; v3, last revised 15 Nov 2025; v1 submitted 29 Sep 2025)
- **Why it matters:** It's the first large-scale empirical view of the MCP ecosystem (17,630 raw entries, 8,401 valid projects), showing more than half of listed projects are invalid or low-value and flagging dependency monocultures and maintenance risk.
- **Summary:** This paper presents the first large-scale empirical study of the MCP ecosystem, designing and implementing MCPCrawler, a systematic measurement framework that collects and normalizes data from six major markets over a 14-day campaign, aggregating 17,630 raw entries of which 8,401 valid projects (8,060 servers and 341 clients) were analyzed. The results reveal that more than half of listed projects are invalid or low-value, that servers face structural risks including dependency monocultures and uneven maintenance, and that clients exhibit a transitional phase in protocol and connection patterns. Together these findings give the first evidence-based view of MCP's trajectory, risks, and future direction.

### 9. Information Fidelity in Tool-Using LLM Agents: A Martingale Analysis of the Model Context Protocol
- **Authors:** Flint Xiaofeng Fan, Cheston Tan, Roger Wattenhofer, Yew-Soon Ong
- **arXiv ID:** [arXiv:2602.13320](https://arxiv.org/abs/2602.13320) (cs.AI; submitted 10 Feb 2026, v1; extended abstract accepted at AAMAS 2026)
- **Why it matters:** It's the first theoretical framework for error accumulation in MCP agents, proving distortion grows linearly with high-probability deviations bounded by O(√T), with empirical guidance (semantic weighting cuts distortion 80%, re-grounding every ~9 steps suffices).
- **Summary:** This paper introduces the first theoretical framework for analyzing error accumulation in MCP agents, proving that cumulative distortion exhibits linear growth with high-probability deviations bounded by O(√T), which rules out exponential failure modes and ensures predictable system behavior. They develop a hybrid distortion metric combining discrete fact matching with continuous semantic similarity, establish martingale concentration bounds on error propagation through sequential tool interactions, and validate predictions on Qwen2-7B, Llama-3-8B, and Mistral-20B-7B, where empirical distortion tracks the linear trend within O(√T) envelopes. Practical takeaways include that semantic weighting reduces distortion by 80% and periodic re-grounding roughly every 9 steps suffices for error control, translated into deployment principles for trustworthy agent systems.

---

## Gaps & Next Steps

Reading the security papers above (SMCP, the SoK, "Beyond the Protocol," "Breaking the Protocol," Log-To-Leak, and Authorization Architectures) plus the ecosystem measurement study, three gaps stand out for our project: **(1) Runtime sandboxing inside a running MCP client** remains an underexplored first-class design goal — none of the surveyed papers propose containment harnesses that measure blast radius for in-session privilege escalation, so our next step is building one against the MCP-38 attack categories and validating against Aegis OS-style runtimes; **(2) long-horizon, multi-turn evaluation** of MCP agents under realistic tooling is still thin, so we should extend the martingale error-bounds work (2602.13320) to multi-session deployments with periodic re-grounding; and **(3) self-hosted vs. remote server coverage** is uneven in the current literature, so our next step is a contained benchmark comparing local MCP servers (where we control the sandbox) against remote aggregator-hosted ones, informed by the MCPCrawler ecosystem data in 2509.25292 and the runtime-enforcement gaps flagged in 2609.15906.
