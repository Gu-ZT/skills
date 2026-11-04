# 查阅依赖源码与参考开源模组

## 提取与查阅依赖源码

需要核对前置模组、辅助库或原版类的具体实现细节时，按以下顺序在本地提取源码：

1. **优先解压 `-sources.jar`**：Gradle 同步依赖时通常会一并缓存 `-sources.jar`，可直接将其解压到项目根目录下的 `reference/<modid>/` 中查阅。
2. **命令行反编译**：当依赖未发布 `-sources.jar` 时，调用 IntelliJ IDEA 内置的 FernFlower（`java-decompiler.jar`）将二进制 JAR 反编译为源码包，再解压为 `.java` 文件：

   ```bash
   java -cp "${IDEA_PATH}/plugins/java-decompiler/lib/java-decompiler.jar" org.jetbrains.java.decompiler.main.decompiler.ConsoleDecompiler -dgs=true "<待反编译的JAR路径>" "reference/"
   unzip "reference/<jar文件名>.jar" -d "reference/<modid>/"
   ```

   其中 `${IDEA_PATH}` 替换为本机 IntelliJ IDEA 的安装目录。
3. **配置 `.gitignore`**：凡是解压到项目 `reference/` 目录下的第三方源码或反编译文件，**必须将 `reference/` 加入 `.gitignore`**，严禁提交到版本库。

## 参考其他开源模组的合规要求

当官方文档未覆盖某项实现机制、需要参考 GitHub 上其他开源模组的代码时，必须遵守以下三条约束：

- **核对开源许可证**：借鉴前先检查目标仓库的 LICENSE。MIT / Apache-2.0 允许在合规署名下复用；GPL 具有传染性，引用其代码要求当前项目同样采用 GPL 协议开源；ARR（All Rights Reserved）或未声明许可证的仓库严禁复制任何代码。
- **注明参考来源**：在当前项目的 `README.md` 致谢或说明章节中列出参考过的模组名称与仓库链接。
- **理解后独立实现**：结合当前模组的包结构与目标版本 API 重新编写逻辑，禁止直接原样粘贴外部仓库的代码片段。
