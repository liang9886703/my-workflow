# TypeScript 工具配置

目标仓库文件是唯一配置事实源，不使用通用模板覆盖项目运行环境

## 调查

修改前读取 `package.json`、`tsconfig.json`、已有 formatter 或 lint 配置、构建脚本和 CI 入口，并确认 runtime、module resolution、测试框架和输出目标

不要从 skill 假设 strict、NodeNext、ESLint、引号风格、声明文件或 Node runtime 已启用

## 调整原则

- 普通代码或格式任务不新增工具链和严格编译选项
- module、resolution、target 和输出选项必须匹配当前 runtime 与构建入口
- 开启 strict 或额外检查属于独立迁移，需要影响评估、分阶段修复和验收计划
- formatter 没有项目配置时接受当前安装版本的实际输出，不在 skill 中另定义引号和行宽
- 新依赖或工具必须有当前 scripts 无法满足的真实需求，并说明 CI、构建和开发环境影响

修改后运行仓库定义的对应 package script，并检查 runtime、测试和构建是否仍使用一致的解析语义
