# Repository Instructions

## Repository Purpose

本仓库维护可跨项目复用的 Codex 工作流、skills 和提示词工程模板。仓库内容必须保持通用，不把单一项目的实现、供应商、环境或临时任务状态写成长期规则。

## Repository Map

- `README.md`：面向人的仓库入口、内容索引和使用方式。
- `project-dev-template/SKILL.md`：项目提示词工程模板的总入口、分层价值、读取路由和实例化流程。
- `project-dev-template/agents/openai.yaml`：该 skill 的 UI 元数据。
- `project-dev-template/references/template/`：可复制并按项目裁剪的 `AGENTS.md`、长期 references 和项目级 skills。

目录内更具体的写法由对应模板或嵌套 `SKILL.md` 拥有；根文件只负责仓库级导航和维护边界。

## Change Rules

- 先读取待修改 skill 的完整 `SKILL.md`，再读取它直接路由到的必要 reference。
- 保留模板的目录层级和单一正文 Owner；不要在根说明、模板和 supporting reference 之间复制同一套正文规则。
- 通用模板只写稳定原则、必答问题、授权边界和验证责任；项目实现细节必须留在实例化后的目标仓库。
- 直接复制的第三方或通用 skill 应保持原文；需要改变其正文时，先确认是否应改为项目覆盖层。
- 不提交凭据、私有路径、内部环境名、任务时间线、原始日志、缓存或编辑器状态。
- 不修改用户已有但与当前任务无关的工作区内容。

## Validation

完成修改后至少执行：

1. 对所有 `SKILL.md` 运行 Codex `quick_validate.py`。
2. 校验 Markdown 相对链接不存在悬空引用。
3. 检查 skill 名称与目录、模板目录与顶层路由一致。
4. 检索项目专属术语、内部路径、环境名和凭据残留。
5. 查看 Git diff，确保只包含当前任务拥有的改动。
