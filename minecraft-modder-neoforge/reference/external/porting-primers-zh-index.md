# Porting-Primers 中文站首页（主题地图 + 类和方法索引）

> - 来源：https://gu-zt.github.io/Porting-Primers/
> - 抓取日期：2026-09-20（内容更新后重新抓取本文件）
> - 许可：CC BY 4.0（© ChampionAsh5357；中文翻译 Gu-ZT，仓库 https://github.com/Gu-ZT/Porting-Primers）
> - 说明：本文件为页面正文的完整镜像；站内相对链接已补全为绝对地址

## 站点说明

原始仓库：https://github.com/Leclowndu93150/Porting-Primers ；原始地址：https://leclowndu93150.github.io/Porting-Primers

涵盖的上游链条：`1.21.1 -> 1.21.2/3 -> 1.21.4 -> 1.21.5 -> 1.21.6 -> 1.21.7 -> 1.21.8 -> 1.21.9 -> 1.21.10 -> 1.21.11 -> 26.1`

上游没有单独的 `1.21.3` 入门文档；`1.21.2` 的入门文档涵盖 `1.21.1 -> 1.21.2/3` 这一步。

## 如何使用本网站

- **知道哪个子系统发生了变化** → 用下方主题地图，每个链接直接指向相关章节。
- **同一子系统在多个版本中都发生了变化** → 见[频繁变更的系统](https://gu-zt.github.io/Porting-Primers/repeatedly-changing-systems.html)了解阅读顺序。
- **要原始入门文档** → 见[详细入门文档](https://gu-zt.github.io/Porting-Primers/detailed-primers/README.html)，含指向每个章节锚点的完整目录。
- **遇到编译错误** → 用下方「类和方法索引」查找它在哪里发生了变化。

## 主题地图

### 构建、映射、名称、导入和包移动

- [重命名混乱](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.11-from-1.21.10.html#重命名混乱) (1.21.11)
- [ResourceLocation 到 Identifier](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.11-from-1.21.10.html#resourcelocation-到-identifier) (1.21.11)
- [util 包](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.11-from-1.21.10.html#util-包) (1.21.11)
- [critereon 到 criterion](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.11-from-1.21.10.html#critereon-到-criterion) (1.21.11)
- [实体和对象子包](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.11-from-1.21.10.html#实体和对象子包) (1.21.11)
- [Java 25 与反混淆](https://gu-zt.github.io/Porting-Primers/detailed-primers/26.1-from-1.21.11.html#java-25-与反混淆) (26.1)
- [JSpecify 注解](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.11-from-1.21.10.html#jspecify-注解) (1.21.11)
- [使用注解](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.11-from-1.21.10.html#使用注解) (1.21.11)

### 数据生成、资源包、注册表、标签、编解码器、战利品、验证和配方序列化

- [持有者集过渡](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.2-from-1.21.1.html#持有者集-过渡) (1.21.2)
- [原料的转变](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.2-from-1.21.1.html#原料的转变) (1.21.2)
- [配方，现在采用注册表格式](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.2-from-1.21.1.html#配方现在采用注册表格式) (1.21.2)
- [配方提供者，数据提供者的“并非真正”](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.2-from-1.21.1.html#配方提供者数据提供者的并非真正) (1.21.2)
- [乐器，数据包版](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.2-from-1.21.1.html#乐器-数据包版) (1.21.2)
- [试炼刷怪笼配置，现在采用数据包形式](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.2-from-1.21.1.html#试炼刷怪笼配置现在采用数据包形式) (1.21.2)
- [条件，通过 HolderGetter 提供](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.2-from-1.21.1.html#条件通过-holdergetter-提供) (1.21.2 次要)
- [可编解码的 JSON 重载监听器](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.2-from-1.21.1.html#可编解码的-json-重载监听器) (1.21.2 次要)
- [上下文键](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.2-from-1.21.1.html#上下文键) (1.21.2 次要)
- [SimpleJsonResourceReloadListener](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.4-from-1.21.2-3.html#simplejsonresourcereloadlistener) (1.21.4 次要)
- [MetadataSectionSerializer，被 Codec 取代](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.4-from-1.21.2-3.html#metadatasectionserializer被-codec-取代) (1.21.4 次要)
- [标签与解析](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.5-from-1.21.4.html#标签与解析) (1.21.5)
- [模型重做](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.5-from-1.21.4.html#模型重做) (1.21.5)
- [注册表上下文交换器](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.5-from-1.21.4.html#注册表上下文交换器) (1.21.5 次要)
- [定时器回调，加入编解码器俱乐部！](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.5-from-1.21.4.html#定时器回调加入编解码器俱乐部) (1.21.5 次要)
- [TagAppender 重写](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.6-from-1.21.5.html#TagAppender-重写) (1.21.6)
- [通用编码与解码：替换直接 NBT 访问](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.6-from-1.21.5.html#通用编码与解码替换直接-nbt-访问) (1.21.6)
- [战利品类型展开](https://gu-zt.github.io/Porting-Primers/detailed-primers/26.1-from-1.21.11.html#战利品类型展开) (26.1)
- [验证大修](https://gu-zt.github.io/Porting-Primers/detailed-primers/26.1-from-1.21.11.html#验证大修) (26.1)
- [数据包村民交易](https://gu-zt.github.io/Porting-Primers/detailed-primers/26.1-from-1.21.11.html#数据包村民交易) (26.1)
- [序列化器记录与配方信息](https://gu-zt.github.io/Porting-Primers/detailed-primers/26.1-from-1.21.11.html#序列化器记录与配方信息) (26.1)
- [新标签提供者](https://gu-zt.github.io/Porting-Primers/detailed-primers/26.1-from-1.21.11.html#新标签提供者) (26.1 次要)
- [可种植标签](https://gu-zt.github.io/Porting-Primers/detailed-primers/26.1-from-1.21.11.html#可种植标签) (26.1 次要)

### 物品、组件、装备、盔甲、工具、战斗、染料和消耗品

- [装备与物品、模型等等](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.2-from-1.21.1.html#装备与物品模型等等) (1.21.2)
- [盔甲材料、装备和模型（纹理）](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.2-from-1.21.1.html#盔甲材料装备和模型纹理) (1.21.2)
- [消耗品](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.2-from-1.21.1.html#消耗品) (1.21.2)
- [交互结果](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.2-from-1.21.1.html#交互结果) (1.21.2)
- [BlockEntityTypes 私有化了！](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.2-from-1.21.1.html#blockentitytypes-私有化了) (1.21.2)
- [注册表对象 ID，在属性里？](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.2-from-1.21.1.html#注册表对象-id在属性里) (1.21.2)
- [属性变更](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.2-from-1.21.1.html#属性变更) (1.21.2)
- [燃料值](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.2-from-1.21.1.html#燃料值) (1.21.2 次要)
- [生物替换当前物品](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.4-from-1.21.2-3.html#生物-替换当前物品) (1.21.4)
- [武器、工具和盔甲：去除冗余](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.5-from-1.21.4.html#武器工具和盔甲去除冗余) (1.21.5)
- [数据组件获取器](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.5-from-1.21.4.html#数据组件获取器) (1.21.5)
- [组件交互事件](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.5-from-1.21.4.html#组件交互事件) (1.21.5 次要)
- [物品拥有者](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.9-from-1.21.8.html#物品拥有者) (1.21.9 次要)
- [容器使用者](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.9-from-1.21.8.html#容器使用者) (1.21.9 次要)
- [槽位来源](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.11-from-1.21.10.html#槽位来源) (1.21.11 次要)
- [新数据组件](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.11-from-1.21.10.html#新数据组件) (1.21.11)
- [数据组件初始化器](https://gu-zt.github.io/Porting-Primers/detailed-primers/26.1-from-1.21.11.html#数据组件初始化器) (26.1)
- [物品实例与堆栈模板](https://gu-zt.github.io/Porting-Primers/detailed-primers/26.1-from-1.21.11.html#物品实例与堆栈模板) (26.1)
- [染料组件](https://gu-zt.github.io/Porting-Primers/detailed-primers/26.1-from-1.21.11.html#染料组件) (26.1)
- [数据组件新增](https://gu-zt.github.io/Porting-Primers/detailed-primers/26.1-from-1.21.11.html#数据组件新增) (26.1 次要)

### 渲染、模型、着色器、粒子、方块模型、物品模型、材质、纹理图集和视觉管线

- [GUI 渲染类型](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.2-from-1.21.1.html#gui-渲染类型) (1.21.2)
- [着色器重写](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.2-from-1.21.1.html#着色器重写) (1.21.2)
- [实体渲染状态](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.2-from-1.21.1.html#实体渲染状态) (1.21.2)
- [雾参数](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.2-from-1.21.1.html#雾参数) (1.21.2 次要)
- [发光强度](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.2-from-1.21.1.html#发光强度) (1.21.2 次要)
- [地图纹理](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.2-from-1.21.1.html#地图纹理) (1.21.2 次要)
- [客户端物品](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.4-from-1.21.2-3.html#客户端物品) (1.21.4)
- [粒子，通过渲染类型渲染](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.4-from-1.21.2-3.html#粒子通过渲染类型渲染) (1.21.4)
- [渲染管线重做](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.5-from-1.21.4.html#渲染管线重做) (1.21.5)
- [模型重做](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.5-from-1.21.4.html#模型重做) (1.21.5)
- [纹理图集重做](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.5-from-1.21.4.html#纹理图集重做) (1.21.5 次要)
- [GUI 变更](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.6-from-1.21.5.html#gui-变更) (1.21.6)
- [Blaze3d 变更](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.6-from-1.21.5.html#blaze3d-变更) (1.21.6)
- [移除生物效果图集](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.6-from-1.21.5.html#移除生物效果图集) (1.21.6 次要)
- [动画烘焙](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.6-from-1.21.5.html#动画烘焙) (1.21.6 次要)
- [ChunkSectionLayers](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.6-from-1.21.5.html#chunksectionlayers) (1.21.6 次要)
- [小幅迁移](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.7-from-1.21.6.html#小幅迁移) (1.21.7 —— GUI 渲染后续)
- [小幅迁移](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.8-from-1.21.7.html#小幅迁移) (1.21.8 —— GraphicsWorkarounds)
- [功能提交：电影版](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.9-from-1.21.8.html#功能提交电影版) (1.21.9)
- [字体字形管线](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.9-from-1.21.8.html#字体-字形-管线) (1.21.9)
- [客户端资源拆分](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.9-from-1.21.8.html#客户端资源拆分) (1.21.9 次要)
- [哦，又来了，一次渲染重写](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.11-from-1.21.10.html#哦又来了一次渲染重写) (1.21.11)
- [Gizmo 控件](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.11-from-1.21.10.html#gizmo-控件) (1.21.11)
- [更多渲染变更](https://gu-zt.github.io/Porting-Primers/detailed-primers/26.1-from-1.21.11.html#更多渲染变更) (26.1)
- [实体纹理与成年/幼年模型](https://gu-zt.github.io/Porting-Primers/detailed-primers/26.1-from-1.21.11.html#实体纹理与成年幼年模型) (26.1 次要)
- [音频变更](https://gu-zt.github.io/Porting-Primers/detailed-primers/26.1-from-1.21.11.html#音频变更) (26.1 次要)

### 实体、生物、生物 AI、转化、生成和实体数据

- [交互结果](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.2-from-1.21.1.html#交互结果) (1.21.2)
- [爆——炸——！](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.2-from-1.21.1.html#爆炸) (1.21.2 次要 —— `Explosion` 现在是一个接口)
- [生物转化](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.2-from-1.21.1.html#生物转化) (1.21.2 次要 —— `Mob#convertTo` 已变更)
- [矿车行为](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.2-from-1.21.1.html#矿车行为) (1.21.2 次要)
- [末影珍珠加载区块](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.2-from-1.21.1.html#末影珍珠加载区块) (1.21.2 次要)
- [实体引用](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.5-from-1.21.4.html#实体引用) (1.21.5 次要 —— UUID 被 `EntityReference` 取代)
- [拴绳](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.6-from-1.21.5.html#拴绳) (1.21.6 次要)
- [类型化实体数据](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.9-from-1.21.8.html#类型化实体数据) (1.21.9 次要)
- [名称和 ID](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.9-from-1.21.8.html#名称和-id) (1.21.9 次要)
- [interactAt 的移除](https://gu-zt.github.io/Porting-Primers/detailed-primers/26.1-from-1.21.11.html#interactat-的移除) (26.1 次要 —— `Entity#interactAt` 已移除)
- [活动与大脑](https://gu-zt.github.io/Porting-Primers/detailed-primers/26.1-from-1.21.11.html#活动与大脑) (26.1 次要 —— AI 大脑系统变更)
- [更多实体声音变种注册表](https://gu-zt.github.io/Porting-Primers/detailed-primers/26.1-from-1.21.11.html#更多实体声音变种注册表) (26.1 次要)
- [僵尸鹦鹉螺变体](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.11-from-1.21.10.html#僵尸鹦鹉螺变体) (1.21.11 次要)

### GUI、输入、按键绑定、调试屏幕、调试工具、RPC 工具和测试基础设施

- [GUI 渲染类型](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.2-from-1.21.1.html#gui-渲染类型) (1.21.2)
- [游戏测试大修](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.5-from-1.21.4.html#游戏测试大修) (1.21.5)
- [GUI 变更](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.6-from-1.21.5.html#gui-变更) (1.21.6)
- [小幅迁移](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.7-from-1.21.6.html#小幅迁移) (1.21.7)
- [调试大修](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.9-from-1.21.8.html#调试大修) (1.21.9)
- [调试屏幕](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.9-from-1.21.8.html#调试屏幕) (1.21.9)
- [JSON-RPC 管理服务器](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.9-from-1.21.8.html#json-rpc-管理服务器) (1.21.9)
- [输入处理整合](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.9-from-1.21.8.html#输入处理整合) (1.21.9)
- [光标类型](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.9-from-1.21.8.html#光标类型) (1.21.9 次要)
- [Gizmo 控件](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.11-from-1.21.10.html#gizmo-控件) (1.21.11)
- [文本收集器](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.11-from-1.21.10.html#文本收集器) (1.21.11 次要)
- [OptionEnum 移除](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.11-from-1.21.10.html#optionenum-移除) (1.21.11 次要)
- [容器屏幕变更](https://gu-zt.github.io/Porting-Primers/detailed-primers/26.1-from-1.21.11.html#容器屏幕变更) (26.1 次要)
- [输入消息编辑器支持](https://gu-zt.github.io/Porting-Primers/detailed-primers/26.1-from-1.21.11.html#输入消息编辑器支持) (26.1 次要)
- [测试环境状态追踪](https://gu-zt.github.io/Porting-Primers/detailed-primers/26.1-from-1.21.11.html#测试环境状态追踪) (26.1 次要)

### 世界状态、保存数据、游戏规则、时间线、时钟、玩家、权限、路径点和其他服务端系统

- [正确处理方块实体的移除](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.5-from-1.21.4.html#正确处理方块实体的移除) (1.21.5)
- [体素形状辅助类](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.5-from-1.21.4.html#体素形状辅助类) (1.21.5)
- [加权列表重做](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.5-from-1.21.4.html#加权列表重做) (1.21.5)
- [加载票](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.5-from-1.21.4.html#加载票) (1.21.5)
- [保存数据，现在带有类型](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.5-from-1.21.4.html#保存数据现在带有类型) (1.21.5)
- [方块效果应用器](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.5-from-1.21.4.html#方块效果应用器) (1.21.5 次要)
- [路径点](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.6-from-1.21.5.html#路径点) (1.21.6)
- [服务端玩家变更](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.6-from-1.21.5.html#服务端玩家变更) (1.21.6)
- [权限来源](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.6-from-1.21.5.html#权限来源) (1.21.6 次要)
- [Level#isClientSide 现在为 private](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.9-from-1.21.8.html#levelisclientside-现在为-private) (1.21.9)
- [加载票标志](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.9-from-1.21.8.html#加载票标志) (1.21.9 次要)
- [重生数据](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.9-from-1.21.8.html#重生数据) (1.21.9 次要)
- [权限大修](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.11-from-1.21.10.html#权限大修) (1.21.11)
- [环境属性的时间线](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.11-from-1.21.10.html#环境属性的时间线) (1.21.11)
- [游戏规则洗牌](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.11-from-1.21.10.html#游戏规则洗牌) (1.21.11)
- [Level#random 字段现在为 protected](https://gu-zt.github.io/Porting-Primers/detailed-primers/26.1-from-1.21.11.html#levelrandom-字段现在为-protected) (26.1)
- [世界时钟与时间标记](https://gu-zt.github.io/Porting-Primers/detailed-primers/26.1-from-1.21.11.html#世界时钟与时间标记) (26.1)
- [将主关卡数据拆分为保存数据](https://gu-zt.github.io/Porting-Primers/detailed-primers/26.1-from-1.21.11.html#将主关卡数据拆分为保存数据) (26.1)
- [聊天权限](https://gu-zt.github.io/Porting-Primers/detailed-primers/26.1-from-1.21.11.html#聊天权限) (26.1 次要)
- [ChunkPos，现在是一个记录](https://gu-zt.github.io/Porting-Primers/detailed-primers/26.1-from-1.21.11.html#chunkpos现在是一个记录) (26.1 次要)
- [炼药锅交互调度器](https://gu-zt.github.io/Porting-Primers/detailed-primers/26.1-from-1.21.11.html#炼药锅交互调度器) (26.1 次要)
- [流体逻辑重组](https://gu-zt.github.io/Porting-Primers/detailed-primers/26.1-from-1.21.11.html#流体逻辑重组) (26.1 次要)
- [移除随机斑块特征](https://gu-zt.github.io/Porting-Primers/detailed-primers/26.1-from-1.21.11.html#移除随机斑块特征) (26.1 次要)
- [基于规则的方块状态提供者](https://gu-zt.github.io/Porting-Primers/detailed-primers/26.1-from-1.21.11.html#基于规则的方块状态提供者) (26.1 次要)
- [文件修缮工](https://gu-zt.github.io/Porting-Primers/detailed-primers/26.1-from-1.21.11.html#文件修复器) (26.1 次要；镜像注记：原页条目文字「文件修缮工」与锚点「文件修复器」不一致，原文如此)

### 其余的小幅迁移

- [语言文件的移除与重命名](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.2-from-1.21.1.html#语言文件的移除与重命名) (1.21.2)
- [MacosUtil#IS_MACOS](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.2-from-1.21.1.html#macosutilis_macos) (1.21.2)
- [更智能的帧率限制](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.2-from-1.21.1.html#更智能的帧率限制) (1.21.2)
- [朝向](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.2-from-1.21.1.html#朝向) (1.21.2)
- [移除雕刻生成步骤](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.2-from-1.21.1.html#移除雕刻生成步骤) (1.21.2)
- [连续执行器](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.2-from-1.21.1.html#连续执行器) (1.21.2)
- [分析器与 Tracy 客户端](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.2-from-1.21.1.html#分析器与-tracy-客户端) (1.21.2)
- [Tick节流器](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.2-from-1.21.1.html#Tick节流器) (1.21.2)
- [音乐，现在带有音量控制](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.4-from-1.21.2-3.html#音乐现在带有音量控制) (1.21.4)
- [解作用域玩家参数](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.5-from-1.21.4.html#解作用域玩家参数) (1.21.5)
- [重载实例创建](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.5-from-1.21.4.html#重载实例创建) (1.21.5)
- [JOML 后端接口](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.5-from-1.21.4.html#joml-后端接口) (1.21.5)
- [状态效果字段重命名](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.5-from-1.21.4.html#状态效果字段重命名) (1.21.5)
- [重载监听器共享状态](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.9-from-1.21.8.html#重载监听器共享状态) (1.21.9)
- [“在架子上” 变换](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.9-from-1.21.8.html#在架子上变换) (1.21.9)
- [共享文本区域调试器](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.11-from-1.21.10.html#共享文本区域调试器) (1.21.11)
- [特定逻辑变更](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.11-from-1.21.10.html#特定逻辑变更) (1.21.11)
- [类型化实例](https://gu-zt.github.io/Porting-Primers/detailed-primers/26.1-from-1.21.11.html#类型化实例) (26.1)
- [不再有绊线管线](https://gu-zt.github.io/Porting-Primers/detailed-primers/26.1-from-1.21.11.html#不再有绊线管线) (26.1)
- [环境属性新增](https://gu-zt.github.io/Porting-Primers/detailed-primers/26.1-from-1.21.11.html#环境属性新增) (26.1)
- [特定逻辑变更](https://gu-zt.github.io/Porting-Primers/detailed-primers/26.1-from-1.21.11.html#特定逻辑变更) (26.1)

每份入门文档的“小幅迁移”章节中还包含“新标签”、“标签变更”、“新增列表”、“变更列表”和“移除列表”子章节，见[详细入门文档](https://gu-zt.github.io/Porting-Primers/detailed-primers/README.html)。

## 类和方法索引

遇到编译错误或需要查找特定类/方法在哪里发生了变化时检索本表。

| 类 / 方法 | 版本 | 章节 |
| --- | --- | --- |
| `AbstractFurnaceBlockEntity` 燃料 | 1.21.2 | [燃料值](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.2-from-1.21.1.html#燃料值) |
| `AbstractMinecart` | 1.21.2 | [矿车行为](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.2-from-1.21.1.html#矿车行为) |
| `Activities` / `Brain` | 26.1 | [活动与大脑](https://gu-zt.github.io/Porting-Primers/detailed-primers/26.1-from-1.21.11.html#活动与大脑) |
| `AnimationDefinition#bake` | 1.21.6 | [动画烘焙](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.6-from-1.21.5.html#动画烘焙) |
| `ArmorItem` / `ArmorMaterial` | 1.21.2 | [盔甲材料、装备和模型（纹理）](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.2-from-1.21.1.html#盔甲材料装备和模型纹理) |
| `BakedModel` / `BakedQuad` | 1.21.5 | [模型重做](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.5-from-1.21.4.html#模型重做) |
| `BlockBehaviour#neighborChanged` | 1.21.2 | [朝向](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.2-from-1.21.1.html#朝向) |
| `BlockEntityType` 构造器 | 1.21.2 | [BlockEntityTypes 私有化了！](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.2-from-1.21.1.html#blockentitytypes-私有化了) |
| `CauldronInteraction` | 26.1 | [炼药锅交互调度器](https://gu-zt.github.io/Porting-Primers/detailed-primers/26.1-from-1.21.11.html#炼药锅交互调度器) |
| `ChunkPos`（现为记录） | 26.1 | [ChunkPos，现在是一个记录](https://gu-zt.github.io/Porting-Primers/detailed-primers/26.1-from-1.21.11.html#chunkpos现在是一个记录) |
| `ChunkSectionLayer` | 1.21.6 | [ChunkSectionLayers](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.6-from-1.21.5.html#chunksectionlayers) |
| 客户端物品 JSON | 1.21.4 | [客户端物品](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.4-from-1.21.2-3.html#客户端物品) |
| `Consumable` / `ConsumableListener` | 1.21.2 | [消耗品](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.2-from-1.21.1.html#消耗品) |
| `DataComponents` 获取器 | 1.21.5 | [数据组件获取器](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.5-from-1.21.4.html#数据组件获取器) |
| `DataComponents` 新类型 | 1.21.11 | [新数据组件](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.11-from-1.21.10.html#新数据组件) |
| `DataComponents` 初始化器 | 26.1 | [数据组件初始化器](https://gu-zt.github.io/Porting-Primers/detailed-primers/26.1-from-1.21.11.html#数据组件初始化器) |
| `DiggerItem` / `SwordItem` 移除 | 1.21.5 | [武器、工具和盔甲：去除冗余](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.5-from-1.21.4.html#武器工具和盔甲去除冗余) |
| `DyeRecipe` / `DyeItem` | 26.1 | [染料组件](https://gu-zt.github.io/Porting-Primers/detailed-primers/26.1-from-1.21.11.html#染料组件) |
| `Entity#interactAt` 移除 | 26.1 | [interactAt 的移除](https://gu-zt.github.io/Porting-Primers/detailed-primers/26.1-from-1.21.11.html#interactat-的移除) |
| `EntityReference`（取代 UUID） | 1.21.5 | [实体引用](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.5-from-1.21.4.html#实体引用) |
| `EntityRenderState` | 1.21.2 | [实体渲染状态](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.2-from-1.21.1.html#实体渲染状态) |
| `Explosion`（现为接口） | 1.21.2 | [爆——炸——！](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.2-from-1.21.1.html#爆炸) |
| `GameRules` | 1.21.11 | [游戏规则洗牌](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.11-from-1.21.10.html#游戏规则洗牌) |
| `GameTest` 框架 | 1.21.5 | [游戏测试大修](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.5-from-1.21.4.html#游戏测试大修) |
| `GenerationStep$Carving` 移除 | 1.21.2 | [移除雕刻生成步骤](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.2-from-1.21.1.html#移除雕刻生成步骤) |
| `GpuTexture` / `RenderPipeline` | 1.21.5 | [渲染管线重做](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.5-from-1.21.4.html#渲染管线重做) |
| `GuiGraphics` / GUI 渲染 | 1.21.6 | [GUI 变更](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.6-from-1.21.5.html#gui-变更) |
| `Holder` / `HolderSet` / `HolderGetter` | 1.21.2 | [持有者集过渡](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.2-from-1.21.1.html#持有者集-过渡) |
| `Identifier`（原 `ResourceLocation`） | 1.21.11 | [ResourceLocation 到 Identifier](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.11-from-1.21.10.html#resourcelocation-到-identifier) |
| `Ingredient` | 1.21.2 | [原料的转变](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.2-from-1.21.1.html#原料的转变) |
| `InteractionResult` | 1.21.2 | [交互结果](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.2-from-1.21.1.html#交互结果) |
| `ItemInstance` / `StackTemplate` | 26.1 | [物品实例与堆栈模板](https://gu-zt.github.io/Porting-Primers/detailed-primers/26.1-from-1.21.11.html#物品实例与堆栈模板) |
| `KeyMapping` / 输入事件 | 1.21.9 | [输入处理整合](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.9-from-1.21.8.html#输入处理整合) |
| `Leashable` | 1.21.6 | [拴绳](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.6-from-1.21.5.html#拴绳) |
| `Level#isClientSide` | 1.21.9 | [Level#isClientSide 现在为 private](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.9-from-1.21.8.html#levelisclientside-现在为-private) |
| `Level#random` | 26.1 | [Level#random 字段现在为 protected](https://gu-zt.github.io/Porting-Primers/detailed-primers/26.1-from-1.21.11.html#levelrandom-字段现在为-protected) |
| `LootContextParam` / `LootContextParamSet` | 1.21.2 | [上下文键](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.2-from-1.21.1.html#上下文键) |
| `LootPoolEntry` / 战利品编解码器 | 26.1 | [战利品类型展开](https://gu-zt.github.io/Porting-Primers/detailed-primers/26.1-from-1.21.11.html#战利品类型展开) |
| `Mob#convertTo` | 1.21.2 | [生物转化](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.2-from-1.21.1.html#生物转化) |
| `OptionEnum` 移除 | 1.21.11 | [OptionEnum 移除](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.11-from-1.21.10.html#optionenum-移除) |
| `Permission` / `PermissionSet` | 1.21.11 | [权限大修](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.11-from-1.21.10.html#权限大修) |
| `Profiler#get`（取代 `getProfiler`） | 1.21.2 | [分析器与 Tracy 客户端](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.2-from-1.21.1.html#分析器与-tracy-客户端) |
| `Recipe` 注册表格式 | 1.21.2 | [配方，现在采用注册表格式](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.2-from-1.21.1.html#配方现在采用注册表格式) |
| `RecipeDisplay` / `SlotDisplay` | 1.21.2 | [配方，现在采用注册表格式](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.2-from-1.21.1.html#配方现在采用注册表格式) |
| `RenderType` 洗牌 | 1.21.11 | [哦，又来了，一次渲染重写](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.11-from-1.21.10.html#哦又来了一次渲染重写) |
| `SavedData` / `SavedDataType` | 1.21.5 | [保存数据，现在带有类型](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.5-from-1.21.4.html#保存数据现在带有类型) |
| `ServerExplosion` | 1.21.2 | [爆——炸——！](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.2-from-1.21.1.html#爆炸) |
| 着色器 JSON / `.vsh` / `.fsh` | 1.21.2 | [着色器重写](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.2-from-1.21.1.html#着色器重写) |
| `SimpleJsonResourceReloadListener` | 1.21.4 | [SimpleJsonResourceReloadListener](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.4-from-1.21.2-3.html#simplejsonresourcereloadlistener) |
| `TagProvider` 追加器 | 1.21.6 | [标签提供者：追加器重写](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.6-from-1.21.5.html#标签提供者-追加器重写) |
| `Validatable` / `ValidationContext` | 26.1 | [验证大修](https://gu-zt.github.io/Porting-Primers/detailed-primers/26.1-from-1.21.11.html#验证大修) |
| 村民交易（数据包） | 26.1 | [数据包村民交易](https://gu-zt.github.io/Porting-Primers/detailed-primers/26.1-from-1.21.11.html#数据包村民交易) |
| `VoxelShape` 辅助类 | 1.21.5 | [体素形状辅助类](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.5-from-1.21.4.html#体素形状辅助类) |
| `Waypoint` 系统 | 1.21.6 | [路径点](https://gu-zt.github.io/Porting-Primers/detailed-primers/1.21.6-from-1.21.5.html#路径点) |
| 世界时钟 / 时间标记 | 26.1 | [世界时钟与时间标记](https://gu-zt.github.io/Porting-Primers/detailed-primers/26.1-from-1.21.11.html#世界时钟与时间标记) |
| 世界数据拆分 | 26.1 | [将主关卡数据拆分为保存数据](https://gu-zt.github.io/Porting-Primers/detailed-primers/26.1-from-1.21.11.html#将主关卡数据拆分为保存数据) |

## 来源与署名

拆分后的入门文档页面复制自 `ChampionAsh5357/neoforged-github`，分支 `update/26.1`。详见[来源与署名](https://gu-zt.github.io/Porting-Primers/source-and-attribution.html)。
