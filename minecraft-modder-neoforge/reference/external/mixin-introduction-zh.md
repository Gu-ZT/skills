# Mixin 介绍（Fabric Wiki 中文）

> - 来源：https://wiki.fabricmc.net/zh_cn:tutorial:mixin_introduction
> - 抓取日期：2026-09-20（内容更新后重新抓取本文件）
> - 许可：CC BY-NC-SA 4.0（署名-非商业性使用-相同方式共享；转载本文件必须保留此署名）
> - 署名：Fabric Wiki 贡献者（页面最后修订：2023-12-18，solidblock）

## 正文

Mixin 是 Fabric 生态系统中强大重要的工具，其主要用途是修改基本游戏中已存在的代码，可以是通过注入自定义的逻辑、移除机制或者修改值。**注意 Mixin 只能使用 Java 语言编写，即便你的项目使用 Kotlin 或者其他语言。**

自从 Fabric Loader 0.15 以来，Fabric Loader 捆绑了 MixinExtras，因此你可以直接使用 MixinExtras 来更好地操纵 Mixin。

Mixin 的完整功能、用途和机制，请参考 [Mixin 的官方 Wiki](https://github.com/SpongePowered/Mixin/wiki)。此外可以在 [Mixin Javadoc](https://jenkins.liteloader.com/view/Other/job/Mixin/javadoc/index.html) 找到附加的文档。

## Fabric Wiki 相关页面

- [Mixin 注册](https://wiki.fabricmc.net/zh_cn:tutorial:mixin_registration)
- [注入](https://wiki.fabricmc.net/zh_cn:tutorial:mixin_injects)
- [访问器和调用器](https://wiki.fabricmc.net/zh_cn:tutorial:mixin_accessors)
- [重定向器](https://wiki.fabricmc.net/zh_cn:tutorial:mixin_redirectors)（含[方法重定向器](https://wiki.fabricmc.net/zh_cn:tutorial:mixin_redirectors_methods)）
- [小提示](https://wiki.fabricmc.net/zh_cn:tutorial:mixin_tips)
- [示例](https://wiki.fabricmc.net/zh_cn:tutorial:mixin_examples)（本仓库完整镜像：[mixin-examples-zh.md](mixin-examples-zh.md)）
- [Mixin 热交换](https://wiki.fabricmc.net/zh_cn:tutorial:mixin_hotswaps)
- [导出 Mixin 类](https://wiki.fabricmc.net/zh_cn:tutorial:mixin_export)
- [访问加宽器](https://wiki.fabricmc.net/zh_cn:tutorial:accesswideners)
- [反射](https://wiki.fabricmc.net/zh_cn:tutorial:reflection)
- [接口注入](https://wiki.fabricmc.net/zh_cn:tutorial:interface_injection)
