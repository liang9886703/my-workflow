# TypeScript 实现规则

## 命名和变量

| 构造 | 约定 | 示例 |
|---|---|---|
| 变量和函数 | `camelCase` | `getSession` |
| class 和公共类型 | `PascalCase` | `SessionState` |
| 模块常量 | `UPPER_SNAKE_CASE` | `DEFAULT_TIMEOUT_MS` |
| 文件 | 沿用目录现状，新增普通文件优先 `kebab-case.ts` | `event-reader.ts` |

默认使用 `const`，需要重新赋值时使用 `let`，不使用 `var`。命名表达领域含义，不使用无意义缩写或类型后缀

## 函数和 class

- 公共边界和非显然返回值使用显式返回类型，局部可可靠推断时保留推断
- 参数较多且具有可选项、同型值或演进需求时使用 options object，不用固定参数个数作为硬门槛
- 提前返回可以减少嵌套时使用提前返回，拆分函数以职责和控制流清晰为依据
- class 用于实例身份、状态和生命周期，简单无状态操作使用函数
- 优先组合，只有真实 is-a 关系和明确生命周期责任时使用继承

## imports 和模块

- 使用命名导出和类型导入，避免无理由的 default export 和 namespace import
- import 分组跟随当前 formatter 和相邻文件，不为排序单独制造大 diff
- barrel 只承担已有装配职责，不为新功能增加第二个生产公共入口
- 不通过跨层 import、全局 singleton 或动态反查绕过 owner

## 异步和资源

- 使用 `async` 和 `await` 表达主控制流，独立任务才并发执行
- `Promise.all`、`allSettled` 或顺序 await 的选择由失败语义和资源关系决定
- stream、timer、process、reader 和 task 必须有 identity、拥有方、取消和清理路径
- 不使用 `forEach(async ...)`，需要顺序时使用 `for...of`，需要并发时显式构造任务集合

## 错误

不写空 catch，不静默吞掉会影响行为的错误。沿用目标仓库契约选择抛错、结构化错误结果或降级，不为了通用形式强制引入自定义 Error、Result 或 Either

catch 值按 `unknown` 处理并收窄。日志包含操作、必要 identity 和错误信息，避免敏感数据和无界 payload。资源清理由明确的 finally 或 ownership 流程完成

## 注释和格式

注释解释非显然的约束、协议理由和副作用，不重复代码。只有公共边界含义无法由类型和命名表达时才写 TSDoc

使用仓库当前 formatter 和 TypeScript 命令，不在本 reference 硬编码引号、分号或行宽
