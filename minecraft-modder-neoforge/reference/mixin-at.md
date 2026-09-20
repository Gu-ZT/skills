# Mixin 与 Access Transformer

## Mixin

- 仅在必要时使用 Mixin，使用时必须说明理由并提供示例。
- **必须在 `neoforge.mods.toml` 中声明 `.mixins.json` 配置文件**，否则 Mixin 不会被 FML 加载：

```toml
[[mixins]]
config = "${mod_id}.mixins.json"
```

- 文档（Fabric 社区维护，适用于所有加载器）：
  - 入门：https://wiki.fabricmc.net/zh_cn:tutorial:mixin_introduction
  - 示例：https://wiki.fabricmc.net/zh_cn:tutorial:mixin_examples

  链接快照（2026-09-20 抓取，以链接为准；过期时重新抓取更新）：
  - Mixin 只能用 Java 编写（即使主项目用 Kotlin）；MixinExtras 由加载器捆绑，无需额外依赖即可使用 `@Local` 等注解。
  - 示例页注入模式索引：`@Inject`（`HEAD` / `TAIL` / `RETURN` / `INVOKE` ± `shift`、`slice` 限定范围、`cancellable` + `ci.cancel()` / `cir.setReturnValue()`）；局部变量捕获（`LocalCapture.CAPTURE_FAILHARD` 或 MixinExtras `@Local(ordinal = n)`）；`@Redirect`（方法调用 / `GETFIELD` / `PUTFIELD`）；`@ModifyArg` / `@ModifyArgs` / `@ModifyVariable` / `@ModifyConstant`；内部类目标用 `targets = "...$Inner"`；访问目标类成员用 `@Shadow` 而非强转 `this`。

## Access Transformer（AT）

访问 Minecraft 私有字段、方法或类时，**优先使用 AT 而非 Mixin 的 `@Accessor` / `@Invoker`**。AT 是 NeoForge 推荐机制，更轻量、性能更好、兼容性更强。

默认路径 `src/main/resources/META-INF/accesstransformer.cfg`，使用默认路径无需额外配置。语法示例：

```
# 公开类
public net.minecraft.server.MinecraftServer
# 公开字段（可附加 -f 移除 final）
public-f net.minecraft.server.MinecraftServer random
# 公开方法（需注明参数和返回值类型描述符）
public net.minecraft.Util makeExecutor(Ljava/lang/String;)Lnet/minecraft/TracingExecutor;
```
