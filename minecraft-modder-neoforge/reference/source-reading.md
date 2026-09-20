# 参考开源模组与查阅依赖源码

## 参考开源模组

官方文档和在线搜索不足以解决问题时，可在 GitHub 搜索其他模组的实现代码作参考，必须遵守：

- **注明来源** — 在项目 `README.md` 中列出参考过的模组及仓库地址。
- **遵守许可协议** — 使用前确认许可证（MIT 可自由使用；GPL 要求你的项目也以 GPL 开源；ARR 默认禁止使用），禁止违反原项目许可条款。
- **学习思路，不盲目复制** — 理解设计思路后在自己的项目结构下重新实现，禁止直接粘贴代码。

## 查阅依赖源码

需要查看前置模组或依赖库的具体实现才能正确调用其 API 时，将依赖源码提取到本地查阅：

1. **优先使用 sources.jar** — Gradle 下载依赖时会同时拉取 `-sources.jar`，解压到项目 `reference/` 目录下即可浏览源码。
2. **反编译兜底** — 依赖未提供 sources.jar 时，使用 IDEA 内置的 java-decompiler 命令行反编译：

   ```bash
   java -cp "${IDEA_PATH}/plugins/java-decompiler/lib/java-decompiler.jar" \
       org.jetbrains.java.decompiler.main.decompiler.ConsoleDecompiler \
       -dgs=true \
       "<待反编译的JAR文件>" \
       "<输出目录>"
   ```

   执行后输出目录下生成一个 `.jar` 文件，需再解压得到 `.java` 源码：

   ```bash
   # 假设输出到 reference/，生成的文件类似 reference/<modid>.jar
   unzip reference/<modid>.jar -d reference/<modid>/
   ```

   `${IDEA_PATH}` 替换为本地 IntelliJ IDEA 安装路径。
3. **必须加入 .gitignore** — `reference/` 目录必须加入 `.gitignore`，防止将他人代码意外发布。
