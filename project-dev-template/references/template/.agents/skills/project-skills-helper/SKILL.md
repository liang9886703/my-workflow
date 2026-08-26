---
name: project-skills-helper
description: 当用户明确要求为当前项目创建、修改、迁移或评审项目级 skill，或维护 `.agents/skills/` 的分类、触发说明、依赖引用与发现规则时使用。
---

# 项目 Skills 生态维护

`project` 是待替换的模板前缀。实例化时选择稳定、简短的项目标识，并一次性替换目录名、frontmatter、标题和相对引用；通用 skill 保留原名，不套项目名前缀。

本 skill 只维护 skill 及其任务路由，不修改生产代码、测试资产或长期设计正文。

## 读取与分类

- 创建新 skill 时同时使用 `skill-creator`，遵守标准目录、frontmatter、渐进披露和校验规则
- 先读取根 `AGENTS.md`、现有项目 skill 和实际调用方，确认新能力是否已有 Owner
- 项目级 skill 保存仓库特有的入口、边界、事实路由和验证责任
- 通用 skill 不得包含项目名、内部路径、供应商环境或固定命令，应能独立安装到其它项目
- 本地安装、缓存、第三方依赖和没有 `SKILL.md` 的资源包不自动成为项目资产

## 命名与结构

- 名称使用小写字母、数字和连字符，目录名必须与 frontmatter `name` 一致
- 项目级名称采用 `<project>-<domain>-<action>` 或更短的同义结构；避免 `misc`、`common-helper` 等无法路由的名称
- `SKILL.md` 保存用途、边界、核心流程和 reference 路由；具体领域规则按需放入 `references/`
- 只有可复用的确定性操作才增加 `scripts/`，只有交付物素材才增加 `assets/`
- 不创建 README、空 reference 或只为看起来完整而存在的目录

## 修改约束

- 只有显式的 skill 创建、修改、迁移或评审任务才编辑 `.agents/skills/`
- 每条工作规则只有一个正文 Owner；其它 skill 通过名称或相对链接交接
- 更窄领域的写入授权和验证要求优先，skills helper 不借维护路由扩大任务权限
- 引用通用 skill 时使用 skill 名称，不写个人安装路径或机器绝对路径
- 新增、移动或删除 skill 时同步检查 `AGENTS.md`、发现配置、版本控制规则和所有相对入链

## 校验与交接

对新增或修改的每个 skill 运行标准结构校验，并检查名称、description 可发现性、Markdown 链接、资源路由和未完成脚手架。交付时说明新增或调整的触发范围、规则 Owner、依赖关系以及未纳入的项目专属细节。
