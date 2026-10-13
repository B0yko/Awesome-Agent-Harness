<div align="center">

[English](README.md) | [中文](README_zh.md)

# Agent Harness for Large Language Model Agents: A Survey

[![GitHub Stars](https://img.shields.io/github/stars/Gloriaameng/Awesome-Agent-Harness?style=social)](https://github.com/Gloriaameng/Awesome-Agent-Harness)
[![License](https://img.shields.io/badge/License-CC--BY--4.0-blue.svg)](license)
[![Resource Index](https://img.shields.io/badge/Resource%20Index-2026.10-0b7285)](#resource-and-paper-status)
[![Paper](https://img.shields.io/badge/Paper-v4-orange)](./Agent_Harness_for_LLM_Agents__A_Survey__v4.pdf)
[![DOI](https://img.shields.io/badge/Archived%20DOI-v3-blue)](https://doi.org/10.20944/preprints202604.0428.v3)

</div>

<p align="center">
  <img src="assets/architecture_diagram.png" width="720" alt="H=(E,T,C,S,L,V) six-component analytical framework"/>
</p>

## Resource and Paper Status

| Artifact | Current version | Date / cutoff | Notes |
|---|---|---|---|
| Resource index | **2026.10** | Evidence reviewed through **2026-10-12** | README system and benchmark landscape |
| Repository paper | **v4** | 2026-04-14 | [PDF](./Agent_Harness_for_LLM_Agents__A_Survey__v4.pdf) |
| Archived preprint | **v3** | 2026-04-09 | [DOI record](https://doi.org/10.20944/preprints202604.0428.v3) |
| Paper v5 | In revision | — | The manuscript is being restructured and is not yet released |

> Agent behavior is produced by a **model–harness–environment configuration**. This resource treats the harness as a consequential and frequently under-reported co-determinant of observed capability, reliability, cost, and safety.

The survey uses **H = (E, T, C, S, L, V)** as an analytical decomposition of six governance functions repeatedly visible across public systems: execution loop, tool registry, context manager, state store, lifecycle hooks, and evaluation interface. Component coverage describes architecture; it does not by itself measure product maturity, quality, or adoption.

📄 **[Read Paper v4](./Agent_Harness_for_LLM_Agents__A_Survey__v4.pdf)** · 🌐 **[Archived preprint v3](https://www.preprints.org/manuscript/202604.0428/v3)**
✉️ Corrections and suggestions: gloriamenng@gmail.com; wangyanan@mail.dlut.edu.cn; chenliyi@xiaohongshu.com

If you cite the currently archived preprint, use:

```bibtex
@article{meng2026agentharness,
  title     = {Agent Harness for Large Language Model Agents: A Survey},
  author    = {Meng, Qianyu and Wang, Yanan and Chen, Liyi and Wu, Wei and
               Li, Yihang and Jiang, Wenyuan and Wang, Qimeng and
               Lu, Chengqiang and Gao, Yan and Wu, Yi and Hu, Yao},
  year      = {2026},
  doi       = {10.20944/preprints202604.0428.v3},
  url       = {https://www.preprints.org/manuscript/202604.0428/v3},
  publisher = {Preprints}
}
```

## 🆕 News & Updates

- **[2026-10-13]** Resource Index 2026.10: rebuilt the 20-system comparison set, separated task environments from harness benchmarks, and added harness evolution and security evaluation.
- **[2026-04-14]** Paper v4 and citation update.
- **[2026-04-09]** Archived preprint v3 released.
- **[2026-04-03]** Initial release.

## Table of Contents

- [Resource and Paper Status](#resource-and-paper-status)
- [Overview](#overview)
- [Historical Timeline](#historical-timeline)
- [Core System Matrix](#core-system-matrix)
- [Benchmark Map](#benchmark-map)
- [Paper List](#paper-list)
  - [System Directory](#system-directory)
- [Citation](#citation)
- [Update Log](#update-log)

## Overview

LLM agents do not act through model inference alone. An execution harness assembles observations, invokes the model, routes tools, persists state, applies policies, records trajectories, and determines when work stops or recovers. Reporting only the model therefore hides a material part of the evaluated system.

| Component | Symbol | Governance function |
|---|:---:|---|
| Execution Loop | **E** | Turn/step control, termination, retry and recovery |
| Tool Registry | **T** | Typed tools, routing, validation and result handling |
| Context Manager | **C** | Prompt assembly, retrieval, compaction and salience |
| State Store | **S** | Cross-turn/session persistence, checkpoints and recovery |
| Lifecycle Hooks | **L** | Authentication, approval, policy, instrumentation and interception |
| Evaluation Interface | **V** | Trajectories, intermediate state, outcome signals and experiment integration |

The index combines peer-reviewed research, preprints, first-party technical documentation, source code, and clearly identified practitioner reports. Matrix cells are evidence-coded against public first-party material. Stars and popularity are not component evidence and are not used as maturity scores.

## Historical Timeline

<p align="center">
  <img src="assets/timeline.png" width="720" alt="Historical Evolution of Agent Harnesses"/>
</p>

| Year | Milestone | Significance |
|------|-----------|--------------|
| 1997–2005 | JUnit, TestNG, xUnit family | Software test harness paradigm; standardized observe-assert lifecycle |
| 2016 | OpenAI Gym (Brockman et al.) | RL environment harness; step/reset API becomes canonical interface |
| 2022 Nov | ChatGPT public release; LangChain emerges | LLM-native agent frameworks begin; tool-use as first-class citizen |
| 2023 | ReAct, Toolformer, MemGPT, Reflexion, Voyager, AutoGPT | Core agent patterns: reasoning-acting, memory, reflection, skill accumulation |
| 2023 | CAMEL, ChatDev, Generative Agents | Multi-agent coordination; social simulation harnesses |
| 2023 | AgentBench, SWE-bench | Agent evaluation infrastructure emerges |
| 2024 | MetaGPT, WebArena, ToolLLM, SWE-agent, OSWorld | Full-stack harnesses; real-world environment benchmarks |
| 2024 | CodeAct, LATS, Tree of Thoughts | Structured action spaces; search-augmented planning |
| 2024 Nov | Anthropic releases MCP protocol | Tool↔harness interface standardization |
| 2025 | HAL, AIOS, LangGraph | Evaluation infrastructure, agent operating systems, and stateful graph runtimes |
| 2025 | Google releases A2A protocol | Agent↔agent interface standardization |
| 2025 | MemoryOS, AgentBound† | Memory abstractions and runtime safety enforcement |
| 2026 Jan–Oct | SkillsBench†, Harness-Bench, EVOHARNESSBENCH, HarnessRisk, HarnessSecurity-Bench, LoopsBench, SCLATE | Skill evaluation, direct harness comparison, evolution, lifecycle risk, long-horizon loops, and auditable runtime infrastructure |

*† preprint*

---

## Core System Matrix

The core comparison set contains **20 systems** selected for architectural relevance, public evidence, active maintenance, or representation of a distinct harness route. Ratings describe documented component coverage at the evidence cutoff; they are not quality rankings.

**Evidence legend:** ● Full — built in and documented · ◐ Partial — limited, optional, or provided through an official extension · ○ Absent — first-party material explicitly excludes it · ? Unverified — public evidence is insufficient.

| Category | System | E | T | C | S | L | V |
|---|---|:---:|:---:|:---:|:---:|:---:|:---:|
| Anchor coding harnesses | **Claude Code** | ● | ● | ● | ◐ | ● | ◐ |
| Anchor coding harnesses | **Codex** | ● | ● | ● | ● | ● | ◐ |
| Anchor coding harnesses | **DeepSeek Harness** | ● | ● | ● | ● | ● | ◐ |
| Anchor coding harnesses | **OpenClaw** | ● | ● | ● | ● | ● | ◐ |
| Coding harnesses | **Gemini CLI** | ● | ● | ● | ● | ● | ◐ |
| Coding harnesses | **OpenCode** | ● | ● | ● | ● | ● | ◐ |
| Coding harnesses | **Goose** | ● | ● | ◐ | ◐ | ● | ◐ |
| Coding harnesses | **Grok Build** | ● | ● | ● | ● | ● | ◐ |
| Coding harnesses | **Cline** | ● | ● | ◐ | ● | ● | ◐ |
| Coding harnesses | **OpenHands** | ● | ● | ● | ● | ● | ◐ |
| Coding harnesses | **Deep Agents** | ● | ● | ● | ● | ● | ● |
| Coding harnesses | **Prime Agent** | ● | ● | ● | ● | ● | ◐ |
| General runtimes | **OpenAI Agents SDK** | ● | ● | ● | ● | ● | ● |
| General runtimes | **Google ADK** | ● | ● | ● | ● | ● | ● |
| General runtimes | **Microsoft Agent Framework** | ● | ● | ● | ● | ● | ● |
| General runtimes | **LangGraph** | ● | ● | ● | ● | ◐ | ◐ |
| Other representative routes | **DeerFlow** | ● | ● | ● | ● | ● | ◐ |
| Other representative routes | **AIOS** | ● | ● | ● | ● | ● | ◐ |
| Other representative routes | **AOHP** | ● | ● | ● | ● | ● | ◐ |
| Other representative routes | **Omnigent** | ● | ● | ◐ | ● | ● | ◐ |

The matrix treats one first-party product or repository as one system boundary. Security layers, benchmarks, capability modules, and third-party extensions are not merged into a system merely to make its row more complete.

## Benchmark Map

Harness research needs to separate the object being varied. A task environment asks whether an agent completes a task; a harness benchmark holds more of the model, task, environment, or budget fixed and measures how runtime design changes behavior.

### 1. Harness effect

- [Harness-Bench](https://arxiv.org/abs/2605.27922): compares model–harness configurations under shared sandboxed tasks, environments, budgets, and evaluation.
- [Beyond the Model](https://arxiv.org/abs/2609.32459): studies tool registries, context compression, planning, subagents, and lazy skills through component changes.
- [LongHarness Bench](https://arxiv.org/abs/2609.38137): evaluates the accuracy and efficiency of long-context harnesses.
- [Harness the Memory](https://arxiv.org/abs/2608.15008): compares memory substrates in a shared harness across models and task suites.

### 2. Harness evolution and runtime self-improvement

- [EVOHARNESSBENCH](https://arxiv.org/abs/2609.04280): evaluates retention and adaptation as tools, skills, and agents change over time.
- [SkillOpt](https://arxiv.org/abs/2605.23904): proposes bounded skill edits from scored trajectories with held-out acceptance gates.
- [SCLATE](https://arxiv.org/abs/2609.32391): places sessions, scheduled tasks, and memory consolidation on a shared event timeline.
- [TaoLive](https://arxiv.org/abs/2608.15763), [Meta-Harness](https://arxiv.org/abs/2603.28052), [AutoHarness](https://arxiv.org/abs/2603.03329), and [VeRO](https://arxiv.org/abs/2602.22480) examine harness-aware training, harness optimization, generated harnesses, and agents evaluating agents.

### 3. Lifecycle, security, and audit

- [HarnessRisk](https://arxiv.org/abs/2608.17597): tests configuration, extension, runtime, persistence, action, and recovery phases.
- [HarnessSecurity-Bench](https://arxiv.org/abs/2610.07639): measures utility and attack effects across real coding harnesses and permission settings.
- [Hearsay](https://arxiv.org/abs/2609.32495): tests whether harness-produced records support independent audit.
- [SandboxEscapeBench](https://arxiv.org/abs/2603.02277): tests whether models can discover and exploit deliberately seeded misconfigurations and vulnerabilities in nested sandboxes.

### 4. Long-horizon loops and recovery

- [LoopsBench](https://arxiv.org/abs/2608.00267), [Long-Horizon-Terminal-Bench](https://arxiv.org/abs/2607.08964), [SWE-Chain](https://arxiv.org/abs/2605.14415), and [ChainSWE](https://arxiv.org/abs/2607.02606) evaluate sustained development, accumulated state, regression obligations, and dependent changes.
- [Hell or High Water](https://arxiv.org/abs/2508.11027) evaluates recovery from external failures.

### 5. Protocol and tool substrate

- [DynamicMCPBench](https://arxiv.org/abs/2607.20531), [MCP-Bench](https://arxiv.org/abs/2508.20453), [MCP-AgentBench](https://arxiv.org/abs/2509.09734), and [MCPAgentBench](https://arxiv.org/abs/2512.24565) test live/stateful MCP use, end-to-end outcomes, and tool discrimination.

### 6. Evaluation infrastructure

- [AgentCompass](https://arxiv.org/abs/2607.13705) separates benchmark, harness, and environment.
- [Harbor](https://github.com/harbor-framework/harbor) provides interchangeable agents, models, datasets, container environments, traces, and parallel rollouts.
- [HAL](https://arxiv.org/abs/2510.11977) provides unified execution and leaderboard infrastructure.

### Task environments and deployment benchmarks

[AgencyBench](https://arxiv.org/abs/2601.11044), [ClawBench](https://github.com/TIGER-AI-Lab/ClawBench), [OSWorld](https://github.com/xlang-ai/OSWorld), [WebArena](https://github.com/web-arena-x/webarena), [GAIA](https://arxiv.org/abs/2311.12983), and [SWE-bench](https://github.com/swe-bench/SWE-bench) remain important task environments. Results on these benchmarks should identify the model, harness, environment, budget, and evaluation version together.

---

## Paper List

### Historical Lineages

#### Software Test Harnesses (1990s–2000s)

- <u>JUnit</u>: **"JUnit: A Cook's Tour"**. *Beck & Gamma.* Java Report, 4(5), May 1999. [[Archived article](https://web.archive.org/web/20200101000000/http://junit.sourceforge.net/doc/cookstour/cookstour.htm)]

#### RL Environment Harnesses (2016–2022)

- <u>OpenAI Gym</u>: **"OpenAI Gym"**. *Brockman et al.* arXiv 2016. [[Paper](https://arxiv.org/abs/1606.01540)] [[Code](https://github.com/openai/gym)]
- <u>Gymnasium</u>: **"Gymnasium: A Standard Interface for Reinforcement Learning Environments"**. *Towers et al.* NeurIPS 2025. [[Paper](https://arxiv.org/abs/2407.17032)] [[Code](https://github.com/Farama-Foundation/Gymnasium)]

#### Early LLM Agent Frameworks (2023–2024)

- <u>ReAct</u>: **"ReAct: Synergizing Reasoning and Acting in Language Models"**. *Yao et al.* ICLR 2023. [[Paper](https://arxiv.org/abs/2210.03629)] [[Code](https://github.com/ysymyth/ReAct)]
- <u>Toolformer</u>: **"Toolformer: Language Models Can Teach Themselves to Use Tools"**. *Schick et al.* NeurIPS 2023. [[Paper](https://arxiv.org/abs/2302.04761)]
- <u>AutoGPT</u>: **"Auto-GPT: An Autonomous GPT-4 Experiment"**. *Gravitas et al.* GitHub 2023. [[Code](https://github.com/Significant-Gravitas/AutoGPT)]
- <u>BabyAGI</u>: **"BabyAGI"**. *Nakajima.* GitHub 2023. [[Code](https://github.com/yoheinakajima/babyagi)]
- <u>HuggingGPT</u>: **"HuggingGPT: Solving AI Tasks with ChatGPT and Its Friends in Hugging Face"**. *Shen et al.* NeurIPS 2023. [[Paper](https://arxiv.org/abs/2303.17580)]
- <u>LangChain</u>: **"LangChain: Building Applications with LLMs through Composability"**. *Chase et al.* GitHub 2022. [[Code](https://github.com/langchain-ai/langchain)]

---

### System Directory

#### Four anchor systems

**Claude Code.** Claude Code connects repository inspection, edits, command execution, web and MCP tools, subagents, skills, hooks, permission rules, checkpoints, and session continuation through a shared coding-agent loop. Its context layer combines project instructions, conversation state, tool results, and compaction. Hooks and permission modes place policy decisions on the execution path, while transcripts and observability integrations expose what the runtime did. In this survey it represents a vertically integrated coding harness whose CLI and Agent SDK expose related runtime capabilities. [[Code](https://github.com/anthropics/claude-code)] [[Agent SDK](https://github.com/anthropics/claude-agent-sdk-python)]

**Codex.** Codex connects repository exploration, editing, command execution, verification, sandboxing, approvals, MCP tools, skills, subagents, and resumable threads through a shared agent runtime. Its execution loop coordinates model requests and tool results; context compaction governs long histories; persisted rollouts and thread state carry work across sessions; structured events and traces support inspection and evaluation. Approval decisions and sandbox constraints remain explicit runtime controls. The CLI, IDE integration, app, and cloud execution surfaces are treated as interfaces to the same harness family rather than separate systems. [[Code](https://github.com/openai/codex)] [[Harness engineering](https://openai.com/index/harness-engineering/)]

**DeepSeek Harness.** DeepSeek Harness makes the model adapter, agent loop, tool registry, session log, storage, sandbox, compaction, telemetry, and user-facing surfaces composable through Cordis plugins, profiles, bundles, and ordered patches. The durable session log is the source from which model context, resumes, forks, transcripts, and telemetry are derived. Typed tool execution passes through validation and pre/post-execution policy hooks. These replaceable and reversible boundaries already provide the main substrate needed to implement harness-level runtime recursive self-improvement: an external optimizer can propose bounded profile or plugin changes, evaluate them on held-out tasks, and accept, version, or roll them back. [[Code](https://github.com/deepseek-ai/deepseek-harness)] [[Architecture](https://github.com/deepseek-ai/deepseek-harness/blob/master/docs/architecture.md)]

**OpenClaw.** OpenClaw represents an always-on personal-agent harness that connects channels, sessions, tools, skills, memory, scheduled work, gateway routing, and sandboxed execution. Its importance lies in deployment continuity: identity, credentials, channel ingress, background jobs, workspace state, and operational policy remain available beyond one chat turn. Explicit tool and channel boundaries, persistent workspaces, scheduled execution, and operational logs make long-running work resumable and inspectable. The core OpenClaw system is assessed separately from PRISM and other security extensions so that system boundaries remain comparable across the matrix. [[Code](https://github.com/openclaw/openclaw)]

#### Core comparison systems

- **Coding harnesses:** [Gemini CLI](https://github.com/google-gemini/gemini-cli), [OpenCode](https://github.com/anomalyco/opencode), [Goose](https://github.com/aaif-goose/goose), [Grok Build](https://github.com/xai-org/grok-build), [Cline](https://github.com/cline/cline), [OpenHands](https://github.com/OpenHands/OpenHands), [Deep Agents](https://github.com/langchain-ai/deepagents), [Prime Agent](https://github.com/PrimeIntellect-ai/prime-agent).
- **General runtimes:** [OpenAI Agents SDK](https://github.com/openai/openai-agents-python), [Google ADK](https://github.com/google/adk-python), [Microsoft Agent Framework](https://github.com/microsoft/agent-framework), [LangGraph](https://github.com/langchain-ai/langgraph).
- **Other representative routes:** [DeerFlow](https://github.com/bytedance/deer-flow), [AIOS](https://github.com/agiresearch/AIOS), [AOHP](https://github.com/aohp-os/aohp), [Omnigent](https://github.com/omnigent-ai/omnigent).

#### Extended catalog and adjacent layers

- **Extended harness catalog:** [Aider](https://github.com/Aider-AI/aider), [SWE-agent](https://github.com/SWE-agent/SWE-agent), [Mastra](https://github.com/mastra-ai/mastra), [AutoGen](https://github.com/microsoft/autogen), [MetaGPT](https://github.com/geekan/MetaGPT), [CAMEL](https://github.com/camel-ai/camel), [ChatDev](https://github.com/OpenBMB/ChatDev), [Raven](https://github.com/EverMind-AI/Raven), [Hermes Agent](https://github.com/nousresearch/hermes-agent), [SandBase](https://github.com/sandbaseai/sandbase-harness), [MiMo-Code](https://github.com/XiaomiMiMo/MiMo-Code), [Open SWE](https://github.com/langchain-ai/open-swe), [QM](https://github.com/yc-software/qm), [Eve](https://github.com/vercel/eve), [Shepherd](https://github.com/shepherd-agents/shepherd), and [YYLO](https://github.com/yylo-dev/yylo).
- **Capability modules and research patterns:** [MemGPT](https://github.com/cpacker/MemGPT), [Reflexion](https://github.com/noahshinn/reflexion), [Voyager](https://github.com/MineDojo/Voyager), [Generative Agents](https://github.com/joonspk-research/generative_agents), [Concordia](https://github.com/google-deepmind/concordia), and [SkillOpt](https://github.com/microsoft/SkillOpt). Their narrower scope is described directly instead of being interpreted as incomplete production harnesses.
- **Evaluation infrastructure:** [HAL](https://arxiv.org/abs/2510.11977), [Harbor](https://github.com/harbor-framework/harbor), [AgentCompass](https://arxiv.org/abs/2607.13705), [BrowserGym](https://github.com/ServiceNow/BrowserGym), and related runners are compared as infrastructure, not as agent products.

### Technical Challenges

**Scope:** This section groups recurring engineering problems where current harness infrastructure provides partial solutions and where academic prototypes and deployed systems expose different constraints.

**Evaluation criteria:** For each challenge, we assess: (1) **Academic coverage** — peer-reviewed solutions, if any; (2) **Production maturity** — whether any deployed system has solved it at scale; (3) **Blocking severity** — whether the unsolved problem prevents deployment or merely limits performance.

**Cross-cutting theme:** Most challenges stem from the **composition problem** — individual components (security sandboxes, memory stores, evaluation metrics) work in isolation, but combining them into a coherent harness surfaces emergent failures. Formal verification, portability testing, and protocol interoperability all require compositional reasoning that current research has not addressed.

#### Security & Sandboxing

**Challenge:** Agent sandboxes must prevent malicious tool use while permitting legitimate system access — a harder problem than traditional application sandboxing because agents **intentionally** interact with sensitive resources (file systems, network APIs, shell commands).

**State of the art:** SandboxEscapeBench measures whether models can exploit deliberately vulnerable sandbox configurations, while PRISM studies runtime interception and defense in depth. Together they motivate testing both isolation boundaries and the policies that mediate privileged actions; neither establishes a universal sandbox configuration for every agent workload.

**Open problems:** Compositional security properties (proving agent + harness + environment satisfy a safety specification) remain unsolved. Current defenses are reactive (detecting escapes) rather than preventive (proving impossibility of escape).

> **Evidence focus:** SandboxEscapeBench tests whether models can discover and exploit deliberately seeded sandbox misconfigurations and vulnerabilities. The result motivates configuration testing and defense in depth; it is not a generic escape rate for correctly configured containers.

- <u>SandboxEscapeBench</u>†: **"Quantifying Frontier LLM Capabilities for Container Sandbox Escape"**. *Marchand et al.* arXiv 2026. [[Paper](https://arxiv.org/abs/2603.02277)]
- <u>InjecAgent</u>: **"InjecAgent: Benchmarking Indirect Prompt Injections in Tool-Integrated Large Language Model Agents"**. *Zhan et al.* arXiv 2024. [[Paper](https://arxiv.org/abs/2403.02691)]
- <u>ToolHijacker</u>†: **"Prompt Injection Attack to Tool Selection in LLM Agents"**. *Shi et al.* NDSS 2026. [[Paper](https://arxiv.org/abs/2504.19793)]
- <u>Securing MCP</u>†: **"Securing the Model Context Protocol (MCP): Risks, Controls, and Governance"**. *Errico et al.* arXiv 2025. [[Paper](https://arxiv.org/abs/2511.20920)]
- <u>SHIELDA</u>†: **"SHIELDA: Structured Handling of Exceptions in LLM-Driven Agentic Workflows"**. *Zhou et al.* arXiv 2025. [[Paper](https://arxiv.org/abs/2508.07935)]
- <u>PALADIN</u>†: **"PALADIN: Self-Correcting Language Model Agents to Cure Tool-Failure Cases"**. *Vuddanti et al.* ICLR 2026. [[Paper](https://arxiv.org/abs/2509.25238)]
- <u>AgentBound</u>†: **"Securing AI Agent Execution"**. *Bühler et al.* arXiv 2025. [[Paper](https://arxiv.org/abs/2510.21236)]
- <u>AgentSpec</u>†: **"Agentspec: Customizable runtime enforcement for safe and reliable llm agents"**. *Wang et al.* arXiv 2025. [[Paper](https://arxiv.org/abs/2503.18666)]
- <u>AgentSys</u>†: **"AgentSys: Secure and Dynamic LLM Agents Through Explicit Hierarchical Memory Management"**. *Wen et al.* arXiv 2026. [[Paper](https://arxiv.org/abs/2602.07398)]
- <u>Docker</u>: **"Docker: Lightweight Linux Containers for Consistent Development and Deployment"**. *Merkel.* Linux Journal 2014(239). [[Paper](https://www.linuxjournal.com/content/docker-lightweight-linux-containers-consistent-development-and-deployment)]
- <u>gVisor</u>: **"The True Cost of Containing: A gVisor Case Study"**. *Young et al.* HotCloud '19. [[Paper](https://www.usenix.org/conference/hotcloud19/presentation/young)]
- <u>Firecracker</u>: **"Firecracker: Lightweight Virtualization for Serverless Applications"**. *Agache et al.* NSDI 2020. [[Paper](https://www.usenix.org/conference/nsdi20/presentation/agache)]
- <u>WebAssembly</u>: **"Bringing the Web up to Speed with WebAssembly"**. *Haas et al.* PLDI 2017. [[Paper](https://doi.org/10.1145/3062341.3062363)]
- <u>Indirect Prompt Injection</u>: **"Not What You've Signed Up For: Compromising Real-World LLM-Integrated Applications with Indirect Prompt Injection"**. *Greshake et al.* AISec 2023. [[Paper](https://arxiv.org/abs/2302.12173)]
- <u>Misevolution Risks</u>†: **"Your agent may misevolve: Emergent risks in self-evolving llm agents"**. *Shao et al.* arXiv 2025. [[Paper](https://arxiv.org/abs/2509.26354)]
- <u>Security Threat Modeling</u>†: **"Security Threat Modeling for Emerging AI-Agent Protocols: A Comparative Analysis of MCP, A2A, Agora, and ANP"**. *Anbiaee et al.* arXiv 2026. [[Paper](https://arxiv.org/abs/2602.11327)]
- <u>AgentHarm</u>†: **"AgentHarm: A Benchmark for Measuring Harmfulness of LLM Agents"**. *Andriushchenko et al.* arXiv 2024. [[Paper](https://arxiv.org/abs/2410.09024)]
- <u>TrustAgent</u>: **"TrustAgent: Towards Safe and Trustworthy LLM-Based Agents"**. *Hua et al.* EMNLP 2024. [[Paper](https://arxiv.org/abs/2402.01586)]
- <u>ToolEmu</u>†: **"Identifying the Risks of LM Agents with an LM-Emulated Sandbox"**. *Ruan et al.* arXiv 2023. [[Paper](https://arxiv.org/abs/2309.15817)]
- <u>Ignore Previous Prompt</u>: **"Ignore Previous Prompt: Attack Techniques For Language Models"**. *Perez & Ribeiro.* NeurIPS ML Safety Workshop 2022. [[Paper](https://arxiv.org/abs/2211.09527)]

#### Evaluation & Benchmarking

> **Evidence focus:** Harness evaluation must report the runtime, environment, task version, budget, trajectory capture, and evaluator together. HAL, OSWorld, and METR illustrate different failure sources: execution variance, evaluator error, and disagreement between benchmark acceptance and human review.

- <u>AgencyBench</u>†: **"AgencyBench: Benchmarking the Frontiers of Autonomous Agents in 1M-Token Real-World Contexts"**. *Li et al.* arXiv 2026. [[Paper](https://arxiv.org/abs/2601.11044)]
- <u>AEGIS</u>†: **"AEGIS: No Tool Call Left Unchecked -- A Pre-Execution Firewall and Audit Layer for AI Agents"**. *Yuan et al.* arXiv 2026. [[Paper](https://arxiv.org/abs/2603.12621)]
- <u>Hell or High Water</u>†: **"Hell or High Water: Evaluating Agentic Recovery from External Failures"**. *Wang et al.* COLM 2025. [[Paper](https://arxiv.org/abs/2508.11027)]
- <u>SearchLLM</u>†: **"Aligning Large Language Models with Searcher Preferences"**. *Wu et al.* arXiv 2026. [[Paper](https://arxiv.org/abs/2603.10473)]
- <u>Meta-Harness</u>†: **"Meta-Harness: End-to-End Optimization of Model Harnesses"**. *Lee et al.* arXiv 2026. [[Paper](https://arxiv.org/abs/2603.28052)]
- <u>AutoHarness</u>†: **"AutoHarness: improving LLM agents by automatically synthesizing a code harness"**. *Lou et al.* arXiv 2026. [[Paper](https://arxiv.org/abs/2603.03329)]
- <u>MASEval</u>†: **"MASEval: Extending Multi-Agent Evaluation from Models to Systems"**. *Emde et al.* arXiv 2026. [[Paper](https://arxiv.org/abs/2603.08835)]
- <u>VeRO</u>†: **"VeRO: An Evaluation Harness for Agents to Optimize Agents"**. *Ursekar et al.* arXiv 2026. [[Paper](https://arxiv.org/abs/2602.22480)]
- <u>ClawBench</u>†: **"ClawBench: Can AI Agents Complete Everyday Online Tasks?"**. *Zhang et al.* arXiv 2026. [[Paper](https://arxiv.org/abs/2604.08523)] [[Code](https://github.com/TIGER-AI-Lab/ClawBench)] [[Project](https://claw-bench.com/)]
- <u>TheAgentCompany</u>†: **"TheAgentCompany: Benchmarking LLM Agents on Consequential Real-World Tasks"**. *Xu et al.* arXiv 2024. [[Paper](https://arxiv.org/abs/2412.14161)]
- <u>BrowserGym</u>†: **"The BrowserGym Ecosystem for Web Agent Research"**. *Le Sellier De Chezelles et al.* arXiv 2024. [[Paper](https://arxiv.org/abs/2412.05467)]
- <u>WorkArena</u>†: **"WorkArena: How Capable are Web Agents at Solving Common Knowledge Work Tasks?"**. *Drouin et al.* arXiv 2024. [[Paper](https://arxiv.org/abs/2403.07718)]
- <u>R-Judge</u>: **"R-Judge: Benchmarking Safety Risk Awareness for LLM Agents"**. *Yuan et al.* EMNLP 2024. [[Paper](https://arxiv.org/abs/2401.10019)]
- <u>R2E</u>: **"R2E: Turning any GitHub Repository into a Programming Agent Environment"**. *Jain et al.* ICML 2024. [[Paper](https://proceedings.mlr.press/v235/jain24c.html)]
- <u>Evaluation Survey</u>: **"Evaluation and Benchmarking of LLM Agents: A Survey"**. *Mohammadi et al.* KDD 2025. [[Paper](https://arxiv.org/abs/2507.21504)]
- <u>PentestJudge</u>†: **"PentestJudge: Judging Agent Behavior Against Operational Requirements"**. *Caldwell et al.* arXiv 2025. [[Paper](https://arxiv.org/abs/2508.02921)]
- <u>PerspectiveGap</u>†: **"PerspectiveGap: A Benchmark for Multi-Agent Orchestration Prompting"**. *Sun et al.* arXiv 2026. [[Paper](https://arxiv.org/abs/2606.08878)] [[Code](https://github.com/WhymustIhaveaname/PerspectiveGap)]
- <u>TraceDance</u>†: **"TraceDance: An Automated System for Building Agent Behavior Benchmarks from Real-World Agent Deployment Traces"**. *Min et al.* arXiv 2026. [[Paper](https://arxiv.org/abs/2609.33295)] [[Project](https://zhishanq.github.io/TraceDance/)]
  - Constructs behavior-specific benchmarks from deployment traces and scores an LLM's next turn in a fixed recorded harness context, without executing its actions or replaying the environment.

#### Protocol Standardization

> **Evidence focus:** MCP, A2A, ACP, and related protocols operate at different interface layers. Their utility depends on semantics, state handling, authorization, error behavior, and testable interoperability, rather than protocol names alone.

- <u>MCP</u>: **"Model Context Protocol"**. *Anthropic.* Technical Report 2024. [[Spec](https://modelcontextprotocol.io)]
- <u>A2A</u>: **"Agent-to-Agent Protocol"**. *Google.* Technical Report 2025. [[Spec](https://a2a-protocol.org/latest/)] [[Announcement](https://developers.googleblog.com/en/a2a-a-new-era-of-agent-interoperability/)]
- <u>Protocol Comparison</u>†: **"A Survey of Agent Interoperability Protocols: Model Context Protocol (MCP), Agent Communication Protocol (ACP), Agent-to-Agent Protocol (A2A), and Agent Network Protocol (ANP)"**. *Ehtesham et al.* arXiv 2025. [[Paper](https://arxiv.org/abs/2505.02279)]
- <u>Gorilla</u>: **"Gorilla: Large Language Model Connected with Massive APIs"**. *Patil et al.* NeurIPS 2023. [[Paper](https://arxiv.org/abs/2305.15334)] [[Code](https://github.com/ShishirPatil/gorilla)]

#### Runtime Context Management

> **Evidence focus:** SkillsBench and long-context studies show that adding context is not enough: selection, placement, compaction, provenance, and conflict handling determine whether additional material helps the agent.

- <u>SkillsBench</u>†: **"SkillsBench: Benchmarking How Well Agent Skills Work Across Diverse Tasks"**. *Li et al.* arXiv 2026. [[Paper](https://arxiv.org/abs/2602.12670)]
- <u>ReadAgent</u>: **"A Human-Inspired Reading Agent with Gist Memory of Very Long Contexts"**. *Lee et al.* ICML 2024. [[Paper](https://arxiv.org/abs/2402.09727)]
- <u>MemoryOS</u>: **"Memory OS of AI Agent"**. *Kang et al.* arXiv 2025. [[Paper](https://arxiv.org/abs/2506.06326)]
- <u>CoALA</u>: **"Cognitive Architectures for Language Agents"**. *Sumers et al.* TMLR 2024. [[Paper](https://arxiv.org/abs/2309.02427)]
- <u>SkillFortify</u>†: **"Formal Analysis and Supply Chain Security for Agentic AI Skills"**. *Bhardwaj.* arXiv 2026. [[Paper](https://arxiv.org/abs/2603.00195)]
- <u>Lost in the Middle</u>: **"Lost in the Middle: How Language Models Use Long Contexts"**. *Liu et al.* TACL 2024. [[Paper](https://arxiv.org/abs/2307.03172)]
- <u>Context Engineering Survey</u>†: **"Context Engineering: A Survey of 1,400 Papers on Effective Context Management for LLM Agents"**. *Mei et al.* arXiv 2025. [[Paper](https://arxiv.org/abs/2507.13334)]

#### Tool Use & Registry

> **Evidence focus:** Tool reliability depends on more than the number of available tools. Tool selection, typed contracts, semantic authorization, result validation, and recovery policy interact across the execution loop.

- <u>CodeAct</u>: **"Executable Code Actions Elicit Better LLM Agents"**. *Wang et al.* ICML 2024. [[Paper](https://arxiv.org/abs/2402.01030)] [[Code](https://github.com/xingyaoww/code-act)]
- <u>Schema First</u>†: **"Schema First Tool APIs for LLM Agents: A Controlled Study of Tool Misuse, Recovery, and Budgeted Performance"**. *Sigdel & Baral.* arXiv 2026. [[Paper](https://arxiv.org/abs/2603.13404)]
- <u>ToolLLM</u>: **"ToolLLM: Facilitating Large Language Models to Master 16000+ Real-world APIs"**. *Qin et al.* ICLR 2024. [[Paper](https://arxiv.org/abs/2307.16789)] [[Code](https://github.com/OpenBMB/ToolBench)]
- <u>ToolSandbox</u>†: **"ToolSandbox: A Stateful, Conversational, Interactive Evaluation Benchmark for LLM Tool Use Capabilities"**. *Lu et al.* arXiv 2024. [[Paper](https://arxiv.org/abs/2408.04682)]
- <u>AutoTool</u>†: **"AutoTool: Efficient Tool Selection for Large Language Model Agents"**. *Jia & Li.* AAAI 2026. [[Paper](https://arxiv.org/abs/2511.14650)]
- <u>Tool Learning Survey</u>: **"Tool Learning with Large Language Models: A Survey"**. *Qu et al.* Frontiers of Computer Science 2024. [[Paper](https://arxiv.org/abs/2405.17935)]
- <u>GoEX</u>†: **"GoEX: Perspectives and Designs Towards a Runtime for Autonomous LLM Applications"**. *Patil et al.* arXiv 2024. [[Paper](https://arxiv.org/abs/2404.06921)]
- <u>AgentTuning</u>: **"AgentTuning: Enabling Generalized Agent Abilities for LLMs"**. *Zeng et al.* ACL 2024. [[Paper](https://arxiv.org/abs/2310.12823)]

#### Memory Architecture

> **Evidence focus:** Memory systems trade off retrieval quality, write policy, temporal consistency, provenance, latency, and cost. No single substrate is uniformly best across task types and interaction horizons.

- <u>Agent Workflow Memory (AWM)</u>†: **"Agent Workflow Memory"**. *Wang et al.* arXiv 2024. [[Paper](https://arxiv.org/abs/2409.07429)]
- <u>Mem0</u>†: **"Mem0: Building Production-Ready AI Agents with Scalable Long-Term Memory"**. *Khant et al.* arXiv 2025. [[Paper](https://arxiv.org/abs/2504.19413)]
- <u>A-MEM</u>†: **"A-MEM: Agentic Memory for LLM Agents"**. *Xu et al.* NeurIPS 2025. [[Paper](https://arxiv.org/abs/2502.12110)]
- <u>MemAct</u>†: **"Memory as Action: Autonomous Context Curation for Long-Horizon Agentic Tasks"**. *Zhang et al.* arXiv 2025. [[Paper](https://arxiv.org/abs/2510.12635)]
- <u>Memory Survey</u>†: **"Memory for Autonomous LLM Agents: Mechanisms, Evaluation, and Emerging Frontiers"**. *Du.* arXiv 2026. [[Paper](https://arxiv.org/abs/2603.07670)]
- <u>MemoryBank</u>: **"MemoryBank: Enhancing Large Language Models with Long-Term Memory"**. *Zhong et al.* AAAI 2024. [[Paper](https://arxiv.org/abs/2305.10250)]
- <u>LoCoMo</u>†: **"Evaluating Very Long-Term Conversational Memory of LLM Agents"**. *Maharana et al.* arXiv 2024. [[Paper](https://arxiv.org/abs/2402.17753)]
- <u>Memory Mechanisms Survey</u>†: **"A Survey on the Memory Mechanism of Large Language Model Based Agents"**. *Zhang et al.* arXiv 2024. [[Paper](https://arxiv.org/abs/2404.13501)]
- <u>Evo-Memory</u>†: **"Evo-Memory: Benchmarking LLM Agent Test-time Learning with Self-Evolving Memory"**. *Wei et al.* arXiv 2025. [[Paper](https://arxiv.org/abs/2511.20857)]

#### Planning & Reasoning

> **Key numbers:** SWE-agent ACI study shows interface design outweighs model capability as the primary performance determinant. LATS integrates MCTS with language model feedback for state-space search. Plan-on-Graph enables adaptive self-correcting planning on knowledge graphs through guidance, memory, and reflection mechanisms.

- <u>Tree of Thoughts</u>: **"Tree of Thoughts: Deliberate Problem Solving with Large Language Models"**. *Yao et al.* NeurIPS 2023. [[Paper](https://arxiv.org/abs/2305.10601)] [[Code](https://github.com/princeton-nlp/tree-of-thought-llm)]
- <u>LATS</u>: **"Language Agent Tree Search Unifies Reasoning, Acting, and Planning in Language Models"**. *Zhou et al.* arXiv 2023. [[Paper](https://arxiv.org/abs/2310.04406)] [[Code](https://github.com/lapisrocks/LanguageAgentTreeSearch)]
- <u>Plan-on-Graph</u>: **"Plan-on-Graph: Self-Correcting Adaptive Planning of Large Language Model on Knowledge Graphs"**. *Chen et al.* NeurIPS 2024. [[Paper](https://proceedings.neurips.cc/paper_files/paper/2024/hash/4254e856d01a5e7b7ea050477c3ef9b9-Abstract-Conference.html)]
- <u>AFlow</u>†: **"AFlow: Automating Agentic Workflow Generation"**. *Zhang et al.* arXiv 2024. [[Paper](https://arxiv.org/abs/2410.10762)]
- <u>Agent Q</u>†: **"Agent Q: Advanced Reasoning and Learning for Autonomous AI Agents"**. *Putta et al.* arXiv 2024. [[Paper](https://arxiv.org/abs/2408.07199)]
- <u>OPENDEV</u>†: **"Building Effective AI Coding Agents for the Terminal: Scaffolding, Harness, Context Engineering, and Lessons Learned"**. *Bui.* arXiv 2026. [[Paper](https://arxiv.org/abs/2603.05344)]
- <u>AOrchestra</u>†: **"AOrchestra: Automating Sub-Agent Creation for Agentic Orchestration"**. *Ruan et al.* arXiv 2026. [[Paper](https://arxiv.org/abs/2602.03786)]
- <u>RAP</u>: **"Reasoning with Language Model is Planning with World Model"**. *Hao et al.* EMNLP 2023. [[Paper](https://arxiv.org/abs/2305.14992)]
- <u>Inner Monologue</u>: **"Inner Monologue: Embodied Reasoning Through Planning with Language Models"**. *Huang et al.* CoRL 2022. [[Paper](https://arxiv.org/abs/2207.05608)]
- <u>Agent-Oriented Planning</u>: **"Agent-Oriented Planning in Multi-Agent Systems"**. *Li et al.* ICLR 2025. [[Paper](https://arxiv.org/abs/2410.02189)]
- <u>ExACT</u>†: **"ExACT: Teaching AI Agents to Explore with Reflective-MCTS and Exploratory Learning"**. *Yu et al.* arXiv 2024. [[Paper](https://arxiv.org/abs/2410.02052)]
- <u>Steer, Don't Solve</u>†: **"Steer, Don't Solve: Training Small Critic Models for Large Code Agents"**. *Gandhi et al.* arXiv 2026. [[Paper](https://arxiv.org/abs/2606.21811)] [[Code](https://github.com/shubhamrgandhi/critic-training)]

#### Multi-Agent Coordination

> **Evidence focus:** [AgencyBench](https://arxiv.org/abs/2601.11044) reports 48.4% aggregate performance for closed models versus 32.1% for open models, and separately observes native-ecosystem advantages for some proprietary systems. The aggregate 48.4% figure is not a native-SDK success rate.

<p align="center">
  <img src="assets/multi_agent_topology.png" width="680" alt="Multi-Agent Coordination Topologies"/>
</p>

- <u>AdaptOrch</u>†: **"AdaptOrch: Task-Adaptive Multi-Agent Orchestration in the Era of LLM Performance Convergence"**. *Yu.* arXiv 2026. [[Paper](https://arxiv.org/abs/2602.16873)]
- <u>SAGA</u>†: **"SAGA: A Security Architecture for Governing AI Agentic Systems"**. *Syros et al.* NDSS 2026. [[Paper](https://arxiv.org/abs/2504.21034)]
- <u>MAS-FIRE</u>†: **"MAS-FIRE: Fault Injection and Reliability Evaluation for LLM-Based Multi-Agent Systems"**. *Jia et al.* arXiv 2026. [[Paper](https://arxiv.org/abs/2602.19843)]
- <u>Byzantine fault tolerance</u>†: **"Rethinking the Reliability of Multi-agent System: A Perspective from Byzantine Fault Tolerance"**. *Zheng et al.* arXiv 2025. [[Paper](https://arxiv.org/abs/2511.10400)]
- <u>Multi-agent baseline study</u>†: **"Rethinking the Value of Multi-Agent Workflow: A Strong Single Agent Baseline"**. *Xu et al.* arXiv 2026. [[Paper](https://arxiv.org/abs/2601.12307)]
- <u>AgentVerse</u>†: **"AgentVerse: Facilitating Multi-Agent Collaboration and Exploring Emergent Behaviors"**. *Chen et al.* arXiv 2023. [[Paper](https://arxiv.org/abs/2308.10848)]
- <u>Mixture-of-Agents</u>†: **"Mixture-of-Agents Enhances Large Language Model Capabilities"**. *Wang et al.* arXiv 2024. [[Paper](https://arxiv.org/abs/2406.04692)]
- <u>Multi-Agent Survey</u>: **"Large Language Model Based Multi-Agents: A Survey of Progress and Challenges"**. *Guo et al.* IJCAI 2024. [[Paper](https://arxiv.org/abs/2402.01680)]
- <u>Concordia</u>†: **"Generative Agent-Based Modeling with Actions Grounded in Physical, Social, or Digital Space Using Concordia"**. *Vezhnevets et al.* arXiv 2023. [[Paper](https://arxiv.org/abs/2312.03664)]
- <u>PEvo</u>: **"Implicit Behavioral Alignment of Language Agents in High-Stakes Crowd Simulations"**. *Wang et al.* EMNLP 2025. [[Paper](https://arxiv.org/abs/2509.16457)]
- <u>Agon</u>†: **"Agon: An Autonomous Large-Scale Omnidisciplinary Research System Built on Prompt Economy"**. *Sun et al.* arXiv 2026. [[Paper](https://arxiv.org/abs/2606.24177)] [[Code](https://github.com/AutoResearch-Factory/Agon)]

#### Compute Economics

> **Evidence focus:** Harness economics should report tokens, wall-clock time, tool and environment cost, concurrency, retries, failed work, and quality together. Throughput alone does not describe the cost of a long-running agent task.

- <u>State of AI Report</u>: **"State of AI: An Empirical 100 Trillion Token Study with OpenRouter"**. *Aubakirova et al.* Andreessen Horowitz (a16z) and OpenRouter Inc., December 2025. [[Report](https://openrouter.ai/state-of-ai)]
- <u>BentoML Inference Report</u>: **"Beyond Tokens-per-Second: How to Balance Speed, Cost, and Quality in LLM Inference"**. *Yang.* BentoML Blog, January 2026. [[Blog](https://www.bentoml.com/blog/beyond-tokens-per-second-how-to-balance-speed-cost-and-quality-in-llm-inference)]
- <u>H100 Price Spike</u>: **"H100 Price Spike: Understanding the 10% Surge in GPU Rental Costs"**. *Li.* Silicon Data Blog, January 2026. [[Blog](https://www.silicondata.com/blog/h100-price-spike)]
- <u>NVIDIA GTC 2026</u>: **"NVIDIA GTC 2026: Live Updates on What's Next in AI"**. *NVIDIA.* NVIDIA Blog, March 2026. [[Blog](https://blogs.nvidia.com/blog/gtc-2026-news/)]
- <u>Repo2Run</u>†: **"Repo2Run: Automated Building Executable Environment for Code Repository at Scale"**. *Hu et al.* arXiv 2025. [[Paper](https://arxiv.org/abs/2502.13681)]
- <u>Policy-First</u>†: **"Guardrails as Infrastructure: Policy-First Control for Tool-Orchestrated Workflows"**. *Sigdel & Baral.* arXiv 2026. [[Paper](https://arxiv.org/abs/2603.18059)]
- <u>Strong-Weak Collaboration</u>: **"An Empirical Study on Strong-Weak Model Collaboration for Repo-level Code Generation"**. *Gandhi et al.* EMNLP 2025. [[Paper](https://aclanthology.org/2025.emnlp-main.1043/)] [[Code](https://github.com/shubhamrgandhi/codegen-strong-weak-collab)]

---

### Emerging Topics

- <u>AutoRef</u>†: **"AutoRef: Harness Optimization for Agentic Multi-Reference Image Generation"**. *Oshima et al.* arXiv 2026. [[Paper](https://arxiv.org/abs/2609.35530)] [[Code](https://github.com/KuOnoda/AutoRef)]
- <u>Harness Engineering for Language Agents</u>†: **"Harness Engineering for Language Agents: The Harness Layer as Control, Agency, and Runtime"**. *He et al.* Preprints 2026. [[Paper](https://www.preprints.org)]
- <u>DeepAgent</u>†: **"Deepagent: A general reasoning agent with scalable toolsets"**. *Li et al.* arXiv 2025. [[Paper](https://arxiv.org/abs/2510.21618)]
- <u>Natural-Language Harnesses</u>†: **"Natural-Language Agent Harnesses"**. *Pan et al.* arXiv 2026. [[Paper](https://arxiv.org/abs/2603.25723)]
- <u>Self-Evolving Agents Survey</u>†: **"A Survey of Self-Evolving Agents: What, When, How, and Where to Evolve on the Path to Artificial Super Intelligence"**. *Gao et al.* TMLR 2026. [[Paper](https://arxiv.org/abs/2507.21046)]
- <u>Self-RAG</u>: **"Self-RAG: Learning to Retrieve, Generate, and Critique Through Self-Reflection"**. *Asai et al.* ICLR 2024. [[Paper](https://arxiv.org/abs/2310.11511)]
- <u>Constitutional AI</u>: **"Constitutional AI: Harmlessness from AI Feedback"**. *Bai et al.* arXiv 2022. [[Paper](https://arxiv.org/abs/2212.08073)]
- <u>AppAgent</u>†: **"AppAgent: Multimodal Agents as Smartphone Users"**. *Zhang et al.* arXiv 2023. [[Paper](https://arxiv.org/abs/2312.13771)]

#### Related Surveys

- <u>LLM Agents Survey</u>: **"A Survey on Large Language Model Based Autonomous Agents"**. *Wang et al.* arXiv 2023. [[Paper](https://arxiv.org/abs/2308.11432)]
- <u>Rise of LLM Agents</u>: **"The Rise and Potential of Large Language Model Based Agents: A Survey"**. *Xi et al.* arXiv 2023. [[Paper](https://arxiv.org/abs/2309.07864)]
- <u>LLM Survey</u>: **"A Survey of Large Language Models"**. *Zhao et al.* arXiv 2023. [[Paper](https://arxiv.org/abs/2303.18223)]
- <u>AI Agent Systems</u>†: **"AI Agent Systems: Architectures, Applications, and Evaluation"**. *Xu.* arXiv 2025. [[Paper](https://arxiv.org/abs/2601.01743)]
- <u>AutoResearch Survey</u>†: **"What's Missing in Autonomous Research? A Systematization of Systems, Benchmarks, and Verification"**. *Ren et al.* 2026. [[Paper](https://www.researchgate.net/publication/406952713)]
- <u>LLM Agents: A Survey</u>†: **"LLM Agents: A Survey"**. *Lee.* Preprints.org 2026. [[Paper](https://www.preprints.org/manuscript/202608.0265/v1)]
- <u>The Agent Loop</u>†: **"The Agent Loop: A Survey of Control Strategies, Skills, and Harnesses for LLM Agents"**. *Lee and Park.* SSRN 2026. [[Paper](https://github.com/js-lee-AI/awesome-agent-loop-papers/blob/main/paper/the-agent-loop-survey.pdf)]

#### Practitioner Reports & Industry Insights

> Production deployment experiences from Stripe, OpenAI, Cursor, METR, and other frontier practitioners.

- <u>Building Effective Agents</u>: **"Building Effective Agents"**. *Anthropic.* Anthropic Engineering Blog, 2026. [[Blog](https://www.anthropic.com/engineering)]
- <u>Demystifying Evals</u>: **"Demystifying Evals for AI Agents"**. *Anthropic.* Anthropic Engineering Blog, 2026. [[Blog](https://www.anthropic.com/engineering)]
- <u>Context Engineering</u>: **"Context Engineering Our Way to Long-Horizon Agents"**. *Chase.* Sequoia Capital Podcast, 2026.
- <u>Agent Frameworks, Runtimes, and Harnesses</u>: **"Agent Frameworks, Runtimes, and Harnesses"**. *LangChain.* LangChain Blog, 2025. [[Blog](https://blog.langchain.com/agent-frameworks-runtimes-and-harnesses-oh-my/)]
- <u>We Removed 80% of Our Agent's Tools</u>: **"We Removed 80% of Our Agent's Tools"**. *Qu.* Vercel Engineering Blog, 2025. [[Blog](https://vercel.com/blog/we-removed-80-percent-of-our-agents-tools)]
- <u>Harness Problem</u>: **"I Improved 15 LLMs at Coding in One Afternoon. Only the Harness Changed."**. *Can.* Personal blog (blog.can.ac), February 2026. [[Blog](https://blog.can.ac/2026/02/12/the-harness-problem/)]
- <u>AI Adoption Journey</u>: **"My AI Adoption Journey"**. *Hashimoto.* Personal blog, February 2026. [[Blog](https://mitchellh.com/writing/my-ai-adoption-journey)]
- <u>The Harness Gap</u>: **"The Harness Gap: AI Coding Output Rose 59% in 2025 While Teams Shipped 7% Less"**. *Zoom In AI.* Medium (Write A Catalyst), March 2026. [[Blog](https://medium.com/write-a-catalyst/the-harness-gap-ai-coding-output-rose-59-in-2025-while-teams-shipped-7-less-082d3d07cff8)]
- <u>Stripe Minions</u>: **"Minions: Stripe's one-shot, end-to-end coding agents"**. *Gray.* Stripe Dev Blog, Feb 2026. [[Blog](https://stripe.dev/blog/minions-stripes-one-shot-end-to-end-coding-agents)]
- <u>Harness Engineering (OpenAI)</u>: **"Harness engineering: leveraging Codex in an agent-first world"**. *Lopopolo.* OpenAI Blog, Feb 2026. [[Blog](https://openai.com/index/harness-engineering/)]
- <u>Self-Driving Codebases</u>: **"Towards self-driving codebases"**. *Lin.* Cursor Blog, Feb 2026. [[Blog](https://cursor.com/blog/self-driving-codebases)]
- <u>METR SWE-bench Analysis</u>: **"Many SWE-bench-Passing PRs Would Not Be Merged into Main"**. *Whitfill et al.* METR Notes, Mar 2026. [[Report](https://metr.org/notes/2026-03-10-many-swe-bench-passing-prs-would-not-be-merged-into-main/)]

- <u>Harness-Aware Training</u>†: **"Training Agents to Evolve with Their Harness: TaoLive Digital Avatar Agent Technical Report"**. *TaoLive AIGC LLM Team.* arXiv, August 2026. [[Paper](https://arxiv.org/abs/2608.15763)]

---

### Future Directions

Eight open research directions identified in the survey (no curated paper list — these are forward-looking):

- **Formal Harness Specification Language** — DSL for specifying and verifying H=(E,T,C,S,L,V) components
- **Cross-Harness Benchmark Suite** — portability testing across incompatible harness ecosystems
- **Security Taxonomy & Threat Model** — extension of OWASP Top 10 to agent harness attack surfaces
- **Protocol Interoperability (MCP/A2A)** — bridging tool-level and agent-level protocols
- **Long-Horizon Evaluation Methodology** — metrics that don't degrade under multi-session, multi-day tasks
- **Harness-Aware Fine-Tuning** — training models that are aware of their execution environment
- **Memory Interface Standardization** — portable memory APIs across flat, episodic, and graph stores
- **Harness Transparency Specification** — auditability and explainability for runtime decisions

---

## Citation

See BibTeX at the top of this README.

---

## Update Log

| Version | Date | Changes |
|---------|------|---------|
| Resource 2026.10 | 2026-10-13 | Rebuilt the system matrix and benchmark map; corrected links and quantitative claims |
| Paper v4 | 2026-04-14 | Repository PDF; the manuscript predates the 2026.10 resource index |
| Archived preprint v3 | 2026-04-09 | DOI-linked public preprint |
---

<p align="center">
  <i>† denotes preprint, not yet peer-reviewed.</i><br>
  <i>This survey is under active development; the full manuscript will be released soon.</i><br>
  <i>Maintained by Qianyu Meng & Liyi Chen. PRs welcome for missing papers or updated links.</i>
</p>
