# 注册系统（DeferredRegister）

## 核心规则

- 所有注册项统一使用 `DeferredRegister` 并在 `init/` 包下集中管理。
- **NeoForge 26.1.2 起，注册物品时必须调用 `Item.Properties().setId(...)` 显式绑定 `ResourceKey`**，未设置 `id` 会导致游戏启动时抛出注册异常。
- `DeferredRegister` 仅提供四个专用子类：`Blocks`、`DataComponents`、`Entities`、`Items`；注册附魔、创造模式物品栏、菜单类型等其他注册表项时，直接使用通用泛型 `DeferredRegister.create(Registries.XXX, MOD_ID)`。
- Minecraft 1.21.11 起原 `ResourceLocation` 已重命名为 `Identifier`，编写资源定位代码时必须使用 `Identifier`。

## 物品注册示例

```java
public static final DeferredRegister.Items ITEMS =
    DeferredRegister.createItems(ExampleMod.MOD_ID);

public static final DeferredItem<Item> EXAMPLE_ITEM =
    ITEMS.register(
        "example_item",
        id -> new Item(new Item.Properties().setId(ResourceKey.create(Registries.ITEM, id)))
    );
```

## 配套资源检查

完成物品或方块代码注册后，必须同步补齐模型、纹理、语言文件与 `neoforge.mods.toml` 配置，具体要求见 [project-setup.md](project-setup.md)。
