<div align="center">

# Codex Skills

**一个面向提交、Minecraft 模组开发、README 润色和多平台 CI 脚手架的个人 Codex 技能集合。**

[English](README.md) | 简体中文

</div>

## 概览

这个仓库存放可复用的 Codex 技能。每个技能都位于独立目录中，并通过带有 front matter 元数据和工作流说明的 `SKILL.md` 描述。

这些技能用于由代理辅助的软件开发流程。用户可以通过类似 `$conventional-commits` 或 `$write-readme-header` 的提示词调用某个聚焦能力。

## 技能

| 技能 | 用途 |
| --- | --- |
| `conventional-commits` | 使用 Conventional Commits 创建 Git 提交，提交主题为带作用域的中文摘要，正文为简洁的项目符号列表。 |
| `minecraft-modder-neoforge` | 辅助 NeoForge Minecraft 模组开发，覆盖物品、方块、实体、配方、数据生成、Mixin、测试和崩溃排查。 |
| `scaffold-multiplatform-ci` | 设计用于质量检查、集成测试、发布准备、平台打包和发布说明的 GitHub Actions 工作流。 |
| `write-readme-header` | 创建紧凑的双语 README 头部，并补全简体中文 README 对应文档。 |

## 仓库结构

```text
.
|-- conventional-commits/
|   |-- SKILL.md
|   `-- agents/openai.yaml
|-- minecraft-modder-neoforge/
|   `-- SKILL.md
|-- scaffold-multiplatform-ci/
|   |-- SKILL.md
|   |-- agents/openai.yaml
|   `-- references/
`-- write-readme-header/
    |-- SKILL.md
    `-- agents/openai.yaml
```

## 使用方式

将这个仓库中的技能目录放到你的 Codex skills 目录下，然后在 Codex 会话中按名称调用技能：

```text
$conventional-commits
$minecraft-modder-neoforge
$scaffold-multiplatform-ci
$write-readme-header
```

每个 `SKILL.md` 都是对应技能行为的权威来源。可选的 `agents/openai.yaml` 文件提供界面元数据，例如显示名称、简介和默认提示词。

## 维护

添加或修改技能时：

- 保持 `SKILL.md` 中的 `name` 字段与目录名一致。
- 编写具体的 `description`，说明技能应在什么场景下使用。
- 将较大的可复用模板、示例或检查清单放入 `references/` 目录，避免无限扩张主说明文件。
- 当技能列表、目录结构或使用模型变化时，同步更新两个 README 文件。

## 许可证

当前仓库没有仓库级许可证文件。在仓库外分发或复用某个技能前，请先检查该技能自身的元数据。
