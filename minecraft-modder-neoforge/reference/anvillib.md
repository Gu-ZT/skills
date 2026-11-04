# AnvilLib 辅助库集成参考

[AnvilLib](https://lib.anvilcraft.dev/) 是面向 NeoForge 的模块化辅助开发库。初始化新模组时询问用户是否引入及需要哪些子模块。

本地参考镜像（2026-09-20 抓取，以原链接为准，过期时重新抓取更新）：
- 官网首页与模块说明：[external/anvillib-home.md](external/anvillib-home.md)（CC-BY-NC-SA 4.0；各模块详细文档路径为 `https://lib.anvilcraft.dev/posts/docs/<模块名>/`）
- Maven Central 产物与版本线清单：[external/anvillib-maven-central.md](external/anvillib-maven-central.md)（注：`cube`、`explosion`、`rpc`、`sync-processor` 四个模块已发布到 Maven 但未在官网首页列出，引入前需查阅对应模块文档；`yukkuri` 仅提供 1.21.1 版本）

## 常用模块一览

| 模块名 | 功能说明 |
| --- | --- |
| `codec` | 数据编解码与网络序列化工具（`CodecUtil`、`StreamCodecUtil`） |
| `collision` | AABB 与三角形 SAT 碰撞检测 |
| `config` | 注解驱动配置系统（`@Config`、`@Comment`），自动生成客户端配置界面 |
| `font` | 基于有向距离场（SDF）的字体渲染 |
| `integration` | 跨模组兼容集成框架（`@Integration` 注解），支持按版本范围匹配 |
| `math` | 可序列化的数学表达式解析与计算 |
| `moveable-entity-block` | 支持活塞推动并保留 NBT 数据的方块实体（`IMoveableEntityBlock`） |
| `multiblock` | 动态多方块结构定义、控制器与运行时管理 |
| `network` | 网络数据包自动注册与通信，支持 `PLAY` / `CONFIGURATION` / `COMMON` 阶段 |
| `recipe` | 世界内自定义配方系统（`Trigger` / `Predicate` / `Outcome`）与数据包支持 |
| `registrum` | 基于 Registrate 的链式注册 API，支持自动生成模型与语言条目 |
| `rendering` | 泛光后处理、缓存 `BlockEntity` 渲染、SDF 图形与 UBO 渲染工具 |
| `space-select` | 可视化空间选区工具 |
| `sync` | 声明式字段同步 |
| `util` | 集合、物品栏、数学、碰撞箱与滚动 UI 等通用工具方法 |
| `wheel` | 客户端轮盘菜单 API |
| `anvillib`（Main） | 包含上述全部子模块的聚合包（坐标 `dev.anvilcraft.lib:anvillib-neoforge-26.1`） |

## Gradle 版本目录配置（`gradle/libs.versions.toml`）

```toml
[versions]
# 26.1 分支目前仅发布 2.0.0+snapshot.NNN 快照版本；引入前必须先查询 Maven 仓库确认最新可用版本，禁止直接照抄下方示例版本号
anvillib = "2.0.0+snapshot.531"

[libraries]
anvillib-config = { group = "dev.anvilcraft.lib", name = "anvillib-config-neoforge-26.1", version.ref = "anvillib" }
anvillib-registrum = { group = "dev.anvilcraft.lib", name = "anvillib-registrum-neoforge-26.1", version.ref = "anvillib" }
```

## 版本查询地址

引入依赖前必须从以下仓库查询当前 Minecraft 版本对应的最新可用版本号：
- Maven Central：https://repo1.maven.org/maven2/dev/anvilcraft/lib/
- 备用 Maven 镜像：https://server.cjsah.net:1002/maven/dev/anvilcraft/lib/
