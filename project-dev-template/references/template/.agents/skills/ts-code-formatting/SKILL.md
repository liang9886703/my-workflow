---
name: ts-code-formatting
description: 当任务涉及编写、修改、重构或审查 TypeScript 代码，或处理类型建模、imports、文件组织、异步错误、测试和 TypeScript 工具配置时使用。适用于不同 TypeScript 项目
---

# TypeScript 代码规范

提供可跨项目复用的 TypeScript 默认规则和按需读取路由。目标仓库的 instructions、配置和现有代码高于本 skill，项目专属对象、路径和协议不进入本 skill

## 优先级

1. 用户明确要求
2. 目标仓库适用的 agent instructions
3. 当前 `package.json`、`tsconfig.json`、formatter、测试框架和相邻代码
4. 本 skill 的通用默认规则

修改现有代码保持范围聚焦，不借格式或类型任务做无关重构

## 默认底线

- 使用仓库当前类型检查和 module resolution，不擅自开启严格选项或新增工具链
- 避免新增不安全 `any`，外部未知输入优先使用 `unknown` 并在边界收窄
- 让类型表达真实 ownership、生命周期和失败契约
- 公共边界和非显然返回值使用明确类型，局部可可靠推断时保留推断
- 错误不能静默吞掉，异步资源必须有清晰的完成、取消和清理责任
- 使用仓库现有 formatter，不在 skill 中硬编码与项目冲突的格式选项

## 读取路由

| 任务 | 读取 |
|---|---|
| 普通 TypeScript 实现 | `references/code-style.md`、`references/core-code.md`，涉及建模时加 `references/type-system.md` |
| imports、文件组织和 class/function 边界 | `references/code-style.md`、`references/core-code.md` |
| 类型、泛型、null 和类型断言 | `references/type-system.md` |
| 审查或重构 | `references/review-refactor.md`，再按问题读取专项 reference |
| 测试 | `references/testing.md` |
| `tsconfig`、formatter 或 lint 工具 | `references/tooling-config.md` |

## 项目扩展

项目级 skill 可以引用本 skill，并补充本项目的目录入口、领域对象、测试布局、错误模型和运行时工具约束。个人 skill 不反向引用任何项目 skill 名称或仓库路径

## 输出

- 实施时给出符合当前仓库约定的代码和验证结果
- 审查时优先报告 bug、类型漏洞、运行时风险和边界问题
- 通用规则与仓库事实冲突时指出冲突并按仓库事实执行
