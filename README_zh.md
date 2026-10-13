<div align="center">

[English](README.md) | [中文](README_zh.md)

# 大语言模型智能体的 Agent Harness：综述

[![GitHub Stars](https://img.shields.io/github/stars/Gloriaameng/Awesome-Agent-Harness?style=social)](https://github.com/Gloriaameng/Awesome-Agent-Harness)
[![License](https://img.shields.io/badge/License-CC--BY--4.0-blue.svg)](license)
[![Resource Index](https://img.shields.io/badge/Resource%20Index-2026.10-0b7285)](#资源与论文状态)
[![Paper](https://img.shields.io/badge/Paper-v4-orange)](./Agent_Harness_for_LLM_Agents__A_Survey__v4.pdf)
[![DOI](https://img.shields.io/badge/Archived%20DOI-v3-blue)](https://doi.org/10.20944/preprints202604.0428.v3)

</div>

<p align="center">
  <img src="assets/architecture_diagram.png" width="720" alt="H=(E,T,C,S,L,V) 六组件分析框架"/>
</p>

## 资源与论文状态

| 产物 | 当前版本 | 日期 / 资料截止时间 | 说明 |
|---|---|---|---|
| 资源索引 | **2026.10** | 资料审查截至 **2026-10-12** | README 系统与 benchmark 图谱 |
| 仓库论文 | **v4** | 2026-04-14 | [PDF](./Agent_Harness_for_LLM_Agents__A_Survey__v4.pdf) |
| 已归档预印本 | **v3** | 2026-04-09 | [DOI 记录](https://doi.org/10.20944/preprints202604.0428.v3) |
| Paper v5 | 修订中 | — | 正在重构，尚未发布 |

> Agent 行为由 **model–harness–environment configuration** 共同产生。本资源将 harness 视为能力、可靠性、成本与安全结果中重要且经常未被单独报告的共同决定因素。

综述使用 **H = (E, T, C, S, L, V)** 分析公开系统中反复出现的六项治理功能：执行循环、工具注册、上下文管理、状态存储、生命周期钩子与评测接口。组件覆盖用于描述架构，不直接等同于产品成熟度、质量或采用规模。

📄 **[阅读 Paper v4](./Agent_Harness_for_LLM_Agents__A_Survey__v4.pdf)** · 🌐 **[已归档预印本 v3](https://www.preprints.org/manuscript/202604.0428/v3)**
✉️ 纠错与建议：gloriamenng@gmail.com；wangyanan@mail.dlut.edu.cn；chenliyi@xiaohongshu.com

引用当前已归档版本时，请使用：

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

## 🆕 新闻与更新

- **[2026-10-13]** Resource Index 2026.10：重建 20 系统比较集，分离任务环境与 harness benchmark，并补入 harness evolution 与安全评测。
- **[2026-04-14]** Paper v4 与引用更新。
- **[2026-04-09]** 已归档预印本 v3 发布。
- **[2026-04-03]** 首次发布。

## 目录

- [资源与论文状态](#资源与论文状态)
- [概述](#概述)
- [历史时间线](#历史时间线)
- [核心系统矩阵](#核心系统矩阵)
- [Benchmark 图谱](#benchmark-图谱)
- [论文列表](#论文列表)
  - [系统目录](#系统目录)
- [引用](#引用)
- [更新日志](#更新日志)

## 概述

LLM agent 并不只依靠模型推理行动。执行 harness 负责组装观察、调用模型、路由工具、保存状态、执行策略、记录轨迹，并决定任务何时停止或恢复。因此，只报告模型会遗漏被评测系统的重要组成部分。

| 组件 | 符号 | 治理功能 |
|---|:---:|---|
| 执行循环 | **E** | 回合/步骤控制、终止、重试与恢复 |
| 工具注册 | **T** | 类型化工具、路由、校验与结果处理 |
| 上下文管理 | **C** | prompt 组装、检索、压缩与显著性管理 |
| 状态存储 | **S** | 跨回合/会话持久化、checkpoint 与恢复 |
| 生命周期钩子 | **L** | 身份、审批、策略、插桩与拦截 |
| 评测接口 | **V** | 轨迹、中间状态、结果信号与实验集成 |

本索引同时收录同行评审研究、预印本、一方技术文档、源代码和明确标记的业界实践报告。矩阵单元格依据公开一方材料编码；stars 和热度不作为组件证据，也不作为成熟度评分。

## 历史时间线

<p align="center">
  <img src="assets/timeline.png" width="720" alt="Agent Harness的历史演进"/>
</p>

| 年份 | 里程碑 | 意义 |
|------|--------|------|
| 1997–2005 | JUnit, TestNG, xUnit 家族 | 软件测试Harness范式；标准化观察-断言生命周期 |
| 2016 | OpenAI Gym (Brockman et al.) | 强化学习环境Harness框架；step/reset API 成为规范接口 |
| 2022年11月 | ChatGPT 公开发布；LangChain 出现 | 面向LLM的智能体框架萌芽；工具使用成为一级公民 |
| 2023 | ReAct, Toolformer, MemGPT, Reflexion, Voyager, AutoGPT | 核心智能体模式：推理-行动、记忆、反思、技能积累 |
| 2023 | CAMEL, ChatDev, Generative Agents | 多智能体协同；社会仿真Harness |
| 2023 | AgentBench, SWE-bench | 智能体评估基础设施涌现 |
| 2024 | MetaGPT, WebArena, ToolLLM, SWE-agent, OSWorld | 全栈执行器；真实世界环境基准测试 |
| 2024 | CodeAct, LATS, Tree of Thoughts | 结构化动作空间；搜索增强规划 |
| 2024年11月 | Anthropic 发布 MCP 协议 | 工具↔harness 接口标准化 |
| 2025 | HAL、AIOS、LangGraph | 评测基础设施、agent 操作系统与有状态图 runtime |
| 2025 | Google 发布 A2A 协议 | agent↔agent 接口标准化 |
| 2025 | MemoryOS、AgentBound† | 记忆抽象与 runtime 安全执行 |
| 2026年1–10月 | SkillsBench†、Harness-Bench、EVOHARNESSBENCH、HarnessRisk、HarnessSecurity-Bench、LoopsBench、SCLATE | skill 评测、直接 harness 比较、演化、生命周期风险、长时循环与可审计 runtime 基础设施 |

*† 表示预印本，尚未经同行评审*

---

## 核心系统矩阵

核心比较集固定为 **20 个系统**，依据架构相关性、公开证据、活跃维护状态以及是否代表独特 harness 路线选取。评分只描述资料截止时间内可核验的组件覆盖，不是质量排名。

**证据图例：**● 完整——内置且有文档 · ◐ 部分——能力有限、可选或依赖官方扩展 · ○ 缺失——一方材料明确排除 · ? 未核验——公开证据不足。

| Category | System | E | T | C | S | L | V |
|---|---|:---:|:---:|:---:|:---:|:---:|:---:|
| 重点 Coding Harness | **Claude Code** | ● | ● | ● | ◐ | ● | ◐ |
| 重点 Coding Harness | **Codex** | ● | ● | ● | ● | ● | ◐ |
| 重点 Coding Harness | **DeepSeek Harness** | ● | ● | ● | ● | ● | ◐ |
| 重点 Coding Harness | **OpenClaw** | ● | ● | ● | ● | ● | ◐ |
| Coding Harness | **Gemini CLI** | ● | ● | ● | ● | ● | ◐ |
| Coding Harness | **OpenCode** | ● | ● | ● | ● | ● | ◐ |
| Coding Harness | **Goose** | ● | ● | ◐ | ◐ | ● | ◐ |
| Coding Harness | **Grok Build** | ● | ● | ● | ● | ● | ◐ |
| Coding Harness | **Cline** | ● | ● | ◐ | ● | ● | ◐ |
| Coding Harness | **OpenHands** | ● | ● | ● | ● | ● | ◐ |
| Coding Harness | **Deep Agents** | ● | ● | ● | ● | ● | ● |
| Coding Harness | **Prime Agent** | ● | ● | ● | ● | ◐ | ◐ |
| 通用 Runtime | **OpenAI Agents SDK** | ● | ● | ● | ● | ● | ● |
| 通用 Runtime | **Google ADK** | ● | ● | ● | ● | ● | ● |
| 通用 Runtime | **Microsoft Agent Framework** | ● | ● | ● | ● | ● | ● |
| 通用 Runtime | **LangGraph** | ● | ◐ | ◐ | ● | ◐ | ◐ |
| 其他代表路线 | **DeerFlow** | ● | ● | ● | ● | ● | ◐ |
| 其他代表路线 | **AIOS** | ● | ● | ● | ● | ● | ◐ |
| 其他代表路线 | **AOHP** | ● | ● | ● | ● | ● | ◐ |
| 其他代表路线 | **Omnigent** | ● | ● | ◐ | ● | ● | ◐ |

矩阵以一个一方产品或仓库作为一个系统边界。安全扩展、benchmark、能力模块和第三方插件不会为了补全组件而与核心系统合并。

## Benchmark 图谱

Harness 研究需要先区分被改变的对象。任务环境回答 agent 能否完成某类任务；harness benchmark 则尽量固定模型、任务、环境或预算，测量 runtime 设计如何改变行为。

### 1. Harness effect

- [Harness-Bench](https://arxiv.org/abs/2605.27922)：在共享的 sandbox task、环境、预算与评测协议下比较 model–harness configuration。
- [Beyond the Model](https://arxiv.org/abs/2609.32459)：通过组件变化研究 tool registry、context compression、planning、subagent 与 lazy skill。
- [LongHarness Bench](https://arxiv.org/abs/2609.38137)：评测 long-context harness 的准确性和效率。
- [Harness the Memory](https://arxiv.org/abs/2608.15008)：在共享 harness 中跨模型和任务集比较 memory substrate。

### 2. Harness evolution 与 runtime self-improvement

- [EVOHARNESSBENCH](https://arxiv.org/abs/2609.04280)：评测工具、skill 与 agent 随时间变化时的 retention 和 adaptation。
- [SkillOpt](https://arxiv.org/abs/2605.23904)：从带分数的 trajectory 产生有界 skill edit，并使用 held-out gate 决定是否接受。
- [SCLATE](https://arxiv.org/abs/2609.32391)：将 session、scheduled task 与 memory consolidation 放在共享事件时间线上。
- [TaoLive](https://arxiv.org/abs/2608.15763)、[Meta-Harness](https://arxiv.org/abs/2603.28052)、[AutoHarness](https://arxiv.org/abs/2603.03329) 与 [VeRO](https://arxiv.org/abs/2602.22480) 分别研究 harness-aware training、harness optimization、自动生成 harness 与 agents evaluating agents。

### 3. Lifecycle、security 与 audit

- [HarnessRisk](https://arxiv.org/abs/2608.17597)：覆盖 configuration、extension、runtime、persistence、action 与 recovery 阶段。
- [HarnessSecurity-Bench](https://arxiv.org/abs/2610.07639)：比较真实 coding harness 与不同权限设置下的 utility 和 attack effect。
- [Hearsay](https://arxiv.org/abs/2609.32495)：测试 harness 自身生成的记录能否支持独立审计。
- [SandboxEscapeBench](https://arxiv.org/abs/2603.02277)：测试模型能否发现并利用 nested sandbox 中人为植入的错误配置与漏洞。

### 4. Long-horizon loop 与 recovery

- [LoopsBench](https://arxiv.org/abs/2608.00267)、[Long-Horizon-Terminal-Bench](https://arxiv.org/abs/2607.08964)、[SWE-Chain](https://arxiv.org/abs/2605.14415) 与 [ChainSWE](https://arxiv.org/abs/2607.02606) 评测持续开发、累积状态、回归义务与依赖修改。
- [Hell or High Water](https://arxiv.org/abs/2508.11027) 评测外部失败后的恢复。

### 5. Protocol 与 tool substrate

- [DynamicMCPBench](https://arxiv.org/abs/2607.20531)、[MCP-Bench](https://arxiv.org/abs/2508.20453)、[MCP-AgentBench](https://arxiv.org/abs/2509.09734) 与 [MCPAgentBench](https://arxiv.org/abs/2512.24565) 分别测试 live/stateful MCP、端到端结果和工具区分能力。

### 6. Evaluation infrastructure

- [AgentCompass](https://arxiv.org/abs/2607.13705) 分离 benchmark、harness 与 environment。
- [Harbor](https://github.com/harbor-framework/harbor) 支持可替换 agent、model、dataset、container environment、trace 与并行 rollout。
- [HAL](https://arxiv.org/abs/2510.11977) 提供统一执行与 leaderboard 基础设施。

### 任务环境与部署 benchmark

[AgencyBench](https://arxiv.org/abs/2601.11044)、[ClawBench](https://github.com/TIGER-AI-Lab/ClawBench)、[OSWorld](https://github.com/xlang-ai/OSWorld)、[WebArena](https://github.com/web-arena-x/webarena)、[GAIA](https://arxiv.org/abs/2311.12983) 与 [SWE-bench](https://github.com/swe-bench/SWE-bench) 仍然是重要任务环境。报告结果时应同时说明 model、harness、environment、budget 与 evaluation version。

---

## 论文列表

### 历史渊源

#### 软件测试Harness (1990s–2000s)

- <u>JUnit</u>: **"JUnit: A Cook's Tour"**. *Beck & Gamma.* Java Report, 4(5), May 1999. [[存档文章](https://web.archive.org/web/20200101000000/http://junit.sourceforge.net/doc/cookstour/cookstour.htm)]

#### 强化学习环境Harness框架 (2016–2022)

- <u>OpenAI Gym</u>: **"OpenAI Gym"**. *Brockman et al.* arXiv 2016. [[论文](https://arxiv.org/abs/1606.01540)] [[代码](https://github.com/openai/gym)]
- <u>Gymnasium</u>: **"Gymnasium: A Standard Interface for Reinforcement Learning Environments"**. *Towers et al.* NeurIPS 2025. [[论文](https://arxiv.org/abs/2407.17032)] [[代码](https://github.com/Farama-Foundation/Gymnasium)]

#### 早期LLM Agent Harness (2023–2024)

- <u>ReAct</u>: **"ReAct: Synergizing Reasoning and Acting in Language Models"**. *Yao et al.* ICLR 2023. [[论文](https://arxiv.org/abs/2210.03629)] [[代码](https://github.com/ysymyth/ReAct)]
- <u>Toolformer</u>: **"Toolformer: Language Models Can Teach Themselves to Use Tools"**. *Schick et al.* NeurIPS 2023. [[论文](https://arxiv.org/abs/2302.04761)]
- <u>AutoGPT</u>: **"Auto-GPT: An Autonomous GPT-4 Experiment"**. *Gravitas et al.* GitHub 2023. [[代码](https://github.com/Significant-Gravitas/AutoGPT)]
- <u>BabyAGI</u>: **"BabyAGI"**. *Nakajima.* GitHub 2023. [[代码](https://github.com/yoheinakajima/babyagi)]
- <u>HuggingGPT</u>: **"HuggingGPT: Solving AI Tasks with ChatGPT and Its Friends in Hugging Face"**. *Shen et al.* NeurIPS 2023. [[论文](https://arxiv.org/abs/2303.17580)]
- <u>LangChain</u>: **"LangChain: Building Applications with LLMs through Composability"**. *Chase et al.* GitHub 2022. [[代码](https://github.com/langchain-ai/langchain)]

---

### 系统目录

#### 四个重点系统

**Claude Code。** Claude Code 通过统一的 coding-agent loop 连接仓库检查、编辑、命令执行、Web 与 MCP 工具、subagent、skill、hook、权限规则、checkpoint 和会话续接。上下文层组合项目指令、对话状态、工具结果和压缩机制；hook 与 permission mode 将策略判断放进执行路径，transcript 与可观测性集成记录 runtime 行为。本文将其视为垂直集成的 coding harness；CLI 与 Agent SDK 是相关 runtime 能力的不同接口。[[代码](https://github.com/anthropics/claude-code)] [[Agent SDK](https://github.com/anthropics/claude-agent-sdk-python)]

**Codex。** Codex 通过统一 agent runtime 连接仓库探索、编辑、命令执行、验证、sandbox、approval、MCP 工具、skill、subagent 与可恢复 thread。执行循环协调模型请求和工具结果，context compaction 管理增长的历史，持久 rollout 与 thread state 支持跨会话工作，结构化事件和 trace 支持检查与评测；approval 决策与 sandbox 约束保持为明确的 runtime control。CLI、IDE 集成、桌面应用和云端执行是同一 harness 家族的不同使用界面，不作为四个独立系统统计。[[代码](https://github.com/openai/codex)] [[Harness engineering](https://openai.com/index/harness-engineering/)]

**DeepSeek Harness。** DeepSeek Harness 使用 Cordis plugin、profile、bundle 和有序 patch，使 model adapter、agent loop、tool registry、session log、storage、sandbox、compaction、telemetry 与用户界面可组合。持久 session log 是 model context、resume、fork、transcript 和 telemetry 的共同来源；类型化工具执行经过校验与 pre/post-execution policy hook。这些可替换、可逆的边界已经提供实现 harness-level runtime recursive self-improvement 的主要底座：外部优化器可以提出有界的 profile 或 plugin 修改，在 held-out task 上评测，并接受、版本化或回滚候选方案。[[代码](https://github.com/deepseek-ai/deepseek-harness)] [[架构](https://github.com/deepseek-ai/deepseek-harness/blob/master/docs/architecture.md)]

**OpenClaw。** OpenClaw 代表 always-on personal-agent harness，将 channel、session、tool、skill、memory、scheduled work、gateway routing 与 sandbox execution 连接起来。它的代表性来自部署连续性：身份、凭证、channel ingress、后台任务、workspace state 与运行策略不随单次对话结束。明确的 tool/channel 边界、持久 workspace、定时执行与运行日志使长时任务能够恢复和检查。核心 OpenClaw 与 PRISM 等安全扩展分开评估，以保持矩阵中的系统边界一致。[[代码](https://github.com/openclaw/openclaw)]

#### 核心比较系统

- **Coding harness：**[Gemini CLI](https://github.com/google-gemini/gemini-cli)、[OpenCode](https://github.com/anomalyco/opencode)、[Goose](https://github.com/aaif-goose/goose)、[Grok Build](https://github.com/xai-org/grok-build)、[Cline](https://github.com/cline/cline)、[OpenHands](https://github.com/OpenHands/OpenHands)、[Deep Agents](https://github.com/langchain-ai/deepagents)、[Prime Agent](https://github.com/PrimeIntellect-ai/prime-agent)。
- **通用 runtime：**[OpenAI Agents SDK](https://github.com/openai/openai-agents-python)、[Google ADK](https://github.com/google/adk-python)、[Microsoft Agent Framework](https://github.com/microsoft/agent-framework)、[LangGraph](https://github.com/langchain-ai/langgraph)。
- **其他代表路线：**[DeerFlow](https://github.com/bytedance/deer-flow)、[AIOS](https://github.com/agiresearch/AIOS)、[AOHP](https://github.com/aohp-os/aohp)、[Omnigent](https://github.com/omnigent-ai/omnigent)。

#### 扩展目录与相邻层

- **扩展 harness 目录：**[Aider](https://github.com/Aider-AI/aider)、[SWE-agent](https://github.com/SWE-agent/SWE-agent)、[Mastra](https://github.com/mastra-ai/mastra)、[AutoGen](https://github.com/microsoft/autogen)、[MetaGPT](https://github.com/geekan/MetaGPT)、[CAMEL](https://github.com/camel-ai/camel)、[ChatDev](https://github.com/OpenBMB/ChatDev)、[Raven](https://github.com/EverMind-AI/Raven)、[Hermes Agent](https://github.com/nousresearch/hermes-agent)、[SandBase](https://github.com/sandbaseai/sandbase-harness)、[MiMo-Code](https://github.com/XiaomiMiMo/MiMo-Code)、[Open SWE](https://github.com/langchain-ai/open-swe)、[QM](https://github.com/yc-software/qm)、[Eve](https://github.com/vercel/eve)、[Shepherd](https://github.com/shepherd-agents/shepherd)、[YYLO](https://github.com/yylo-dev/yylo)。
- **能力模块与研究模式：**[MemGPT](https://github.com/cpacker/MemGPT)、[Reflexion](https://github.com/noahshinn/reflexion)、[Voyager](https://github.com/MineDojo/Voyager)、[Generative Agents](https://github.com/joonspk-research/generative_agents)、[Concordia](https://github.com/google-deepmind/concordia)、[SkillOpt](https://github.com/microsoft/SkillOpt)。直接说明这些对象的专门作用，不再把较窄范围解释为“不完整的生产 harness”。
- **评测基础设施：**[HAL](https://arxiv.org/abs/2510.11977)、[Harbor](https://github.com/harbor-framework/harbor)、[AgentCompass](https://arxiv.org/abs/2607.13705)、[BrowserGym](https://github.com/ServiceNow/BrowserGym) 及相关 runner 作为基础设施比较，不与 agent 产品混为一类。

### 技术挑战

**范围：**本节归纳反复出现的工程问题。现有 harness 基础设施对这些问题提供了部分方案，而学术原型与部署系统暴露出不同约束。

**评估标准：**对于每项挑战，我们评估：(1) **学术覆盖度**——同行评审解决方案（如有）；(2) **生产成熟度**——是否有任何已部署系统在规模上解决了该问题；(3) **阻塞严重性**——未解决的问题是阻止部署还是仅限制性能。

**横切主题：**大多数挑战源于**组合问题**——单个组件（安全沙箱、记忆存储、评估指标）可以独立工作，但将它们组合成连贯的执行器会浮现涌现性故障。形式化验证、可移植性测试和协议互操作性都需要当前研究尚未解决的组合式推理。

#### 安全与沙箱

**挑战：**智能体沙箱必须防止恶意工具使用，同时允许合法的系统访问——这比传统应用沙箱更困难，因为智能体**有意地**与敏感资源（文件系统、网络API、shell命令）交互。

**技术现状：**SandboxEscapeBench 测量模型能否利用人为设置的易受攻击 sandbox 配置，PRISM 则研究 runtime 拦截与纵深防御。两者共同指向对隔离边界和特权操作策略进行持续测试，但都不等于已经得到适用于所有 agent workload 的通用 sandbox 配置。

**开放问题：**组合式安全属性（证明智能体+Harness+环境满足安全规范）仍未解决。当前防御是反应式的（检测逃逸）而非预防式的（证明逃逸不可能）。

> **证据重点：**SandboxEscapeBench 测试模型能否发现并利用人为植入的 sandbox 错误配置与漏洞。它说明需要持续验证配置并采用纵深防御，不能被解释为正确配置容器的通用逃逸率。

- <u>SandboxEscapeBench</u>†: **"Quantifying Frontier LLM Capabilities for Container Sandbox Escape"**. *Marchand et al.* arXiv 2026. [[论文](https://arxiv.org/abs/2603.02277)]
- <u>InjecAgent</u>: **"InjecAgent: Benchmarking Indirect Prompt Injections in Tool-Integrated Large Language Model Agents"**. *Zhan et al.* arXiv 2024. [[论文](https://arxiv.org/abs/2403.02691)]
- <u>ToolHijacker</u>†: **"Prompt Injection Attack to Tool Selection in LLM Agents"**. *Shi et al.* NDSS 2026. [[论文](https://arxiv.org/abs/2504.19793)]
- <u>Securing MCP</u>†: **"Securing the Model Context Protocol (MCP): Risks, Controls, and Governance"**. *Errico et al.* arXiv 2025. [[论文](https://arxiv.org/abs/2511.20920)]
- <u>SHIELDA</u>†: **"SHIELDA: Structured Handling of Exceptions in LLM-Driven Agentic Workflows"**. *Zhou et al.* arXiv 2025. [[论文](https://arxiv.org/abs/2508.07935)]
- <u>PALADIN</u>†: **"PALADIN: Self-Correcting Language Model Agents to Cure Tool-Failure Cases"**. *Vuddanti et al.* ICLR 2026. [[论文](https://arxiv.org/abs/2509.25238)]
- <u>AgentBound</u>†: **"Securing AI Agent Execution"**. *Bühler et al.* arXiv 2025. [[论文](https://arxiv.org/abs/2510.21236)]
- <u>AgentSpec</u>†: **"Agentspec: Customizable runtime enforcement for safe and reliable llm agents"**. *Wang et al.* arXiv 2025. [[论文](https://arxiv.org/abs/2503.18666)]
- <u>AgentSys</u>†: **"AgentSys: Secure and Dynamic LLM Agents Through Explicit Hierarchical Memory Management"**. *Wen et al.* arXiv 2026. [[论文](https://arxiv.org/abs/2602.07398)]
- <u>Docker</u>: **"Docker: Lightweight Linux Containers for Consistent Development and Deployment"**. *Merkel.* Linux Journal 2014(239). [[论文](https://www.linuxjournal.com/content/docker-lightweight-linux-containers-consistent-development-and-deployment)]
- <u>gVisor</u>: **"The True Cost of Containing: A gVisor Case Study"**. *Young et al.* HotCloud '19. [[论文](https://www.usenix.org/conference/hotcloud19/presentation/young)]
- <u>Firecracker</u>: **"Firecracker: Lightweight Virtualization for Serverless Applications"**. *Agache et al.* NSDI 2020. [[论文](https://www.usenix.org/conference/nsdi20/presentation/agache)]
- <u>WebAssembly</u>: **"Bringing the Web up to Speed with WebAssembly"**. *Haas et al.* PLDI 2017. [[论文](https://doi.org/10.1145/3062341.3062363)]
- <u>Indirect Prompt Injection</u>: **"Not What You've Signed Up For: Compromising Real-World LLM-Integrated Applications with Indirect Prompt Injection"**. *Greshake et al.* AISec 2023. [[论文](https://arxiv.org/abs/2302.12173)]
- <u>Misevolution Risks</u>†: **"Your agent may misevolve: Emergent risks in self-evolving llm agents"**. *Shao et al.* arXiv 2025. [[论文](https://arxiv.org/abs/2509.26354)]
- <u>Security Threat Modeling</u>†: **"Security Threat Modeling for Emerging AI-Agent Protocols: A Comparative Analysis of MCP, A2A, Agora, and ANP"**. *Anbiaee et al.* arXiv 2026. [[论文](https://arxiv.org/abs/2602.11327)]
- <u>AgentHarm</u>†: **"AgentHarm: A Benchmark for Measuring Harmfulness of LLM Agents"**. *Andriushchenko et al.* arXiv 2024. [[论文](https://arxiv.org/abs/2410.09024)]
- <u>TrustAgent</u>: **"TrustAgent: Towards Safe and Trustworthy LLM-Based Agents"**. *Hua et al.* EMNLP 2024. [[论文](https://arxiv.org/abs/2402.01586)]
- <u>ToolEmu</u>†: **"Identifying the Risks of LM Agents with an LM-Emulated Sandbox"**. *Ruan et al.* arXiv 2023. [[论文](https://arxiv.org/abs/2309.15817)]
- <u>Ignore Previous Prompt</u>: **"Ignore Previous Prompt: Attack Techniques For Language Models"**. *Perez & Ribeiro.* NeurIPS ML Safety Workshop 2022. [[论文](https://arxiv.org/abs/2211.09527)]

#### 评估与基准测试

> **证据重点：**Harness 评测需要同时报告 runtime、environment、task version、budget、trajectory capture 与 evaluator。HAL、OSWorld 和 METR 分别展示执行方差、评测器误差以及 benchmark 接受与人工审查之间的差异。

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
- <u>PerspectiveGap</u>†: **"PerspectiveGap: A Benchmark for Multi-Agent Orchestration Prompting"**. *Sun et al.* arXiv 2026. [[论文](https://arxiv.org/abs/2606.08878)] [[代码](https://github.com/WhymustIhaveaname/PerspectiveGap)]
- <u>TraceDance</u>†: **"TraceDance: An Automated System for Building Agent Behavior Benchmarks from Real-World Agent Deployment Traces"**. *Min et al.* arXiv 2026. [[论文](https://arxiv.org/abs/2609.33295)] [[项目](https://zhishanq.github.io/TraceDance/)]
  - 从部署轨迹构建特定行为的评测集，在固定的已记录 harness 上下文中评估模型的下一轮输出，不执行其动作，也不重放环境。

#### 协议标准化

> **证据重点：**MCP、A2A、ACP 等协议处在不同接口层。协议的作用取决于语义、状态处理、授权、错误行为与可测试的互操作性，不能只比较协议名称。

- <u>MCP</u>: **"Model Context Protocol"**. *Anthropic.* Technical Report 2024. [[Spec](https://modelcontextprotocol.io)]
- <u>A2A</u>: **"Agent-to-Agent Protocol"**. *Google.* Technical Report 2025. [[规范](https://a2a-protocol.org/latest/)] [[公告](https://developers.googleblog.com/en/a2a-a-new-era-of-agent-interoperability/)]
- <u>Protocol Comparison</u>†: **"A Survey of Agent Interoperability Protocols: Model Context Protocol (MCP), Agent Communication Protocol (ACP), Agent-to-Agent Protocol (A2A), and Agent Network Protocol (ANP)"**. *Ehtesham et al.* arXiv 2025. [[论文](https://arxiv.org/abs/2505.02279)]
- <u>Gorilla</u>: **"Gorilla: Large Language Model Connected with Massive APIs"**. *Patil et al.* NeurIPS 2023. [[Paper](https://arxiv.org/abs/2305.15334)] [[Code](https://github.com/ShishirPatil/gorilla)]

#### 运行时上下文管理

> **证据重点：**SkillsBench 与长上下文研究表明，增加上下文本身并不足够；选择、位置、压缩、来源和冲突处理共同决定新增材料是否真正帮助 agent。

- <u>SkillsBench</u>†: **"SkillsBench: Benchmarking How Well Agent Skills Work Across Diverse Tasks"**. *Li et al.* arXiv 2026. [[Paper](https://arxiv.org/abs/2602.12670)]
- <u>ReadAgent</u>: **"A Human-Inspired Reading Agent with Gist Memory of Very Long Contexts"**. *Lee et al.* ICML 2024. [[Paper](https://arxiv.org/abs/2402.09727)]
- <u>MemoryOS</u>: **"Memory OS of AI Agent"**. *Kang et al.* arXiv 2025. [[Paper](https://arxiv.org/abs/2506.06326)]
- <u>CoALA</u>: **"Cognitive Architectures for Language Agents"**. *Sumers et al.* TMLR 2024. [[Paper](https://arxiv.org/abs/2309.02427)]
- <u>SkillFortify</u>†: **"Formal Analysis and Supply Chain Security for Agentic AI Skills"**. *Bhardwaj.* arXiv 2026. [[Paper](https://arxiv.org/abs/2603.00195)]
- <u>Lost in the Middle</u>: **"Lost in the Middle: How Language Models Use Long Contexts"**. *Liu et al.* TACL 2024. [[Paper](https://arxiv.org/abs/2307.03172)]
- <u>Context Engineering Survey</u>†: **"Context Engineering: A Survey of 1,400 Papers on Effective Context Management for LLM Agents"**. *Mei et al.* arXiv 2025. [[Paper](https://arxiv.org/abs/2507.13334)]

#### 工具使用与注册

> **证据重点：**工具可靠性不只取决于工具数量。工具选择、类型契约、语义授权、结果校验和恢复策略会在执行循环中共同作用。

- <u>CodeAct</u>: **"Executable Code Actions Elicit Better LLM Agents"**. *Wang et al.* ICML 2024. [[Paper](https://arxiv.org/abs/2402.01030)] [[Code](https://github.com/xingyaoww/code-act)]
- <u>Schema First</u>†: **"Schema First Tool APIs for LLM Agents: A Controlled Study of Tool Misuse, Recovery, and Budgeted Performance"**. *Sigdel & Baral.* arXiv 2026. [[Paper](https://arxiv.org/abs/2603.13404)]
- <u>ToolLLM</u>: **"ToolLLM: Facilitating Large Language Models to Master 16000+ Real-world APIs"**. *Qin et al.* ICLR 2024. [[Paper](https://arxiv.org/abs/2307.16789)] [[Code](https://github.com/OpenBMB/ToolBench)]
- <u>ToolSandbox</u>†: **"ToolSandbox: A Stateful, Conversational, Interactive Evaluation Benchmark for LLM Tool Use Capabilities"**. *Lu et al.* arXiv 2024. [[Paper](https://arxiv.org/abs/2408.04682)]
- <u>AutoTool</u>†: **"AutoTool: Efficient Tool Selection for Large Language Model Agents"**. *Jia & Li.* AAAI 2026. [[Paper](https://arxiv.org/abs/2511.14650)]
- <u>Tool Learning Survey</u>: **"Tool Learning with Large Language Models: A Survey"**. *Qu et al.* Frontiers of Computer Science 2024. [[Paper](https://arxiv.org/abs/2405.17935)]
- <u>GoEX</u>†: **"GoEX: Perspectives and Designs Towards a Runtime for Autonomous LLM Applications"**. *Patil et al.* arXiv 2024. [[Paper](https://arxiv.org/abs/2404.06921)]
- <u>AgentTuning</u>: **"AgentTuning: Enabling Generalized Agent Abilities for LLMs"**. *Zeng et al.* ACL 2024. [[Paper](https://arxiv.org/abs/2310.12823)]

#### 记忆架构

> **证据重点：**记忆系统需要在检索质量、写入策略、时间一致性、来源、延迟与成本之间取舍。没有一种 substrate 能在所有任务类型和交互时域中稳定占优。

- <u>Agent Workflow Memory (AWM)</u>†: **"Agent Workflow Memory"**. *Wang et al.* arXiv 2024. [[Paper](https://arxiv.org/abs/2409.07429)]
- <u>Mem0</u>†: **"Mem0: Building Production-Ready AI Agents with Scalable Long-Term Memory"**. *Khant et al.* arXiv 2025. [[Paper](https://arxiv.org/abs/2504.19413)]
- <u>A-MEM</u>†: **"A-MEM: Agentic Memory for LLM Agents"**. *Xu et al.* NeurIPS 2025. [[Paper](https://arxiv.org/abs/2502.12110)]
- <u>MemAct</u>†: **"Memory as Action: Autonomous Context Curation for Long-Horizon Agentic Tasks"**. *Zhang et al.* arXiv 2025. [[Paper](https://arxiv.org/abs/2510.12635)]
- <u>Memory Survey</u>†: **"Memory for Autonomous LLM Agents: Mechanisms, Evaluation, and Emerging Frontiers"**. *Du.* arXiv 2026. [[Paper](https://arxiv.org/abs/2603.07670)]
- <u>MemoryBank</u>: **"MemoryBank: Enhancing Large Language Models with Long-Term Memory"**. *Zhong et al.* AAAI 2024. [[Paper](https://arxiv.org/abs/2305.10250)]
- <u>LoCoMo</u>†: **"Evaluating Very Long-Term Conversational Memory of LLM Agents"**. *Maharana et al.* arXiv 2024. [[Paper](https://arxiv.org/abs/2402.17753)]
- <u>Memory Mechanisms Survey</u>†: **"A Survey on the Memory Mechanism of Large Language Model Based Agents"**. *Zhang et al.* arXiv 2024. [[Paper](https://arxiv.org/abs/2404.13501)]
- <u>Evo-Memory</u>†: **"Evo-Memory: Benchmarking LLM Agent Test-time Learning with Self-Evolving Memory"**. *Wei et al.* arXiv 2025. [[Paper](https://arxiv.org/abs/2511.20857)]

#### 规划与推理

> **关键数据：**SWE-agent ACI 研究表明，接口设计超越模型能力成为性能的首要决定因素。LATS 将MCTS与语言模型反馈集成用于状态空间搜索。Plan-on-Graph通过引导、记忆和反思机制在知识图谱上实现自适应自我修正规划。

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


#### 多智能体协同

> **证据重点：**[AgencyBench](https://arxiv.org/abs/2601.11044) 报告闭源模型整体表现为 48.4%，开源模型为 32.1%，并另行观察到部分专有系统的原生生态优势。48.4% 不是原生 SDK 的成功率。

<p align="center">
  <img src="assets/multi_agent_topology.png" width="680" alt="多智能体协同拓扑"/>
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
- <u>PEvo</u>: **"Implicit Behavioral Alignment of Language Agents in High-Stakes Crowd Simulations"**. *Wang et al.* EMNLP 2025. [[论文](https://arxiv.org/abs/2509.16457)]
- <u>Agon</u>†: **"Agon: An Autonomous Large-Scale Omnidisciplinary Research System Built on Prompt Economy"**. *Sun et al.* arXiv 2026. [[论文](https://arxiv.org/abs/2606.24177)] [[代码](https://github.com/AutoResearch-Factory/Agon)]

#### 计算经济学

> **证据重点：**Harness economics 应同时报告 token、wall-clock time、工具与环境成本、并发、重试、失败工作和结果质量。只报告吞吐量无法描述长时 agent task 的真实成本。

- <u>State of AI Report</u>: **"State of AI: An Empirical 100 Trillion Token Study with OpenRouter"**. *Aubakirova et al.* Andreessen Horowitz (a16z) and OpenRouter Inc., December 2025. [[报告](https://openrouter.ai/state-of-ai)]
- <u>BentoML Inference Report</u>: **"Beyond Tokens-per-Second: How to Balance Speed, Cost, and Quality in LLM Inference"**. *Yang.* BentoML Blog, January 2026. [[博客](https://www.bentoml.com/blog/beyond-tokens-per-second-how-to-balance-speed-cost-and-quality-in-llm-inference)]
- <u>H100 Price Spike</u>: **"H100 Price Spike: Understanding the 10% Surge in GPU Rental Costs"**. *Li.* Silicon Data Blog, January 2026. [[博客](https://www.silicondata.com/blog/h100-price-spike)]
- <u>NVIDIA GTC 2026</u>: **"NVIDIA GTC 2026: Live Updates on What's Next in AI"**. *NVIDIA.* NVIDIA Blog, March 2026. [[博客](https://blogs.nvidia.com/blog/gtc-2026-news/)]
- <u>Repo2Run</u>†: **"Repo2Run: Automated Building Executable Environment for Code Repository at Scale"**. *Hu et al.* arXiv 2025. [[Paper](https://arxiv.org/abs/2502.13681)]
- <u>Policy-First</u>†: **"Guardrails as Infrastructure: Policy-First Control for Tool-Orchestrated Workflows"**. *Sigdel & Baral.* arXiv 2026. [[Paper](https://arxiv.org/abs/2603.18059)]
- <u>Strong-Weak Collaboration</u>: **"An Empirical Study on Strong-Weak Model Collaboration for Repo-level Code Generation"**. *Gandhi et al.* EMNLP 2025. [[论文](https://aclanthology.org/2025.emnlp-main.1043/)] [[代码](https://github.com/shubhamrgandhi/codegen-strong-weak-collab)]

---

### 新兴主题

- <u>AutoRef</u>†: **"AutoRef: Harness Optimization for Agentic Multi-Reference Image Generation"**. *Oshima et al.* arXiv 2026. [[论文](https://arxiv.org/abs/2609.35530)] [[代码](https://github.com/KuOnoda/AutoRef)]
- <u>Harness Engineering for Language Agents</u>†: **"Harness Engineering for Language Agents: The Harness Layer as Control, Agency, and Runtime"**. *He et al.* Preprints 2026. [[论文](https://www.preprints.org)]
- <u>DeepAgent</u>†: **"Deepagent: A general reasoning agent with scalable toolsets"**. *Li et al.* arXiv 2025. [[论文](https://arxiv.org/abs/2510.21618)]
- <u>Natural-Language Harnesses</u>†: **"Natural-Language Agent Harnesses"**. *Pan et al.* arXiv 2026. [[论文](https://arxiv.org/abs/2603.25723)]
- <u>Self-Evolving Agents Survey</u>†: **"A Survey of Self-Evolving Agents: What, When, How, and Where to Evolve on the Path to Artificial Super Intelligence"**. *Gao et al.* TMLR 2026. [[论文](https://arxiv.org/abs/2507.21046)]
- <u>Self-RAG</u>: **"Self-RAG: Learning to Retrieve, Generate, and Critique Through Self-Reflection"**. *Asai et al.* ICLR 2024. [[论文](https://arxiv.org/abs/2310.11511)]
- <u>Constitutional AI</u>: **"Constitutional AI: Harmlessness from AI Feedback"**. *Bai et al.* arXiv 2022. [[论文](https://arxiv.org/abs/2212.08073)]
- <u>AppAgent</u>†: **"AppAgent: Multimodal Agents as Smartphone Users"**. *Zhang et al.* arXiv 2023. [[论文](https://arxiv.org/abs/2312.13771)]

#### 相关综述

- <u>LLM Agents Survey</u>: **"A Survey on Large Language Model Based Autonomous Agents"**. *Wang et al.* arXiv 2023. [[Paper](https://arxiv.org/abs/2308.11432)]
- <u>Rise of LLM Agents</u>: **"The Rise and Potential of Large Language Model Based Agents: A Survey"**. *Xi et al.* arXiv 2023. [[Paper](https://arxiv.org/abs/2309.07864)]
- <u>LLM Survey</u>: **"A Survey of Large Language Models"**. *Zhao et al.* arXiv 2023. [[Paper](https://arxiv.org/abs/2303.18223)]
- <u>AI Agent Systems</u>†: **"AI Agent Systems: Architectures, Applications, and Evaluation"**. *Xu.* arXiv 2025. [[Paper](https://arxiv.org/abs/2601.01743)]
- <u>AutoResearch Survey</u>†: **"What's Missing in Autonomous Research? A Systematization of Systems, Benchmarks, and Verification"**. *Ren et al.* 2026. [[论文](https://www.researchgate.net/publication/406952713)]
- <u>LLM Agents: A Survey</u>†: **"LLM Agents: A Survey"**. *Lee.* Preprints.org 2026. [[Paper](https://www.preprints.org/manuscript/202608.0265/v1)]
- <u>The Agent Loop</u>†: **"The Agent Loop: A Survey of Control Strategies, Skills, and Harnesses for LLM Agents"**. *Lee and Park.* SSRN 2026. [[Paper](https://github.com/js-lee-AI/awesome-agent-loop-papers/blob/main/paper/the-agent-loop-survey.pdf)]

#### 业界实践报告与洞察

> 来自 Stripe、OpenAI、Cursor、METR 及其他前沿实践者的生产部署经验。

- <u>Building Effective Agents</u>: **"Building Effective Agents"**. *Anthropic.* Anthropic Engineering Blog, 2026. [[博客](https://www.anthropic.com/engineering)]
- <u>Demystifying Evals</u>: **"Demystifying Evals for AI Agents"**. *Anthropic.* Anthropic Engineering Blog, 2026. [[博客](https://www.anthropic.com/engineering)]
- <u>Context Engineering</u>: **"Context Engineering Our Way to Long-Horizon Agents"**. *Chase.* Sequoia Capital Podcast, 2026.
- <u>Agent Frameworks, Runtimes, and Harnesses</u>: **"Agent Frameworks, Runtimes, and Harnesses"**. *LangChain.* LangChain Blog, 2025. [[博客](https://blog.langchain.com/agent-frameworks-runtimes-and-harnesses-oh-my/)]
- <u>We Removed 80% of Our Agent's Tools</u>: **"We Removed 80% of Our Agent's Tools"**. *Qu.* Vercel Engineering Blog, 2025. [[博客](https://vercel.com/blog/we-removed-80-percent-of-our-agents-tools)]
- <u>Harness Problem</u>: **"I Improved 15 LLMs at Coding in One Afternoon. Only the Harness Changed."**. *Can.* Personal blog (blog.can.ac), February 2026. [[博客](https://blog.can.ac/2026/02/12/the-harness-problem/)]
- <u>AI Adoption Journey</u>: **"My AI Adoption Journey"**. *Hashimoto.* Personal blog, February 2026. [[博客](https://mitchellh.com/writing/my-ai-adoption-journey)]
- <u>The Harness Gap</u>: **"The Harness Gap: AI Coding Output Rose 59% in 2025 While Teams Shipped 7% Less"**. *Zoom In AI.* Medium (Write A Catalyst), March 2026. [[博客](https://medium.com/write-a-catalyst/the-harness-gap-ai-coding-output-rose-59-in-2025-while-teams-shipped-7-less-082d3d07cff8)]
- <u>Stripe Minions</u>: **"Minions: Stripe's one-shot, end-to-end coding agents"**. *Gray.* Stripe Dev Blog, Feb 2026. [[博客](https://stripe.dev/blog/minions-stripes-one-shot-end-to-end-coding-agents)]
- <u>Harness Engineering (OpenAI)</u>: **"Harness engineering: leveraging Codex in an agent-first world"**. *Lopopolo.* OpenAI Blog, Feb 2026. [[博客](https://openai.com/index/harness-engineering/)]
- <u>Self-Driving Codebases</u>: **"Towards self-driving codebases"**. *Lin.* Cursor Blog, Feb 2026. [[博客](https://cursor.com/blog/self-driving-codebases)]
- <u>METR SWE-bench Analysis</u>: **"Many SWE-bench-Passing PRs Would Not Be Merged into Main"**. *Whitfill et al.* METR Notes, Mar 2026. [[报告](https://metr.org/notes/2026-03-10-many-swe-bench-passing-prs-would-not-be-merged-into-main/)]
- <u>Harness-Aware Training</u>†: **"Training Agents to Evolve with Their Harness: TaoLive Digital Avatar Agent Technical Report"**. *TaoLive AIGC LLM Team.* arXiv, August 2026. [[论文](https://arxiv.org/abs/2608.15763)]

---

### 未来方向

综述中识别的八个开放研究方向（无精选论文列表——这些是前瞻性方向）：

- **形式化Agent Harness规范语言** — 用于指定和验证 H=(E,T,C,S,L,V) 组件的领域特定语言（DSL）
- **跨Agent Harness基准测试套件** — 跨不兼容执行器生态系统的可移植性测试
- **安全分类与威胁模型** — 将OWASP Top 10扩展至智能体执行器攻击面
- **协议互操作性（MCP/A2A）** — 桥接工具级和智能体级协议
- **长时域评估方法论** — 在多会话、多天任务下不会退化的指标
- **Agent Harness感知微调** — 训练模型使其感知执行环境
- **记忆接口标准化** — 跨平面式、情节式和图式存储的可移植记忆API
- **Agent Harness透明性规范** — 运行时决策的可审计性和可解释性

---

## 引用

参见本 README 顶部的 BibTeX 引用格式。

---

## 更新日志

| 版本 | 日期 | 变更 |
|------|------|------|
| Resource 2026.10 | 2026-10-13 | 重建系统矩阵与 benchmark 图谱，修正链接和定量表述 |
| Paper v4 | 2026-04-14 | 仓库 PDF；论文修订时间早于 2026.10 资源索引 |
| 已归档预印本 v3 | 2026-04-09 | DOI 对应的公开预印本 |

---

<p align="center">
  <i>† 表示预印本，尚未经同行评审。</i><br>
  <i>本综述正在积极开发中；完整手稿将于近期发布。</i><br>
  <i>由 Qianyu Meng， Yanan Wang与 Liyi Chen 维护。欢迎提交缺失论文或更新链接的 PR。</i>
</p>
