# 数据生成（Datagen）

## 核心原则

凡是可通过 Datagen 自动生成的 JSON 资源，必须使用 Datagen 生成并输出到 `src/generated/resources/`，**禁止手写或手动修改生成的 JSON 文件**。仅 PNG 纹理等二进制文件手动放置在 `src/main/resources/assets/<modid>/textures/` 下。

Minecraft 跨版本升级时，`DataGenerator`、`PackOutput` 及各 `Provider` 的签名可能发生变动；遇到 API 变更时必须查阅官方文档或依赖源码适配新签名，禁止因 API 变动而回退到手写 JSON。

## 资源类型与 Provider 对应表

| 资源类型 | Provider 类 | 生成路径（相对于 `src/generated/resources/`） |
| --- | --- | --- |
| 语言文件 | `LanguageProvider` | `assets/<modid>/lang/en_us.json` |
| 物品与方块模型 | `ModelProvider` | `assets/<modid>/models/` |
| 配方 | `RecipeProvider` | `data/<modid>/recipe/` |
| 战利品表 | `LootTableProvider` | `data/<modid>/loot_table/` |
| 方块状态 | `BlockStateProvider` | `assets/<modid>/blockstates/` |
| 标签 | `TagProvider` | `data/<modid>/tags/` |

## 入口类示例（`data/` 包）

```java
@EventBusSubscriber(modid = ExampleMod.MOD_ID)
public class ExampleModData {
    @SubscribeEvent
    public static void gatherData(GatherDataEvent.Client event) {
        DataGenerator generator = event.getGenerator();
        PackOutput packOutput = generator.getPackOutput();
        generator.addProvider(true, new ExampleModLanguageProvider(packOutput));
    }
}
```

## LanguageProvider 示例

```java
public class ExampleModLanguageProvider extends LanguageProvider {
    public ExampleModLanguageProvider(PackOutput output) {
        super(output, ExampleMod.MOD_ID, "en_us");
    }

    @Override
    protected void addTranslations() {
        this.add("item.examplemod.example_item", "Example Item");
        this.add("block.examplemod.example_block", "Example Block");
        this.add("itemGroup.examplemod.default", "Example Mod");
    }
}
```

## 生成与验证

执行 `./gradlew runData`，确认 `src/generated/resources/` 下已生成对应的 JSON 文件，再启动客户端验证游戏内模型、名称与配方正常生效。
