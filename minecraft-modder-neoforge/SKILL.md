---
name: minecraft-modder-neoforge
description: Minecraft NeoForge 模组开发规范与参考。用于创建新模组、添加物品/方块/实体、编写配方（RecipeProvider）、注册（DeferredRegister）、数据生成（datagen）、Mixin、Access Transformer、单元测试或排查模组崩溃时加载；默认基于 NeoForge 26.1.2 与 Minecraft 26.1.2。
---

# Minecraft NeoForge 模组开发规范

## reference/ 导航

| 文档 | 内容 |
| --- | --- |
| [reference/project-setup.md](reference/project-setup.md) | 目录结构、Gradle 构建/运行命令、模板仓库、许可证约定、资源文件要求与开发工具配置 |
| [reference/registration.md](reference/registration.md) | `DeferredRegister` 注册规范、`Item.Properties().setId(...)` 强制用法与 `Identifier` 变更 |
| [reference/datagen.md](reference/datagen.md) | Datagen 资源生成规范、`GatherDataEvent.Client` 入口与各 `Provider` 用法 |
| [reference/mixin-at.md](reference/mixin-at.md) | Mixin 启用配置与 `accesstransformer.cfg` 语法 |
| [reference/testing.md](reference/testing.md) | JUnit 单元测试、`testframework` 服务端测试（`EphemeralTestServerProvider`）与 GameTest |
| [reference/anvillib.md](reference/anvillib.md) | AnvilLib 模块列表、Gradle 版本目录引入方式与 Maven 仓库地址 |
| [reference/source-reading.md](reference/source-reading.md) | 查阅依赖 `-sources.jar`、命令行反编译与参考开源模组的许可证规范 |
| [reference/tasks.md](reference/tasks.md) | 常见开发任务的交付内容与验收标准 |
| [reference/external/](reference/external/) | 官方文档、迁移 Primers（中英文）、Mixin 教程与 AnvilLib 清单的本地镜像 |

## 编码前核查与文档查阅

1. **澄清歧义与简化方案**：需求存在多种理解时，必须先列出可选方案交由用户确认，禁止自行猜测；存在更直接的实现方式时，必须主动提出（例如只需新增单个普通物品时，直接注册该物品，禁止搭建多层抽象注册框架）。
2. **先查文档再写代码**：禁止凭记忆猜测 API 类名、方法签名、最新版本号或配置格式。涉及不熟悉或跨版本变动的 API 时，优先读取 [reference/external/](reference/external/) 下的本地镜像（2026-09-20 抓取）；本地镜像未覆盖或已过期时，查阅在线原链接并同步更新对应镜像文件。若官方文档与源码均无对应 API，直接向用户说明并提供替代方案，禁止编造 API：
   - NeoForge 官方文档：[neoforged-docs-home.md](reference/external/neoforged-docs-home.md)（https://docs.neoforged.net/ ）
   - 版本迁移 Primers：[neoforged-primers-index.md](reference/external/neoforged-primers-index.md)（https://docs.neoforged.net/primer/docs/ ）、中文翻译 [porting-primers-zh-index.md](reference/external/porting-primers-zh-index.md)（https://gu-zt.github.io/Porting-Primers/ ）
   - Mixin 教程与参考：[mixin-introduction-zh.md](reference/external/mixin-introduction-zh.md)、[mixin-examples-zh.md](reference/external/mixin-examples-zh.md)、[mixin-wiki-home.md](reference/external/mixin-wiki-home.md)
3. **26.1 关键 API 变更**：`ResourceLocation` 已更名为 `Identifier`（1.21.11 起）；构建环境升级至 Java 25 并默认反混淆、验证机制重做、新增标签提供者与数据组件初始化器（26.1 起）；模型系统（1.21.5）与渲染管线（1.21.11）均已重做。完整变更索引见 [porting-primers-zh-index.md](reference/external/porting-primers-zh-index.md)。

## 工程与编码约束

- **默认版本与构建工具**：除非用户指定其他加载器或版本，默认使用 NeoForge 26.1.2、Minecraft 26.1.2 与官方推荐的 ModDevGradle（MDG）。
- **包结构职责分离**：注册项（`init/`）、事件监听、网络包（`network/`）、数据生成（`data/`）与客户端专属逻辑（`client/`）必须分包存放。
- **代码格式与注释**：Java 源码必须显式写出 `import` 语句，禁止在代码体中内联全限定类名；关键公开方法添加简体中文注释与 Javadoc。
- **最简实现**：只编写完成当前需求所需的代码；禁止为单次使用的物品或方块引入抽象工厂、建造者模式或未要求的配置项，禁止为不可能触发的分支编写防御代码。
- **最小改动范围**：修改已有模组时只改动与当前请求直接相关的代码，保持既有代码风格；清理因本次修改新产生的未使用 `import`、变量或方法，禁止顺手重构无关代码或跨范围删除既有文件。

## 关键强制规则

- **注册物品必须显式调用 `setId`**：NeoForge 26.1.2 起，构造 `Item.Properties` 时必须调用 `new Item.Properties().setId(ResourceKey.create(Registries.ITEM, id))`，否则游戏启动注册阶段直接抛出异常（见 [reference/registration.md](reference/registration.md)）。
- **可生成资源必须走 Datagen**：模型、语言文件、配方、战利品表、方块状态与标签必须通过 Datagen 生成到 `src/generated/resources/`，禁止手写上述 JSON 文件（见 [reference/datagen.md](reference/datagen.md)）。
- **访问私有成员优先使用 AT**：需要访问原版私有类、字段或方法时，优先在 `src/main/resources/META-INF/accesstransformer.cfg` 中配置 Access Transformer，禁止优先使用 Mixin 的 `@Accessor` 或 `@Invoker`（见 [reference/mixin-at.md](reference/mixin-at.md)）。
- **使用 Mixin 必须声明配置**：引入 Mixin 时必须在 `neoforge.mods.toml` 中声明 `[[mixins]] config = "${mod_id}.mixins.json"`，否则运行期不会加载 Mixin。
- **新增游戏内容必须补齐配套资源**：新增物品或方块时，必须同步检查并补齐模型、纹理 PNG、语言本地化条目及 `neoforge.mods.toml` 声明。
- **外部参考源码禁止入库**：解压到项目 `reference/` 目录供查阅的依赖源码或反编译产物，必须加入 `.gitignore`（见 [reference/source-reading.md](reference/source-reading.md)）。

## Checklist

- [ ] 需求存在歧义时是否已先向用户确认，且未引入当前需求不需要的抽象层？
- [ ] 所用 API、类名（如 `Identifier`）与版本号是否已核对文档或依赖源码？
- [ ] 目标版本是否为 NeoForge 26.1.2 / Minecraft 26.1.2（或用户明确指定的版本）？
- [ ] 注册物品时是否已通过 `Item.Properties().setId(...)` 显式传入 `ResourceKey`？
- [ ] 模型、语言、配方、战利品表、方块状态与标签是否全部通过 Datagen 生成，未手写 JSON？
- [ ] 访问私有成员是否优先使用了 Access Transformer，且使用 Mixin 时已在 `neoforge.mods.toml` 中声明？
- [ ] 新增物品或方块是否已配齐纹理路径、模型、语言条目与 `neoforge.mods.toml` 配置？
- [ ] 新增代码是否按职责分包（`init/`、`data/`、`network/`、`client/`），显式导入所需类型（无内联全限定名）并添加了中文注释？
- [ ] 解压到项目 `reference/` 目录的依赖源码或反编译文件是否已加入 `.gitignore`，且 `git diff` 仅包含当前请求直接涉及的改动？
