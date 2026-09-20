# 推荐库：AnvilLib

[AnvilLib](https://lib.anvilcraft.dev/) 是 NeoForge 模组开发辅助库，按模块按需引入。创建项目时询问用户是否使用。使用细节以官方文档 https://lib.anvilcraft.dev/ 为准。

链接镜像（2026-09-20 抓取，以原链接为准；过期时重新抓取更新）：

- 官网首页完整镜像：[external/anvillib-home.md](external/anvillib-home.md)（CC-BY-NC-SA 4.0；各模块文档位于 `https://lib.anvilcraft.dev/posts/docs/<模块名>/`）。
- Maven Central `dev/anvilcraft/lib/` 目录完整镜像：[external/anvillib-maven-central.md](external/anvillib-maven-central.md)（各 artifact 已发布版本线；cube / explosion / rpc / sync-processor 未在官网首页列出，引入前查其文档；聚合模块 Main 坐标为 `dev.anvilcraft.lib:anvillib-neoforge-26.1`；`yukkuri` 仅 1.21.1）。

## 模块清单（官网首页列出部分；Maven 实际产物见上方链接镜像）

| 模块 | 功能 |
| --- | --- |
| **Codec** | 数据编解码与网络序列化工具（`CodecUtil`、`StreamCodecUtil`） |
| **Collision** | AABB / 三角形 SAT 碰撞检测 |
| **Config** | 基于注解的配置系统（`@Config`、`@Comment`），自动生成客户端配置 GUI |
| **Font** | 基于 SDF 的字体渲染系统 |
| **Integration** | 模组兼容性集成框架（`@Integration` 注解），支持版本范围匹配 |
| **Math** | 可序列化的数学表达式系统 |
| **Moveable Entity Block** | 可被活塞推动的方块实体支持（`IMoveableEntityBlock`），保留 NBT 数据 |
| **Multiblock** | 动态多方块系统（控制器、定义系统、运行时管理） |
| **Network** | 网络通信与数据包自动注册，支持 PLAY / CONFIGURATION / COMMON 通道 |
| **Recipe** | 世界内自定义配方系统，支持 Trigger / Predicate / Outcome 和数据包 |
| **Registrum** | 基于 Registrate 的简化注册系统，链式 API，自动生成语言文件和模型 |
| **Rendering** | 渲染工具（泛光后处理、Cached BlockEntity 渲染、SDF 图形、UBO 框架） |
| **Space Select** | 可视化空间选区系统 |
| **Sync** | 声明式字段同步系统 |
| **Util** | 可共享的工具方法（集合、物品栏、数学、碰撞箱、滚动 UI 等） |
| **Wheel** | 轮盘菜单客户端 API |
| **Main** | 聚合模块，包含全部子模块（以官网清单为准） |

## Gradle 引入（版本目录）

```toml
[versions]
anvillib = "2.0.0+snapshot.531"    # 示例版本，禁止照抄；26.1 线目前仅有 2.0.0+snapshot.NNN 快照，必须按下方地址查询后替换

[libraries]
anvillib-config = { group = "dev.anvilcraft.lib", name = "anvillib-config-neoforge-26.1", version.ref = "anvillib" }
anvillib-registrum = { group = "dev.anvilcraft.lib", name = "anvillib-registrum-neoforge-26.1", version.ref = "anvillib" }
# 其他模块按需添加
```

## 查询最新版本号

- Maven Central：https://repo1.maven.org/maven2/dev/anvilcraft/lib/
- 备用镜像：https://server.cjsah.net:1002/maven/dev/anvilcraft/lib/

版本号禁止凭记忆，引入前必须查询确认。
