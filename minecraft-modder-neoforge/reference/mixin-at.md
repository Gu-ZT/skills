# Mixin 与 Access Transformer（AT）

## Access Transformer（优先使用）

需要读取或调用 Minecraft 原版私有类、字段、方法或移除 `final` 修饰符时，**必须优先使用 Access Transformer（AT），禁止优先使用 Mixin 的 `@Accessor` 或 `@Invoker`**。

AT 默认配置文件路径为 `src/main/resources/META-INF/accesstransformer.cfg`（使用该默认路径无需在构建脚本中额外声明）。语法示例：

```text
# 将类改为 public
public net.minecraft.server.MinecraftServer

# 将字段改为 public，并附加 -f 移除 final 修饰符
public-f net.minecraft.server.MinecraftServer random

# 将方法改为 public（需写明完整的字节码参数与返回值描述符）
public net.minecraft.Util makeExecutor(Ljava/lang/String;)Lnet/minecraft/TracingExecutor;
```

## Mixin 配置与使用规范

- 仅当 NeoForge 事件总线与 AT 均无法满足需求（如需要修改原版方法内部执行流）时才使用 Mixin，并在代码注释中写明注入原因。
- **使用 Mixin 时必须在 `neoforge.mods.toml` 中声明配置文件**，否则运行期 FML 不会加载 Mixin：

```toml
[[mixins]]
config = "${mod_id}.mixins.json"
```

- 注入注解（`@Inject`、`@Redirect`、`@ModifyArg`、`@ModifyArgs`、`@ModifyVariable`、`@ModifyConstant`）、局部变量捕获与 Slice 用法优先查阅本地镜像（Fabric 社区维护的 Mixin 教程适用于包括 NeoForge 在内的所有加载器，本地镜像遵循 CC BY-NC-SA 4.0）：
  - 基础概念：[mixin-introduction-zh.md](external/mixin-introduction-zh.md)（原链：https://wiki.fabricmc.net/zh_cn:tutorial:mixin_introduction ）
  - 注入示例：[mixin-examples-zh.md](external/mixin-examples-zh.md)（原链：https://wiki.fabricmc.net/zh_cn:tutorial:mixin_examples ）
  - SpongePowered 官方 Wiki：[mixin-wiki-home.md](external/mixin-wiki-home.md)（原链：https://github.com/SpongePowered/Mixin/wiki ）
