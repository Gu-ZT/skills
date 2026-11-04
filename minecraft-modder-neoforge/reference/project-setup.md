# 项目结构与构建配置

## 标准目录结构（ModDevGradle + 版本目录）

```text
project_root/
├── build.gradle
├── gradle.properties
├── settings.gradle
├── gradle/
│   ├── libs.versions.toml          # 统一管理依赖版本
│   └── wrapper/
└── src/
    ├── generated/resources/        # Datagen 输出目录（禁止手动编辑）
    │   ├── data/<modid>/
    │   │   └── recipe/             # Datagen 生成的配方
    │   └── assets/<modid>/
    │       ├── lang/               # Datagen 生成的语言文件
    │       └── models/             # Datagen 生成的模型文件
    ├── main/
    │   ├── java/com/example/examplemod/
    │   │   ├── ExampleMod.java
    │   │   ├── client/             # 客户端专属逻辑
    │   │   ├── data/               # Datagen Provider 实现
    │   │   ├── init/               # 注册项（物品、方块、创造模式物品栏等）
    │   │   ├── mixin/              # Mixin 类
    │   │   ├── network/            # 网络数据包
    │   │   └── util/               # 通用工具类
    │   ├── resources/
    │   │   ├── META-INF/
    │   │   │   └── accesstransformer.cfg  # 访问原版私有成员时配置
    │   │   ├── <modid>.mixins.json
    │   │   └── assets/<modid>/
    │   │       └── textures/       # 手动放置的 PNG 纹理
    │   └── templates/
    │       └── META-INF/
    │           └── neoforge.mods.toml
```

## 初始化新模组流程

1. 使用模板仓库初始化项目骨架（默认对应 NeoForge 26.1.2 与 Minecraft 26.1.2；若本机未安装 Git，先搜索当前操作系统的 Git 安装说明并引导安装）：

   ```bash
   git clone https://github.com/Gu-ZT/neoforge-template-mod.git
   ```

   注：该仓库在 2026-09-20 抓取时 `main`/`master` 分支 `README.md` 均返回 404，仓库内容未经验证。克隆后必须先读取仓库内的 `README.md` 与 `gradle.properties` 核对实际分支、版本号与目录结构，禁止直接假设默认值；若该仓库不可访问，通过搜索引擎查找当前可用的 NeoForge 26.1 模板仓库。
2. 询问用户是否引入 AnvilLib 及其具体子模块（见 [anvillib.md](anvillib.md)）。
3. 确认许可证：除用户另有指定外，源码默认使用 `LGPL-3.0`，纹理与模型等美术资源默认使用 `ARR`（All Rights Reserved）。
4. 初始化 Git 仓库并编写包含模组简介、构建命令与运行说明的 `README.md`。
5. 执行 `./gradlew build` 验证构建通过，并启动客户端确认模组列表能正常识别该模组。

## 常用 Gradle 命令

| 命令 | 说明 |
| --- | --- |
| `./gradlew build` | 编译并打包模组 JAR |
| `./gradlew runClient` | 启动开发客户端 |
| `./gradlew runServer` | 启动开发服务端 |
| `./gradlew runData` | 运行 Datagen 生成资源文件 |
| `./gradlew test` | 运行 JUnit 单元测试 |
| `./gradlew runGameTestServer` | 启动 GameTest 测试服务端 |

## 新增物品与方块的配套资源要求

每次新增物品或方块时，必须同时配齐以下四项：

- **模型文件**：通过 Datagen 的 `ModelProvider` 生成（见 [datagen.md](datagen.md)）。
- **纹理文件**：将 PNG 纹理放入 `src/main/resources/assets/<modid>/textures/item/` 或 `textures/block/`。
- **语言文件**：通过 Datagen 的 `LanguageProvider` 生成本地化译名。
- **`neoforge.mods.toml`**：按需更新模组元数据或依赖声明。

## 辅助工具配置

### IntelliJ IDEA MCP 服务

在 IntelliJ IDEA 中启用内置 MCP 服务后，可直接调用 IDE 的文件读写、重构、测试运行与编译诊断能力：

1. 打开 `文件` -> `设置` -> `工具` -> `MCP 服务器`。
2. 勾选启用 MCP 服务器（插件默认内置，可在 `设置` -> `插件` -> `已安装` 中确认）。
3. 在「客户端自动配置」中选择当前 AI 客户端并点击「自动配置」，重启客户端生效。如需免确认执行命令，可在 `MCP 服务器` -> `命令执行` 中开启 Brave 模式。

### 网页抓取备用工具（`mcp-webscraper`）

当运行环境缺少内置网页抓取工具且需要查阅在线文档时，可运行 `npx mcp-webscraper` 或在 `.mcp.json` 中配置 MCP 服务：

```json
{
  "mcpServers": {
    "webscraper": {
      "command": "npx",
      "args": ["-y", "mcp-webscraper"]
    }
  }
}
```

抓取依赖前端渲染的文档站（如 VitePress）时，需额外执行 `npx playwright install chromium` 安装浏览器内核。
