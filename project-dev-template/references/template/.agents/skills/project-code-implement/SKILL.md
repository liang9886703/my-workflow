---
name: project-code-implement
description: 当任务需要在当前项目中实施、修改或重构生产代码、同目录小型测试、运行时配置或日志时使用；负责按代码域读取当前约束、完成实现并验证，不在代码任务中顺手改写长期设计。
---

# 项目代码实施

`project` 是模板命名空间。实例化时统一替换 skill 名称和相互引用，并根据真实代码域建立 implementation reference 路由。

本 skill 是生产实现入口。长期设计 reference 在代码任务中只读；当前实现必须遵守的非显然约束写入本 skill 的 `references/<domain>.md`，按稳定代码域组织，不按任务创建文档。

## 读取顺序

1. 读取当前作用域的 `AGENTS.md`、用户需求、目标代码、相邻测试与仓库配置
2. 按受影响行为读取最小相关的概念、架构、数据、API、capability、environment 或 workflow reference
3. 读取父域和目标域已有的 `references/<domain>.md`；没有时以代码和长期设计为事实，不猜测隐藏规则
4. 涉及格式、模块接入、测试、构建部署或评审时，同时使用对应项目 skill

创建或维护实现 reference 时读取 [domain reference 写法](references/domain.md)。

## 写入边界

- 可以修改任务范围内的生产代码、同目录或紧邻的小型测试、运行时配置、日志和对应实现 reference
- 专用测试目录、fixture、测试入口与完整验证流程归 `project-test-verification`
- `.agents/references/`、README、`AGENTS.md` 和其它 skill 在普通代码任务中保持只读
- 不为便于测试扩大生产 API、增加旁路入口或暴露 private 状态
- 不把用户已有改动归入任务，也不撤销无关修改

若长期设计与当前实现冲突，不静默选择一方：先依据用户明确目标完成安全范围内的工作；冲突会导致破坏性或对外不兼容变化时停止扩大修改，并报告事实、影响和需要的决定。

## 实施原则

- 从公开入口、composition root、ownership 和依赖方向确定改动落点
- 资源、异步任务、状态与数据必须有明确 owner、identity、生命周期和清理责任
- 延续局部错误、日志、配置和兼容契约，不为统一外观引入新的全局抽象
- 先修复根因，再用最小行为改动保护兼容边界；不顺便重构无关区域
- 纯重命名、拆函数或等价重构通常不更新实现 reference，除非阅读入口或约束发生变化

## 验证与交接

先运行直接证明目标行为的最小测试，再按风险交给 `project-test-verification` 执行相邻或完整验证。构建、部署和真实环境验证分别遵守其专用 skill 的授权边界。

交付必须说明：行为改动、实际验证、修改过的 implementation reference、未覆盖风险，以及建议另开文档任务处理的长期设计候选；没有文档候选时也明确说明。
