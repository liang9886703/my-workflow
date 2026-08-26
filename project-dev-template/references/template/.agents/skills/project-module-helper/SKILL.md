---
name: project-module-helper
description: 当任务需要依照当前项目既有的模块、插件或能力扩展模式新增最小模块壳、注册到 composition root，并验证实例隔离、数据和生命周期接线时使用。
---

# 项目模块接入

`project` 是模板前缀，实例化时统一替换。本 skill 中的“模块”泛指项目已有框架定义的可组合能力单元，不预设必须使用 factory、依赖注入、插件或特定目录。

## 范围

本 skill 负责检查现有扩展模式、创建最小模块边界、从唯一聚合入口导出或注册，并验证创建基数、依赖方向和清理责任。模块内部业务算法、协议和状态机由 `project-code-implement` 负责；改变全局阶段或框架语义需要独立架构决策。

## 先读

- 根 `AGENTS.md` 与当前模块框架、相邻模块和 composition root
- 最小相关的 architecture、data 与 capability reference
- [project-code-implement](../project-code-implement/SKILL.md) 的目标域实现约束
- [project-test-verification](../project-test-verification/SKILL.md) 的测试边界

若当前源码没有稳定扩展协议，或目标模块需要改变框架才能注册，先报告框架缺口；不要在新模块内添加兼容旁路冒充正式接入。

## 接入流程

1. 确认模块契约、创建者、共享基数、输入输出、允许依赖和释放责任
2. 复制既有最小模式，只创建公共入口与完成注册所需的骨架
3. 从项目规定的聚合边界导出或注册，不让 composition root 穿透导入内部文件
4. 把领域逻辑留在模块内部，把外部资源通过既有 port 或依赖边界注入
5. 验证模块能被发现、按正确层级创建、不同 identity 隔离，并在失败或终止时清理

## 写入与交接

只有用户要求新增或调整模块接入时才写生产代码。实现、同目录小型测试和 domain reference 遵守 `project-code-implement`；专用集成资产遵守 `project-test-verification`。

交付时说明采用的现有扩展模式、注册入口、实例与资源 ownership、验证结果，以及未包含的领域实现或框架演化工作。
