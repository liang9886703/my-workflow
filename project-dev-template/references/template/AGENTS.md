# {{PROJECT_NAME}}

本文件是 `{{PROJECT_NAME}}` 的 AI 协作入口。实例化模板时替换项目名，补齐代码与测试路径；此处只维护阅读路由、事实归属和协作边界，不复制项目介绍或设计正文。

## Role

你是本项目的工程协作者。以用户当前任务、仓库现状和下述事实 Owner 为依据完成工作；不把模板中的示例当成项目事实。

## 仓库地图

实例化时用真实仓库边界替换下表，并删除本说明。只列能帮助 agent 选择入口和适用约束的稳定服务、子项目或代码域，不复制完整目录树。

| 范围或服务 | 稳定职责 | 生产入口 | 测试/验证入口 | 构建或运行入口 | 更窄 AGENTS |
|---|---|---|---|---|---|
| `{{SCOPE_PATH}}` | 一句话说明该范围拥有的结果 | manifest、composition root 或公共入口 | 测试目录、测试清单或验证命令的文档入口 | 构建清单、CI job、部署或启动入口 | 没有则写“沿用根规则” |

地图只负责导航：职责设计写入 architecture/capability reference，接口字段写入 API，命令细节写入对应 skill 或仓库脚本。新增子级 `AGENTS.md` 前先确认该子树确有独立读取顺序、修改边界或验证规则。

## 事实 Owner

每条稳定规则或事实只保留一个正文 Owner，其它文档只写摘要和链接：

| 信息类型 | 正文 Owner | 本文件的责任 |
|---|---|---|
| 面向人的项目介绍、安装与快速开始 | `README.md` | 只指路，不复述 |
| AI 阅读顺序、任务路由与协作边界 | `AGENTS.md` | 直接维护 |
| 长期设计原则、稳定契约与演化边界 | `.agents/references/` | 只列入口 |
| 专项任务的执行方法、写入授权与验证责任 | `.agents/skills/` | 只列触发入口 |
| 当前可执行行为与实现细节 | 源码、配置、schema 与测试 | 在任务中读取证据，不搬入本文件 |

文档与实现不一致时，先确认冲突属于“设计尚未落地”“实现偏离设计”还是“文档过期”，再修改唯一 Owner；不要通过在多个位置补写同一段话来掩盖冲突。

## 长期设计路由

按问题读取最小必要集合；跨领域变更先读概念、架构和数据三个基础入口，再读专项文档。

| 问题 | 入口 |
|---|---|
| 项目定位、核心概念、系统边界 | [concept-design.md](.agents/references/concept-design.md) |
| 分层、组件关系、依赖方向、控制边界 | [architecture-design.md](.agents/references/architecture-design.md) |
| 数据 ownership、共享、通信与生命周期 | [data-design.md](.agents/references/data-design.md) |
| 对外接口和接入契约 | [api/](.agents/references/api/) |
| 构建、制品、配置渲染与发布边界 | [build/](.agents/references/build/) |
| 单项能力的职责与稳定设计 | [capability/](.agents/references/capability/) |
| 部署单元、网络、权限和资源约束 | [environment/](.agents/references/environment/) |
| 用户动作或业务入口的数据流 | [workflow/](.agents/references/workflow/) |

目录中的 `concept-design.md`、`architecture-design.md`、`data-design.md` 是基础设计，不充当所有细节的汇总页；专项事实仍由对应子目录文档维护。

## 任务路由

收到任务后读取对应 skill。若任务同时跨越多个类型，先由拥有最终交付物的 skill 主导，再按需读取协作 skill。

| 任务类型 | Skill 入口 |
|---|---|
| 仓库结构与治理 | [project-repository-helper](.agents/skills/project-repository-helper/SKILL.md) |
| 长期文档创建、拆分与同步 | [project-docs-helper](.agents/skills/project-docs-helper/SKILL.md) |
| 项目 skill 生态维护 | [project-skills-helper](.agents/skills/project-skills-helper/SKILL.md) |
| 功能实现与缺陷修复 | [project-code-implement](.agents/skills/project-code-implement/SKILL.md) |
| 代码格式化 | [project-code-formatting](.agents/skills/project-code-formatting/SKILL.md) |
| 模块新增、拆分或边界调整 | [project-module-helper](.agents/skills/project-module-helper/SKILL.md) |
| 代码评审 | [project-code-review](.agents/skills/project-code-review/SKILL.md) |
| 提交信息整理 | [project-code-commit-helper](.agents/skills/project-code-commit-helper/SKILL.md) |
| 分层测试与验收 | [project-test-verification](.agents/skills/project-test-verification/SKILL.md) |
| 真实运行时探测 | [project-runtime-probe](.agents/skills/project-runtime-probe/SKILL.md) |
| 构建和交付制品 | [project-deploy-build](.agents/skills/project-deploy-build/SKILL.md) |

## 读取顺序

1. 读取本文件，确定事实 Owner 和任务 skill。
2. 读取与任务直接相关的长期 reference；涉及边界变化时补读基础设计。
3. 读取目标代码、测试、配置和 schema，确认当前实现，不以文档摘要替代仓库证据。
4. 只有在确有需要时读取相邻能力；不要默认加载整个 `.agents/`。

## 修改边界

- 只修改用户任务覆盖的范围，保留工作区内已有且无关的改动。
- 设计原则写入长期 reference；接口字段写入 API reference；实现细节写入代码或实施 skill 的专项 reference；任务过程和一次性排查记录不进入长期设计。
- 改变名称、职责、依赖、协议、数据 Owner、生命周期或失败语义时，同步检查对应正文 Owner 与直接调用方文档。
- 不在 `AGENTS.md` 中新增完整架构、接口 schema、能力流程或测试命令；这里仅增加或调整路由。
- 真实服务、外部写入、发布和不可逆操作必须取得当前任务明确授权。

## 验证与交付

- 使用任务 skill 指定的最小充分验证，并覆盖本次修改实际触及的边界。
- 文档变更检查相对链接、Owner 唯一性和相邻文档的一致性；代码变更检查测试、类型、格式和构建中适用的部分。
- 无法执行的验证必须说明原因、未覆盖风险和可复现的后续命令，不把“未运行”表述为“已通过”。
