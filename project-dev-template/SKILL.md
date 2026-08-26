---
name: project-dev-template
description: 为代码仓库创建、迁移或审查以 AGENTS.md、长期设计 reference 和项目级 skills 为核心的提示词工程结构。适用于建设新仓库的 AI 协作入口、把现有项目规则抽象成可维护体系，或治理文档与 skill 的归属、路由和重复；不用于代替具体项目设计或直接实施生产代码。
---

# 项目开发提示词模板

把提示词工程视为仓库的一部分：`AGENTS.md` 负责让 agent 找到正确事实，长期 reference 保存人和 agent 共用的稳定设计，项目级 skills 约束特定任务怎样读取、修改和验证。三层共同工作，但不共享正文 Owner。

模板位于 [`references/template/`](references/template/)。它是结构和写法的起点，不是必须完整复制的固定文档集。

## 使用原则

- 先读取目标仓库当前 instructions、目录、构建配置、测试入口和已有文档，再决定需要哪些模板。
- 结构服从项目真实边界；没有对应概念、运行环境或交付链时，不创建空文档或空 skill。
- 每条稳定事实、规则或流程只设一个正文 Owner，其它位置用名称和相对链接路由。
- 先形成能够导航的最小结构，再按真实复杂度拆分；不要把模板标题当作必须填满的表格。
- 模板不授权修改生产代码、部署环境、外部系统或 Git 历史；实际动作仍以用户任务和目标仓库约束为准。

## 分层价值与边界

### 项目入口 `AGENTS.md`

[`references/template/AGENTS.md`](references/template/AGENTS.md) 是仓库级 agent 入口。它回答 agent 在哪里、先读什么、事实归谁、允许改什么、如何验证，不展开设计正文。

当仓库包含相对独立的服务或子项目时，可在其目录增加更窄的 `AGENTS.md`；父级保留总路由，子级只维护本范围差异。README 面向人介绍项目，不作为 agent 规则的替代品。

### 长期设计 `.agents/references/`

[`references/template/.agents/references/`](references/template/.agents/references/) 保存长期有效、可由人审阅的设计。它解释代码本身不能稳定表达的意图、ownership、边界、兼容性和演化方向，不记录任务进度、排查时间线或逐行源码转述。

| 位置 | 整体价值 | 何时读取 |
|---|---|---|
| `concept-design.md` | 对齐项目定位、术语、边界和设计问题 | 需求含义、系统范围或核心概念不清时 |
| `architecture-design.md` | 维护分层、组件关系、依赖方向和生命周期 | 跨能力设计、结构调整或新增主要组件时 |
| `data-design.md` | 维护数据 ownership、共享、并发和清理边界 | 改变数据结构、状态、持久化或跨模块通信时 |
| `api/` | 维护对外可观察的接口和协议契约 | 新增、修改、兼容或评审接口时 |
| `build/` | 维护源码到可发布产物的稳定链路 | 构建、配置生成、制品或发布边界变化时 |
| `capability/` | 维护单项业务或基础能力的长期职责 | 修改能力职责、对象关系或稳定失败语义时 |
| `environment/` | 维护运行拓扑、资源、安全和外部依赖边界 | 部署单元、网络、权限或运行假设变化时 |
| `workflow/` | 按业务动作维护跨能力数据流 | 需要理解一个入口如何改变数据和状态时 |

各文档的具体写法只在对应模板内维护，本文件不重复其章节和问题清单。

### 项目任务规则 `.agents/skills/`

[`references/template/.agents/skills/`](references/template/.agents/skills/) 保存“怎样完成某类任务”的项目级规则。Skill 负责触发条件、读取路由、写入授权、验证责任和交接关系，不承载长期设计正文。

项目级名称使用 `project-<area>-<action>` 形态；实例化时用稳定的仓库、服务或组件 slug 替换 `project`。只有确实依赖项目边界的规则才加项目前缀，跨项目规则保持通用名称。

| 类型 | 模板 | 在生态中的作用 |
|---|---|---|
| 仓库治理 | `project-repository-helper` | 维护协作入口、目录规则和仓库级知识闭环 |
| 文档治理 | `project-docs-helper` | 选择长期事实 Owner 并维护 reference |
| Skill 治理 | `project-skills-helper` | 维护 skill 分类、触发、依赖和追踪边界 |
| 代码实施 | `project-code-implement` | 按代码域读取实现约束并完成聚焦修改 |
| 代码规范 | `project-code-formatting` | 在语言通用规范上叠加项目差异 |
| 模块接入 | `project-module-helper` | 约束新增模块的边界、注册和隔离验证 |
| 代码评审 | `project-code-review` | 以行为风险和契约为中心审查改动 |
| 提交整理 | `project-code-commit-helper` | 只读分析 diff 并生成项目约定的提交信息 |
| 测试体系 | `project-test-verification` | 定义测试级别、资产 ownership 和验证升级规则 |
| 运行探测 | `project-runtime-probe` | 静态证据不足时设计受控、可回收的运行实验 |
| 构建交付 | `project-deploy-build` | 路由构建、制品、配置和部署验证任务 |

模板还携带三个可选通用 skill：`create-architectural-decision-record`、`api-design-principles` 和 `ts-code-formatting`。前两者按任务选用；`ts-code-formatting` 只保留在 TypeScript 项目，其他技术栈应删除或替换，而不是改成名不副实的通用规则。

### 实例化门槛

不要默认复制整套模板。每个候选入口先通过以下判断：

| 候选 | 创建条件 | 不创建时放在哪里 |
|---|---|---|
| 根 `AGENTS.md` | 仓库需要 agent 协作入口 | 根入口始终保留；内容可很短 |
| 子目录 `AGENTS.md` | 子树有独立事实 Owner、读取顺序、修改边界或验证入口，且父级规则不足以表达差异 | 继续使用最近父级 `AGENTS.md` |
| 长期 reference | 已有无法只靠代码/配置稳定推出的长期事实，能指定单一 Owner，并会约束未来设计或兼容性 | 代码、配置、schema、测试或现有 reference |
| 项目级 skill | 某类任务存在项目特有的读取路由、写入授权或验证责任，并会在后续任务重复使用 | `AGENTS.md` 的简短规则或已安装通用 skill |
| Skill supporting reference | 细节只在该任务模式需要，且移出 `SKILL.md` 能避免无关上下文 | 保留在短 `SKILL.md` 正文 |

以下信号单独出现时不足以创建新入口：模板中存在该文件、当前目录看起来相似、只有一次任务需要、内容可从 manifest 或相邻代码直接得到、只能填入通用常识，或无法说明谁负责维护。

对普通已有仓库，先建立一个最小根 `AGENTS.md`，再从已发现的稳定事实反推必要 reference 和 skills。只有评估结果逐项满足上表时，才从完整生态中增加对应模板。

## 实例化流程

### 1. 盘点现状

读取目标仓库适用的 instructions 与 Git 已跟踪内容，识别：

- 项目边界、主要服务和代码入口；
- 已有设计文档、API、构建、环境与测试入口；
- 当前项目级或本地安装 skills；
- 重复、冲突、过期路径和缺少 Owner 的规则。

工作区已有改动属于用户。除非任务明确要求，不清理、不覆盖，也不把本地安装内容自动纳入仓库资产。

### 2. 先定整体结构

先写或修订根 `AGENTS.md` 的仓库地图和读取路由，再确定需要哪些 reference 类型与项目级 skill。此时只决定位置、Owner 和相邻层关系，不先填充所有细节。

### 3. 按类型实例化

只读取当前要生成的模板文件，把其中的问题转化为目标仓库的真实内容：

- 删除说明性占位语句和不适用章节；
- 使用目标仓库的相对路径、稳定对象和公开入口；
- 对未知但重要的项目事实标为待确认，不把模板示例伪装成事实；
- 语言或框架通用 skill 与项目覆盖 skill 分离，项目层只记录差异。

模板文件有两种生命周期：

- 固定入口：`AGENTS.md`、基础设计、`api/http.md`、`build/pipeline.md` 和 `environment/runtime.md` 在满足创建门槛时填充为真实文档，并保留稳定路径。
- 可复制脚手架：`capability/capability.md` 和 `workflow/action.md` 只用于生成具体文件；按真实能力或动作改名后，删除未实例化的通用脚手架，不让项目长期文档依赖这些临时路径。项目 skill 自己的 `references/domain.md`、`references/capability.md` 属于稳定写作与维护指南，实例化项目 skill 时保留。

项目级 skill 只能链接实例化后仍稳定存在的入口。需要引用可复制脚手架时，由本 meta-skill 在实例化期间读取，不把该链接写进目标项目的长期 skill。

### 4. 回看整体

逐项回查 `AGENTS.md`、reference 和 skills：目录说明必须指向真实文件，规则 Owner 唯一，触发描述与正文一致，设计与执行规则没有相互复制。移动或删除入口时同步修复全部活动链接。

## 维护规则

- 新规则写入拥有它的最窄稳定范围；跨范围影响通过链接和同步检查表达。
- 长期 reference 只在独立设计/文档任务或用户明确授权时修改；代码任务产生的实现细节写入对应实施 skill 的 domain reference，并报告长期设计缺口。
- 对外契约、兼容性、数据 ownership 或安全边界变化时，检查上游、下游、测试与迁移说明。
- Skill 的 description 只描述真实能力和触发场景；正文按需路由 supporting references，不做技能百科。
- 新增模板类型前先证明现有 Owner 无法承载；不要用目录数量代表体系完整度。

## 验证

完成创建或迁移后至少确认：

- 所有 `SKILL.md` 具有合法 frontmatter，名称与目录一致；
- 所有相对链接可解析，入口路径没有悬空；
- `AGENTS.md` 路由、实际目录和 Git 跟踪策略一致；
- reference 没有任务记录、原始日志、密钥、局部 helper 转述或互相复制的正文；
- workflow 以数据生产、转换、传递、状态变化、持久化、消费和失败收敛为主体；
- API 文档明确请求、成功、错误、兼容和 Owner；
- 项目级 skills 覆盖其声明的写入与验证责任，且没有扩大用户授权；
- 可复制脚手架已改名为具体 Owner 或删除，固定入口已去除模板说明；再删除不属于目标项目的可选 skill，才把产物视为完成。
