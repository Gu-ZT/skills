# 常见开发任务与验收标准

## 1. 创建新模组

- **执行内容**：按 [project-setup.md](project-setup.md) 克隆模板仓库并核对版本、询问是否引入 AnvilLib、确认代码与美术资源许可证、初始化 Git 仓库并编写 `README.md`。
- **验收标准**：`./gradlew build` 构建通过；运行 `./gradlew runClient` 后在游戏模组列表中可见该模组。

## 2. 添加物品或方块

- **执行内容**：在 `init/` 包下完成 `DeferredRegister` 注册（物品必须调用 `Item.Properties().setId(...)`，见 [registration.md](registration.md)），通过 Datagen 生成模型与语言条目，并将 PNG 纹理放入 `textures/item/` 或 `textures/block/`。
- **验收标准**：`./gradlew runData` 成功生成 JSON；游戏内创造模式物品栏或指令可获取该物品/方块，纹理渲染与显示名称正常，无紫黑丢失材质或原始本地化键名。

## 3. 添加合成配方

- **执行内容**：在 `data/` 包下继承 `RecipeProvider` 生成配方，输出至 `src/generated/resources/data/<modid>/recipe/`。原版有序与无序合成类型固定为 `minecraft:crafting_shaped` 与 `minecraft:crafting_shapeless`，禁止误写为 `minecraft:recipe_shaped`。
- **验收标准**：`./gradlew runData` 在 `recipe/` 目录生成对应 JSON；游戏内工作台可按配方正常合成。

## 4. 添加自定义实体

- **执行内容**：编写实体类、属性注册、客户端渲染器（`EntityRenderer`）、模型类及生成规则。
- **验收标准**：游戏内可通过指令或刷怪蛋生成该实体，模型动画、碰撞箱与纹理渲染正常。

## 5. 添加配置文件

- **执行内容**：使用 NeoForge 的 `ModConfigSpec`（或用户选定的 AnvilLib `@Config`）定义配置项并注册到模组容器。
- **验收标准**：启动游戏后在 `run/config/` 下自动生成配置文件；修改配置值后游戏内对应逻辑随之生效。

## 6. 排查与修复崩溃

- **执行内容**：读取崩溃日志（`crash-reports/` 或 `latest.log`）堆栈信息，定位未设置物品 `id`、注册时机错误、客户端类在服务端加载或 Mixin 注入目标签名不匹配等根因，并修改对应代码。
- **验收标准**：说明崩溃触发原因与修复点，重新运行对应端确认崩溃不再复现。

## 7. 编写自动化测试

- **执行内容**：按 [testing.md](testing.md) 配置 JUnit 5 或 `testframework`（`@ExtendWith(EphemeralTestServerProvider.class)`），为关键业务逻辑编写测试。
- **验收标准**：`./gradlew test` 或 `./gradlew runGameTestServer` 全部通过。
