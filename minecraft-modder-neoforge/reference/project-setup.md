# 项目结构与构建

## 项目结构（MDG + 版本目录）

```
project_root/
├── build.gradle
├── gradle.properties
├── settings.gradle
├── gradle/
│   ├── libs.versions.toml          # 版本目录（统一管理依赖版本）
│   └── wrapper/
└── src/
    ├── generated/resources/        # datagen 输出（禁止手动编辑）
    │   ├── data/<modid>/
    │   │   └── recipe/             # 配方文件由 datagen 生成
    │   └── assets/<modid>/
    │       ├── lang/               # 语言文件由 datagen 生成
    │       └── models/             # 模型文件由 datagen 生成
    ├── main/
    │   ├── java/<your/package>/
    │   │   ├── <YourModMainClass>.java
    │   │   ├── client/             # 客户端逻辑
    │   │   ├── data/               # datagen（语言、模型、配方、战利品表）
    │   │   ├── init/               # 注册项（物品、方块、创造模式物品栏等）
    │   │   ├── mixin/
    │   │   ├── network/            # 网络包（如需要）
    │   │   └── util/               # 工具类（如需要）
    │   ├── resources/
    │   │   ├── META-INF/
    │   │   │   └── accesstransformer.cfg  # 可选，仅访问私有成员时
    │   │   ├── <modid>.mixins.json
    │   │   └── assets/<modid>/
    │   │       └── textures/       # 仅手动管理的纹理
    │   └── templates/              # 模板文件（构建时处理）
    │       └── META-INF/
    │           └── neoforge.mods.toml
```

## 创建新模组

1. 优先使用模板仓库生成骨架（默认 NeoForge 26.1.2 + MC 26.1.2）：

   ```bash
   git clone https://github.com/Gu-ZT/neoforge-template-mod.git
   ```

2. 初始化时询问用户是否引入 AnvilLib 及需要哪些模块（见 [anvillib.md](anvillib.md)）。
3. 许可证约定：代码默认 **LGPL-3.0**，资源文件（纹理、模型等）默认 **ARR（All Rights Reserved）**；用户有特殊要求时按用户要求。
4. 同步初始化 Git 仓库并创建 `README.md`（含 mod 简介、构建和运行说明）。
5. 验证：`./gradlew build` 通过；运行客户端后模组列表可见该 mod。

## 构建与运行命令

| 命令 | 用途 |
| --- | --- |
| `./gradlew build` | 构建 |
| `./gradlew runClient` | 运行客户端 |
| `./gradlew runServer` | 运行服务器 |
| `./gradlew runData` | 运行数据生成 |
| `./gradlew test` | 运行单元测试 |
| `./gradlew runGameTestServer` | 运行 GameTest |

## 资源文件要求

生成物品或方块时必须同时提供：

- **模型文件** — 优先 datagen ModelProvider 生成（见 [datagen.md](datagen.md)）
- **纹理文件** — 手动放置 PNG 到 `textures/item/`、`textures/block/`
- **语言文件** — 优先 datagen LanguageProvider 生成
- **`neoforge.mods.toml`** — 提醒用户同步包含新内容的相关声明

## 工具链配置

### Git

创建模组项目需要 Git（克隆模板仓库）。未安装时先搜索当前操作系统下 Git 最新安装指南，引导用户安装。

### IntelliJ IDEA MCP 服务器

使用 IntelliJ IDEA 时，可通过内置 MCP 服务器让 AI 直接操作 IDE（读写文件、执行重构、运行测试、获取编译错误）：

1. `文件` → `设置` → `工具` → `MCP 服务器`
2. 确认 MCP 服务器插件已启用（默认捆绑，设置 → 插件 → 已安装）
3. 点击「启用 MCP 服务器」
4. 在「客户端自动配置」区域选择对应客户端，点击「自动配置」
5. 重启客户端生效

可选启用 **Brave 模式**（无需确认即可运行命令），位于 MCP 服务器设置 → 命令执行。

### WebScraper（网页抓取兜底）

当前客户端无网页抓取能力时，引导用户安装 `mcp-webscraper`：

```bash
npx mcp-webscraper
```

客户端 MCP 配置（如 `.mcp.json`）：

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

静态页面无需额外依赖。渲染 JS 页面（如 Vitepress 文档站）需安装 Playwright：

```bash
npx playwright install chromium
```
