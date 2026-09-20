# 数据生成（Datagen-First）

## 原则

**优先使用 datagen 生成一切可自动生成的资源，禁止手写 JSON 文件。**

Minecraft 版本更新时 datagen API（`DataGenerator`、`PackOutput`、各 Provider 构造参数）可能大幅变更。无论 API 变得多复杂，都必须通过阅读官方文档和查阅源码正确使用 datagen，**禁止因 API 不熟悉回退到手写 JSON**。

仅 `textures/` 等二进制资源手动放置于 `src/main/resources/assets/<modid>/textures/`。

## 必须通过 datagen 生成的资源

输出目录 `src/generated/resources/`（禁止手动编辑）：

| 资源 | Provider | 输出路径 |
| --- | --- | --- |
| 语言文件 | `LanguageProvider` | `assets/<modid>/lang/en_us.json` |
| 物品/方块模型 | `ModelProvider` | `assets/<modid>/models/` |
| 配方 | `RecipeProvider` | `data/<modid>/recipe/` |
| 战利品表 | `LootTableProvider` | `data/<modid>/loot_table/` |
| 方块状态 | `BlockStateProvider` | `assets/<modid>/blockstates/` |
| 标签 | `TagProvider` | `data/<modid>/tags/` |

## 入口类（`data/` 包下）

```java
@EventBusSubscriber(modid = YourMod.MOD_ID)
public class YourModData {
    @SubscribeEvent
    public static void gatherData(GatherDataEvent.Client event) {
        DataGenerator generator = event.getGenerator();
        PackOutput packOutput = generator.getPackOutput();
        generator.addProvider(true, new YourModLanguageProvider(packOutput));
        // ...其他 Provider
    }
}
```

## LanguageProvider 示例

```java
public class YourModLanguageProvider extends LanguageProvider {
    public YourModLanguageProvider(PackOutput output) {
        super(output, YourMod.MOD_ID, "en_us");
    }

    @Override
    protected void addTranslations() {
        this.add("item.yourmod.example_item", "Example Item");
        this.add("block.yourmod.example_block", "Example Block");
        this.add("itemGroup.yourmod.default", "Your Mod");
    }
}
```

## 验证

运行 `./gradlew runData` 后检查 `src/generated/resources/` 下生成了预期 JSON；进游戏确认资源生效。
