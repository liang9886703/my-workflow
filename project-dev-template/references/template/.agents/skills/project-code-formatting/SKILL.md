---
name: project-code-formatting
description: 修改当前项目生产代码时使用，用于在语言通用规范之上应用仓库特有的目录入口、导入边界、错误与日志、测试布局和工具配置约束；不负责重新定义业务架构。
---

# 项目代码规范覆盖

`project` 是模板前缀，实例化时统一替换。再按实际技术栈选择通用语言规范；TypeScript 项目可配合 `ts-code-formatting`，其它项目应删除或替换该可选 skill，而不是照搬 TypeScript 规则。

## 读取顺序

1. 读取所选语言或框架的通用规范
2. 读取根 `AGENTS.md` 和 [project-code-implement](../project-code-implement/SKILL.md) 路由的目标域约束
3. 读取当前 manifest、编译器、formatter、linter、相邻代码和测试配置
4. 只有稳定对象或能力边界受影响时才读直接相关长期 reference

实际仓库配置和既有公共入口是事实来源；不要用通用模板覆盖项目的 module resolution、运行时或测试框架。

## 项目覆盖

- 目录和入口：落实公共入口、内部文件、composition root 与允许的导入方向
- 类型和资源：让代码表达既定 ownership、identity、生命周期和清理边界
- 错误和日志：沿用局部失败契约、结构化字段、脱敏和可观测性要求
- 测试可见性：通过公共行为或既有测试边界验证，不为测试新增生产旁路
- 工具配置：修改配置时确认 formatter、类型检查、测试、构建和运行时采用一致解析语义

本 skill 不重复通用语言样式，也不拥有 capability、API 或 implementation reference 的设计正文。

## 验证与输出

运行仓库定义的格式检查、静态检查和受影响测试；只有用户明确要求时才执行会重写无关文件的批量格式化。输出说明采用的通用规范、项目覆盖、配置事实源、验证结果和仍需项目级检查的行为。
