# my-workflow

个人可复用的 Codex 工作流与提示词工程模板仓库。

## 当前内容

- [`project-dev-template/`](project-dev-template/)：为代码仓库建立 `AGENTS.md`、长期设计 references 和项目级 skills 的通用模板。

## 使用方式

将需要的 skill 复制或链接到 Codex skills 目录后，按其 `SKILL.md` 的读取路由使用。例如：

```sh
cp -R project-dev-template ~/.codex/skills/
```

`project-dev-template/references/template/` 是可裁剪脚手架，不应未经判断整套复制到目标项目。实例化时先读取目标仓库事实，再决定需要哪些 reference 和项目级 skill。

## 维护原则

- 通用规则与具体项目事实分离，不提交公司内部路径、环境、工单或凭据。
- 每条长期事实只设一个正文 Owner，其它位置只保留摘要和相对链接。
- 修改 skill 后校验 frontmatter、相对链接、模板路由和项目专属残留词。
