<div align="center">

[English](README.md) | [中文](README_zh.md)

# Awesome Agent Harness

### Systems, benchmarks, papers, and engineering evidence for the runtime layer of LLM agents

[![Awesome](https://awesome.re/badge-flat2.svg)](https://awesome.re)
[![GitHub Stars](https://img.shields.io/github/stars/Gloriaameng/Awesome-Agent-Harness?style=social)](https://github.com/Gloriaameng/Awesome-Agent-Harness)
[![License](https://img.shields.io/badge/License-CC--BY--4.0-blue.svg)](license)
[![Resource Index](https://img.shields.io/badge/Resource%20Index-2026.10-0b7285)](#release-status)
[![Core Systems](https://img.shields.io/badge/Core%20Systems-20-5c7cfa)](#harness-directory)
[![Harness Benchmarks](https://img.shields.io/badge/Harness%20Benchmarks-27-7950f2)](#benchmark-directory)
[![Research References](https://img.shields.io/badge/Research%20References-133-2b8a3e)](#research-library)
[![Paper](https://img.shields.io/badge/Paper-v4-orange)](./Agent_Harness_for_LLM_Agents__A_Survey__v4.pdf)

</div>

> **A model never acts alone.** The execution loop, tools, context, state, permissions, and evaluator around it shape what the agent can do, how long it can keep working, what failures it can recover from, and whether its result can be trusted.

This repository is a curated map of that **agent harness** layer. It connects production systems, open-source runtimes, direct harness benchmarks, task environments, and the research needed to build and evaluate long-running agents.

**Start exploring:** [Featured harnesses](#featured-harnesses) · [All systems](#harness-directory) · [Harness benchmarks](#benchmark-directory) · [Evidence matrix](#20-system-evidence-matrix) · [Research library](#research-library) · [Paper v4](./Agent_Harness_for_LLM_Agents__A_Survey__v4.pdf)

---

## Start Here

| If you want to... | Go to... |
|---|---|
| Understand what makes an agent runtime different from a model or framework | [The ETCSLV lens](#the-etcslv-lens) |
| Compare the most consequential coding harnesses | [Claude Code, Codex, DeepSeek Harness, and OpenClaw](#featured-harnesses) |
| Find a runtime, coding harness, agent OS, or composable framework | [Harness Directory](#harness-directory) |
| Measure what the harness changes while controlling the model and task | [Benchmark Directory](#benchmark-directory) |
| Separate harness evaluation from general agent task evaluation | [Task environments](#task-environments) |
| Trace a matrix rating or assess the evidence boundary | [20-System Evidence Matrix](#20-system-evidence-matrix) and [Curation and Evidence](#curation-and-evidence) |
| Read papers by security, context, tools, memory, planning, coordination, or cost | [Research Library](#research-library) |

### Release Status

| Artifact | Current version | Date / cutoff | Status |
|---|---|---|---|
| Resource index | **2026.10** | Evidence reviewed through **2026-10-12** | This README; last updated **2026-10-13** |
| Repository paper | **v4** | 2026-04-14 | [Public PDF](./Agent_Harness_for_LLM_Agents__A_Survey__v4.pdf) |
| Archived preprint | **v3** | 2026-04-09 | [DOI record](https://doi.org/10.20944/preprints202604.0428.v3) |
| Paper v5 | In revision | — | Not yet released |

The resource index moves independently from the paper. Paper v4 is the April snapshot; Paper v5 will integrate the newer systems and benchmarks after manuscript review.

## Contents

- [Featured Harnesses](#featured-harnesses)
- [Harness Directory](#harness-directory)
  - [Core coding harnesses](#core-coding-harnesses)
  - [General agent runtimes](#general-agent-runtimes)
  - [OS, personal, and composable harnesses](#os-personal-and-composable-harnesses)
  - [Extended catalog](#extended-catalog)
  - [Capability modules](#capability-modules-and-research-patterns)
  - [Evaluation infrastructure](#evaluation-infrastructure)
- [Benchmark Directory](#benchmark-directory)
  - [Harness effect](#1-harness-effect)
  - [Harness evolution and RSI](#2-harness-evolution-and-runtime-self-improvement)
  - [Lifecycle, security, and audit](#3-lifecycle-security-and-audit)
  - [Long-horizon loops and recovery](#4-long-horizon-loops-and-recovery)
  - [Protocol and tool substrate](#5-protocol-and-tool-substrate)
  - [Evaluation infrastructure](#6-evaluation-infrastructure)
  - [Task environments](#task-environments)
- [The ETCSLV Lens](#the-etcslv-lens)
- [Historical Timeline](#historical-timeline)
- [20-System Evidence Matrix](#20-system-evidence-matrix)
- [Curation and Evidence](#curation-and-evidence)
- [Research Library](#research-library)
  - [Historical Lineages](#historical-lineages)
  - [Research by Engineering Problem](#research-by-engineering-problem)
  - [Emerging Topics](#emerging-topics)
  - [Related Surveys](#related-surveys)
  - [Practitioner Reports](#practitioner-reports--industry-insights)
  - [Future Directions](#future-directions)
- [Paper and Citation](#paper-and-citation)
- [Contributing](#contributing)
- [Update Log](#update-log)

---

## Featured Harnesses

These four systems are the survey's anchor cases. They receive the same analytical weight because each exposes a distinct answer to the same runtime problem: how to turn model calls into governed, persistent, tool-using work.

- **[Claude Code](https://github.com/anthropics/claude-code)** — A vertically integrated coding harness that joins repository inspection, edits, commands, web and MCP tools, subagents, skills, hooks, permissions, checkpoints, and session continuation. Its CLI and [Agent SDK](https://github.com/anthropics/claude-agent-sdk-python) make the execution and policy layers visible across interactive and programmable use.
- **[Codex](https://github.com/openai/codex)** — An open-source coding harness spanning terminal, IDE, app, and cloud workflows. Its runtime combines repository tools, sandboxing, approvals, MCP, skills, subagents, compaction, resumable threads, and structured events. The shared runtime makes long-horizon work inspectable across surfaces, while OpenAI's [harness engineering](https://openai.com/index/harness-engineering/) account shows how those controls shape sustained software work.
- **[DeepSeek Harness](https://github.com/deepseek-ai/deepseek-harness)** — A plugin-native runtime in which model adapters, loops, tools, context projection, storage, telemetry, and interfaces are composed through profiles, bundles, and ordered patches. These boundaries let teams replace and audit the loop, context policy, tool behavior, and observability separately. The [architecture](https://github.com/deepseek-ai/deepseek-harness/blob/master/docs/architecture.md), [tool subsystem](https://github.com/deepseek-ai/deepseek-harness/blob/master/packages/core/tools/README.md), and [compaction design](https://github.com/deepseek-ai/deepseek-harness/blob/master/docs/subsystems/compaction.md) also provide a concrete base for bounded, evaluated, reversible harness-level improvement.
- **[OpenClaw](https://github.com/openclaw/openclaw)** — An always-on personal-agent harness organized around channels, sessions, tools, skills, memory, scheduled work, gateway routing, and sandboxed execution. It makes deployment continuity central: identity, credentials, background jobs, workspace state, and operational policy persist beyond a single chat turn. That operating model makes it a key case for studying durable personal agents rather than one-shot assistants.

## Harness Directory

The **20-system core set** supports like-for-like architectural comparison. The extended catalog preserves important systems and adjacent routes while keeping maturity judgments separate.

### Core coding harnesses

The four featured systems above are joined by eight coding harnesses in the core comparison set.

- **[Gemini CLI](https://github.com/google-gemini/gemini-cli)** — Google's open-source terminal agent with built-in tools, MCP support, extensions, project context, and non-interactive operation.
- **[OpenCode](https://github.com/anomalyco/opencode)** — An open-source coding agent with terminal and client/server surfaces, multi-provider model support, tool execution, sessions, and extensibility.
- **[Goose](https://github.com/aaif-goose/goose)** — A local, extensible coding agent whose tools and integrations are exposed through extensions and MCP-compatible interfaces.
- **[Grok Build](https://github.com/xai-org/grok-build)** — xAI's open coding-agent harness for repository work, tool use, context handling, and iterative verification.
- **[Cline](https://github.com/cline/cline)** — An IDE coding agent with plan/act workflows, checkpoints, browser and terminal tools, MCP integrations, and explicit approval points.
- **[OpenHands](https://github.com/OpenHands/OpenHands)** — A platform for software-development agents with isolated runtimes, event streams, tool execution, browsing, delegation, and evaluation integrations.
- **[Deep Agents](https://github.com/langchain-ai/deepagents)** — A batteries-included agent harness that combines planning, filesystems, subagents, context management, memory, and LangGraph execution.
- **[Prime Agent](https://github.com/PrimeIntellect-ai/prime-agent)** — A coding-agent system centered on long-running repository tasks, execution environments, trajectory capture, and training/evaluation workflows.

### General agent runtimes

- **[OpenAI Agents SDK](https://github.com/openai/openai-agents-python)** — A runtime for tools, handoffs, guardrails, sessions, tracing, and multi-agent workflows.
- **[Google ADK](https://github.com/google/adk-python)** — An agent development kit with workflow agents, tools, sessions, callbacks, evaluation, and deployment integrations.
- **[Microsoft Agent Framework](https://github.com/microsoft/agent-framework)** — Microsoft's runtime for agents, workflows, middleware, memory, tools, observability, and evaluation.
- **[LangGraph](https://github.com/langchain-ai/langgraph)** — A stateful graph runtime for durable execution, checkpoints, interrupts, streaming, and human-in-the-loop agent workflows.

### OS, personal, and composable harnesses

- **[DeerFlow](https://github.com/bytedance/deer-flow)** — A modular agent harness for research and coding workflows with subagents, skills, memory, sandbox execution, and long-running tasks.
- **[AIOS](https://github.com/agiresearch/AIOS)** — An LLM agent operating-system architecture that schedules agents and mediates models, tools, memory, storage, and access control.
- **[AOHP](https://github.com/aohp-os/aohp)** — An OS-level harness for personalized interaction, local resources, efficiency, and security boundaries.
- **[Omnigent](https://github.com/omnigent-ai/omnigent)** — A general agent platform joining tool use, state, memory, policy, and multi-surface execution.

### Extended catalog

- **[Aider](https://github.com/Aider-AI/aider)** — Terminal pair programming with repository maps, edit formats, git integration, and broad model support.
- **[SWE-agent](https://github.com/SWE-agent/SWE-agent)** — An agent-computer interface designed for solving software-engineering issues in repository environments.
- **[Mastra](https://github.com/mastra-ai/mastra)** — A TypeScript framework for agents, workflows, tools, memory, observability, and evaluation.
- **[AutoGen](https://github.com/microsoft/autogen)** — An event-driven framework for conversational and multi-agent applications.
- **[MetaGPT](https://github.com/geekan/MetaGPT)** — A multi-agent software workflow organized around roles, standard operating procedures, and shared artifacts.
- **[CAMEL](https://github.com/camel-ai/camel)** — A multi-agent framework for role-playing, tool use, memory, and agent societies.
- **[ChatDev](https://github.com/OpenBMB/ChatDev)** — A virtual software company that coordinates specialized agents through a staged development process.
- **[Raven](https://github.com/EverMind-AI/Raven)** — A composable “harness of harnesses” for assembling and coordinating agent capabilities.
- **[Hermes Agent](https://github.com/nousresearch/hermes-agent)** — A self-improving agent framework with persistent skills, tools, and learning across tasks. [Docs](https://hermes-agent.nousresearch.com/docs/)
- **[SandBase](https://github.com/sandbaseai/sandbase-harness)** — A local-first, self-hosted agent runtime and MCP bridge with explicit tool and execution boundaries.
- **[MiMo-Code](https://github.com/XiaomiMiMo/MiMo-Code)** — Xiaomi's open-source coding-agent project for repository-level development workflows.
- **[Open SWE](https://github.com/langchain-ai/open-swe)** — An open-source asynchronous coding-agent reference built for delegated repository work.
- **[QM](https://github.com/yc-software/qm)** — An open coding-agent project exploring autonomous repository work and tool-driven development.
- **[Eve](https://github.com/vercel/eve)** — Vercel's open agent project for iterative software work and execution-driven feedback.
- **[Shepherd](https://github.com/shepherd-agents/shepherd)** — An agent orchestration project for coordinating development tasks and specialized workers.
- **[YYLO](https://github.com/yylo-dev/yylo)** — A CLI for orchestrating coding agents with plugins, evidence capture, and longitudinal workflows.

### Capability modules and research patterns

These projects are evaluated for their focused capability or research pattern rather than full-stack component coverage.

- **[MemGPT](https://github.com/cpacker/MemGPT)** — Tiered memory and context management inspired by operating systems.
- **[Reflexion](https://github.com/noahshinn/reflexion)** — Verbal feedback and reflective memory across trials.
- **[Voyager](https://github.com/MineDojo/Voyager)** — Open-ended skill acquisition, curriculum generation, and reusable code skills.
- **[Generative Agents](https://github.com/joonspk-research/generative_agents)** — Memory, reflection, and planning for believable social agents.
- **[Concordia](https://github.com/google-deepmind/concordia)** — A library for generative agent-based simulations grounded in physical, social, or digital worlds.
- **[SkillOpt](https://github.com/microsoft/SkillOpt)** — Bounded skill optimization from scored trajectories with evaluation gates.

### Evaluation infrastructure

- **[HAL](https://arxiv.org/abs/2510.11977)** — Unified agent execution, evaluation, and leaderboard infrastructure.
- **[Harbor](https://github.com/harbor-framework/harbor)** — Interchangeable agents, models, datasets, container environments, traces, and parallel rollouts.
- **[AgentCompass](https://arxiv.org/abs/2607.13705)** — Infrastructure that separates benchmark, harness, and environment for reproducible agent evaluation.
- **[BrowserGym](https://github.com/ServiceNow/BrowserGym)** — A common environment and evaluation layer for web-agent research.
- **[lm-evaluation-harness](https://github.com/EleutherAI/lm-evaluation-harness)** — A widely used evaluation runner for language models; included as the lineage and naming reference for modern agent harness evaluation.

---

## Benchmark Directory

A benchmark belongs here when it reveals something about the **runtime around the model**: component choice, state over time, recovery, permissions, auditability, protocol behavior, or evaluation infrastructure. Every result should identify the model, harness, environment, task version, budget, and evaluator together.

### 1. Harness effect

- **[Harness-Bench](https://arxiv.org/abs/2605.27922)** — Compares model–harness configurations under shared sandboxed tasks, environments, budgets, and evaluation.
- **[Beyond the Model](https://arxiv.org/abs/2609.32459)** — Isolates the effects of tool registries, context compression, planning, subagents, and lazy skills.
- **[LongHarness Bench](https://arxiv.org/abs/2609.38137)** — Evaluates the accuracy and efficiency of harnesses for long-context work.
- **[Harness the Memory](https://arxiv.org/abs/2608.15008)** — Compares memory substrates in a shared harness across models and task suites.

### 2. Harness evolution and runtime self-improvement

- **[EVOHARNESSBENCH](https://arxiv.org/abs/2609.04280)** — Measures retention and adaptation as tools, skills, and agents change over time.
- **[SkillOpt](https://arxiv.org/abs/2605.23904)** — Generates bounded skill edits from scored trajectories and accepts them through held-out evaluation gates.
- **[SCLATE](https://arxiv.org/abs/2609.32391)** — Places sessions, scheduled tasks, and memory consolidation on a shared event timeline.
- **[TaoLive](https://arxiv.org/abs/2608.15763)** — Studies harness-aware training for agents that must evolve with a changing runtime.
- **[Meta-Harness](https://arxiv.org/abs/2603.28052)** — Optimizes model harnesses end to end.
- **[AutoHarness](https://arxiv.org/abs/2603.03329)** — Synthesizes code harnesses to improve an agent around a fixed model.
- **[VeRO](https://arxiv.org/abs/2602.22480)** — Provides an evaluation harness in which agents evaluate and optimize other agents.

### 3. Lifecycle, security, and audit

- **[HarnessRisk](https://arxiv.org/abs/2608.17597)** — Tests risks across configuration, extension, runtime, persistence, action, and recovery phases.
- **[HarnessSecurity-Bench](https://arxiv.org/abs/2610.07639)** — Measures utility and attack effects across real coding harnesses and permission settings.
- **[Hearsay](https://arxiv.org/abs/2609.32495)** — Tests whether harness-produced records support independent audit.
- **[SandboxEscapeBench](https://arxiv.org/abs/2603.02277)** — Measures whether models discover and exploit deliberately seeded sandbox misconfigurations and vulnerabilities.

### 4. Long-horizon loops and recovery

- **[LoopsBench](https://arxiv.org/abs/2608.00267)** — Evaluates sustained development loops and the ability to keep making valid progress.
- **[Long-Horizon-Terminal-Bench](https://arxiv.org/abs/2607.08964)** — Tests agents on extended terminal tasks with accumulating state.
- **[SWE-Chain](https://arxiv.org/abs/2605.14415)** — Evaluates dependent software changes and obligations that propagate across a chain.
- **[ChainSWE](https://arxiv.org/abs/2607.02606)** — Measures repository work where later tasks depend on earlier changes and preserved state.
- **[Hell or High Water](https://arxiv.org/abs/2508.11027)** — Evaluates recovery from external failures during agent execution.

### 5. Protocol and tool substrate

- **[DynamicMCPBench](https://arxiv.org/abs/2607.20531)** — Evaluates live and changing MCP servers, tools, and state.
- **[MCP-Bench](https://arxiv.org/abs/2508.20453)** — Benchmarks end-to-end tool use through the Model Context Protocol.
- **[MCP-AgentBench](https://arxiv.org/abs/2509.09734)** — Tests MCP-based agents across tool discovery, selection, and execution.
- **[MCPAgentBench](https://arxiv.org/abs/2512.24565)** — Evaluates tool discrimination and stateful MCP interaction.

### 6. Evaluation infrastructure

- **[AgentCompass](https://arxiv.org/abs/2607.13705)** — Makes benchmark, harness, and environment explicit experimental units.
- **[Harbor](https://github.com/harbor-framework/harbor)** — Runs interchangeable agents and models in containerized datasets with traces and parallel rollouts.
- **[HAL](https://arxiv.org/abs/2510.11977)** — Supplies unified execution and leaderboard infrastructure for agent evaluation.

### Task environments

These benchmarks ask **what tasks an agent can complete**. Harness studies use them as task substrates and add controls that isolate the runtime as an experimental variable.

- **[AgencyBench](https://arxiv.org/abs/2601.11044)** — Long-context, consequential tasks for autonomous agents; report its aggregate and ecosystem-specific findings separately.
- **[ClawBench](https://github.com/TIGER-AI-Lab/ClawBench)** — Everyday online tasks for personal and computer-use agents. [Paper](https://arxiv.org/abs/2604.08523)
- **[OSWorld](https://github.com/xlang-ai/OSWorld)** — Open-ended computer tasks in real operating-system environments.
- **[WebArena](https://github.com/web-arena-x/webarena)** — Realistic websites and end-to-end tasks for autonomous web agents.
- **[GAIA](https://arxiv.org/abs/2311.12983)** — General-assistant questions that require reasoning, tools, and multiple modalities.
- **[SWE-bench](https://github.com/swe-bench/SWE-bench)** — Real GitHub issues resolved against executable repositories.

---

## The ETCSLV Lens

We analyze a harness as **H = (E, T, C, S, L, V)**: six governance functions that repeatedly appear across public systems. The lens compares architectural coverage; product quality and production readiness require separate evidence.

<p align="center">
  <img src="assets/architecture_diagram.png" width="720" alt="H=(E,T,C,S,L,V) six-component analytical framework"/>
</p>

| Component | Symbol | What to look for |
|---|:---:|---|
| Execution Loop | **E** | Turn and step control, termination, retry, recovery, delegation |
| Tool Registry | **T** | Typed tools, routing, validation, authorization, result handling |
| Context Manager | **C** | Prompt assembly, retrieval, compaction, salience, provenance |
| State Store | **S** | Cross-turn and cross-session persistence, checkpoints, recovery |
| Lifecycle Hooks | **L** | Authentication, approval, policy, instrumentation, interception |
| Evaluation Interface | **V** | Trajectories, intermediate state, outcomes, experiments, audit |

## Historical Timeline

<p align="center">
  <img src="assets/timeline.png" width="720" alt="Historical evolution of agent harnesses"/>
</p>

| Year | Milestone | Why it matters to harnesses |
|---|---|---|
| 1997–2005 | JUnit, TestNG, xUnit family | Standardized setup, execution, observation, assertion, and teardown |
| 2016 | OpenAI Gym | Made step/reset a canonical interface between agents and environments |
| 2022 | ChatGPT and LangChain | Brought tool use and composable LLM applications into a common runtime pattern |
| 2023 | ReAct, Toolformer, MemGPT, Reflexion, Voyager, AutoGPT | Established reasoning–acting, memory, reflection, and skill accumulation patterns |
| 2023 | CAMEL, ChatDev, Generative Agents | Expanded orchestration to roles, teams, and social simulation |
| 2023 | AgentBench, SWE-bench | Made environment design and agent evaluation central infrastructure |
| 2024 | MetaGPT, WebArena, ToolLLM, SWE-agent, OSWorld | Connected agents to realistic tools, repositories, browsers, and desktops |
| 2024 | CodeAct, LATS, Tree of Thoughts | Explored executable actions and search-based control policies |
| 2024 | Model Context Protocol | Standardized a growing part of the tool-to-harness boundary |
| 2025 | HAL, AIOS, LangGraph, A2A | Advanced evaluation infrastructure, agent OS design, durable graphs, and agent interoperability |
| 2025 | MemoryOS, AgentBound† | Developed memory abstractions and runtime enforcement |
| 2026 | SkillsBench†, Harness-Bench, EVOHARNESSBENCH, HarnessRisk, HarnessSecurity-Bench, LoopsBench, SCLATE | Shifted evaluation toward skills, harness effects, evolution, lifecycle risk, recovery, and auditability |

## 20-System Evidence Matrix

Ratings describe documented component coverage at the evidence cutoff. Quality, production maturity, and adoption are reported separately; popularity and stars serve only as adoption signals.

**Legend:** ● **Full** — built in and documented · ◐ **Partial** — limited, optional, or supplied by an official extension · ○ **Absent** — first-party material explicitly excludes it · ? **Unverified** — public evidence is insufficient.

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
| Coding harnesses | **Prime Agent** | ● | ● | ● | ● | ◐ | ◐ |
| General runtimes | **OpenAI Agents SDK** | ● | ● | ● | ● | ● | ● |
| General runtimes | **Google ADK** | ● | ● | ● | ● | ● | ● |
| General runtimes | **Microsoft Agent Framework** | ● | ● | ● | ● | ● | ● |
| General runtimes | **LangGraph** | ● | ◐ | ◐ | ● | ◐ | ◐ |
| Other representative routes | **DeerFlow** | ● | ● | ● | ● | ● | ◐ |
| Other representative routes | **AIOS** | ● | ● | ● | ● | ● | ◐ |
| Other representative routes | **AOHP** | ● | ● | ● | ● | ● | ◐ |
| Other representative routes | **Omnigent** | ● | ● | ◐ | ● | ● | ◐ |

## Curation and Evidence

This is an **opinionated research index**. An entry belongs when it contributes a distinct harness architecture, a directly relevant benchmark, a reusable component, or evidence that changes how runtimes should be built or evaluated.

- **Prefer primary evidence:** source code, official documentation, papers, specifications, and clearly labeled first-party reports.
- **Say why it belongs:** every system and benchmark gets a one-sentence description of its contribution.
- **Keep experimental units separate:** model, harness, environment, task, budget, and evaluator should be named independently.
- **Keep layers separate:** full harnesses, capability modules, security layers, task environments, and evaluation runners are cataloged in their own categories.
- **Track uncertainty:** `Unverified` records insufficient public evidence; an `Absent` rating requires explicit first-party evidence.
- **Record the cutoff:** ratings reflect public evidence available through **2026-10-12** and may change as systems evolve.

---

## Research Library

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

### Research by Engineering Problem

+The hardest harness problems appear where execution, context, state, permissions, and evaluation meet. The nine reading lists below organize papers, benchmarks, and practitioner evidence by engineering problem; every source remains individually visible for scanning and citation.

+#### Security & Sandboxing

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
- <u>Context Engineering</u>: **"Context Engineering Our Way to Long-Horizon Agents"**. *Chase.* Sequoia Capital Podcast, 2026. [[Podcast](https://sequoiacap.com/podcast/context-engineering-our-way-to-long-horizon-agents-langchains-harrison-chase)]
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

## Paper and Citation

The repository currently publishes **Paper v4**. The resource index above is newer and will be incorporated into Paper v5 after the manuscript, figures, and references complete review.

- 📄 [Read Paper v4](./Agent_Harness_for_LLM_Agents__A_Survey__v4.pdf)
- 🌐 [Archived preprint v3](https://www.preprints.org/manuscript/202604.0428/v3)
- 🔗 [DOI: 10.20944/preprints202604.0428.v3](https://doi.org/10.20944/preprints202604.0428.v3)

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

## Contributing

Missing a system, benchmark, paper, or corrected link? [Open an issue](https://github.com/Gloriaameng/Awesome-Agent-Harness/issues) or [submit a pull request](https://github.com/Gloriaameng/Awesome-Agent-Harness/pulls).

A strong contribution includes:

1. The canonical project, paper, or specification link.
2. One sentence explaining why it matters to the harness layer.
3. Primary evidence for architectural claims or quantitative results.
4. The version, commit, benchmark setup, and access date when the claim can drift.
5. The right category: full harness, module, benchmark, task environment, protocol, or evaluation infrastructure.

Corrections and suggestions: gloriamenng@gmail.com · wangyanan@mail.dlut.edu.cn · chenliyi@xiaohongshu.com

## Update Log

| Track | Version | Date | Changes |
|---|---|---|---|
| Resource index | **2026.10** | 2026-10-13 | Rebuilt the README as a navigable Awesome List; expanded every system and benchmark into an individually described entry; retained the evidence matrix and research library |
| Paper | **v4** | 2026-04-14 | Current repository PDF; predates the 2026.10 resource index |
| Archived preprint | **v3** | 2026-04-09 | DOI-linked public preprint |

---

<p align="center">
  <i>† denotes a preprint that was not peer-reviewed at the listed version.</i><br>
  <i>Maintained by Qianyu Meng & Liyi Chen. Curated contributions are welcome.</i>
</p>
