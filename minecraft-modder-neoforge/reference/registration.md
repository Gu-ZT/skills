# 注册（DeferredRegister）

## 基本规则

- 使用 `DeferredRegister` 系统，注册项集中在 `init/` 包下。
- **NeoForge 26.1.2 起，注册物品必须通过 `Item.Properties().setId(...)` 显式设置 id**，否则运行时报错。
- `DeferredRegister` 只有四个内置子类：`Blocks`、`DataComponents`、`Entities`、`Items`。其他注册类型（附魔、创造模式物品栏等）直接使用 `DeferredRegister<T>` 泛型。

## 物品注册示例

```java
public static final DeferredRegister.Items ITEMS =
    DeferredRegister.createItems(YourMod.MOD_ID);

public static final DeferredItem<Item> EXAMPLE_ITEM =
    ITEMS.register("example_item", id -> new Item(new Item.Properties().setId(ResourceKey.create(Registries.ITEM, id))));
```

## 配套资源

注册物品/方块后必须同步处理配套资源（模型、纹理、语言文件、`neoforge.mods.toml` 声明），要求见 [project-setup.md](project-setup.md) 资源文件要求一节。
