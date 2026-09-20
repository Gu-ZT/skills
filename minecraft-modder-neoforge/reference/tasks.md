# 常见任务与完成标准

## 1. 创建新模组

- 按 [project-setup.md](project-setup.md) 执行：模板仓库生成骨架、确认 AnvilLib 模块、确定许可证、初始化 Git 与 README。
- ✅ 验证：`./gradlew build` 通过；运行客户端后模组列表可见该 mod。

## 2. 添加物品/方块

- 注册（[registration.md](registration.md)）、模型、纹理、本地化一次性给出；模型和语言文件走 datagen，纹理手动放置。
- ✅ 验证：物品/方块在游戏中可见、纹理正确、创造模式物品栏可找到、lang 文件有对应名称。

## 3. 添加合成表

- 通过 RecipeProvider 在 datagen 中生成，输出到 `data/<modid>/recipe/`。
- 原版工作台合成类型用 `minecraft:crafting_shaped` / `crafting_shapeless`，禁止写成 `minecraft:recipe_shaped`。
- ✅ 验证：`./gradlew runData` 后 `src/generated/resources/data/<modid>/recipe/` 下出现 JSON；游戏内可正常合成。

## 4. 自定义实体

- 提供实体类、渲染器、模型、生成逻辑。
- ✅ 验证：实体能在游戏中生成/召唤，模型和纹理渲染正确。

## 5. 配置文件

- 使用 `ModConfigSpec`。
- ✅ 验证：配置文件在 `config/` 目录生成；修改配置后游戏内行为相应改变。

## 6. 调试崩溃

- 分析日志，定位注册问题或 Mixin 冲突，给出修复建议。
- ✅ 验证：复现步骤 → 定位根因 → 给出修改方案 → 确认修复后崩溃不再出现。

## 7. 编写测试

- 为关键逻辑编写 JUnit 单元测试或 GameTest，配置见 [testing.md](testing.md)。
- ✅ 验证：`./gradlew test` 全部通过；需服务端环境时引入 `testframework` 并使用 `@ExtendWith(EphemeralTestServerProvider.class)`。
