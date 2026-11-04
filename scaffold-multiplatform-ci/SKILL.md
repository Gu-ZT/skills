---
name: scaffold-multiplatform-ci
description: 为原生或桌面端项目创建与更新跨操作系统、跨 CPU 架构的 GitHub Actions CI 与发布工作流。用于配置多平台质量检查矩阵、容器集成测试、交叉编译目标、安装包打包上传、签名门禁与按架构分类的双语 Release Notes 时加载。
---

# 多平台与多架构 CI/Release 工作流规范

## references/ 导航

| 文档 | 内容 |
| --- | --- |
| [references/matrix-recipes.md](references/matrix-recipes.md) | Windows / Linux / macOS / Android 常见 runner、编译目标三元组、打包格式与交叉编译校验规则 |
| [references/workflow-template.yml](references/workflow-template.yml) | 包含 `quality`、`integration`、`prepare`、`build`、`update-release-notes` 五阶段的 GitHub Actions 骨架模板 |

## 架构矩阵设计原则

编写工作流 YAML 前，必须先盘点仓库工具链（Rust / Go / C++ / Node）、锁文件、原生 SDK 依赖、打包工具与现有发布约定，再确定支持矩阵。每个矩阵项必须明确记录：

- GitHub Actions runner 镜像名称。
- 编译器或交叉编译目标三元组（target triple）。
- 依赖的系统 SDK、运行库及第三方许可证文件要求。
- 安装包格式与产物文件名后缀。
- 是否具备代码签名与公证（notarization）条件。
- 包含操作系统与目标架构的独立缓存键（如 `linux-aarch64-release`）。

架构覆盖遵循应纳尽纳原则：只要项目源码、依赖库、系统 SDK 与工具链能够编译并打包某个目标平台，就必须将其加入 CI，包括 Windows ARM64、Linux ARM64 和 macOS x86_64 等架构。优先使用原生架构 runner；仅能交叉编译时，仍必须在 CI 中执行编译与打包校验，并在文档和发布说明中注明该架构仅完成构建校验、未执行原生运行时测试。仅当用户明确缩减支持范围，或存在具体的工具链与依赖阻塞并在文档中写明原因时，才允许省略目标架构。

## 五阶段流水线设计

基于 [references/workflow-template.yml](references/workflow-template.yml) 生成单一工作流，禁止将 CI 检查与 Release 发布拆成两个重复运行相同测试的工作流。触发条件（`on`）中，`pull_request` 仅运行校验，禁止触发任何发布动作；除用户明确关闭持续预发布外，默认分支（如 `main`）的每次成功 `push` 自动发布带唯一标识的预发布版本（prerelease），精确匹配版本号的 Git 标签（`v*`）发布正式版本（stable release）。工作流最小权限仅授予 `contents: write`。

五个阶段依次为：

1. **质量检查（`quality`）**：设置 `fail-fast: false` 的多操作系统矩阵。安装原生系统依赖与锁文件依赖，执行格式检查、严格 lint（将警告视为错误）、全量单元测试与前端构建检查。
2. **集成测试（`integration`）**：在独立 Linux runner 上启动真实协议服务或 Docker 容器，使用带超时上限的循环等待服务就绪，按需串行运行集成测试；清理步骤必须配置 `if: always()` 以收集容器日志并销毁容器与卷。
3. **发布准备（`prepare`）**：依赖 `quality` 与 `integration` 全部成功。默认分支构建生成唯一预发布标签（如 `v<manifest-version>-dev.<run-number>`），标签构建校验其与清单版本精确一致。以幂等且草稿（`draft: true`）状态创建或复用 GitHub Release，输出 `release_id`、`tag`、`version`、`changelog_version` 与 `prerelease` 状态。
4. **多架构构建打包（`build`）**：依赖 `prepare`，显式指定目标三元组与包含架构的缓存键。打包前安装对应平台 SDK，将生成的安装包、校验和与许可证文件上传至草稿 Release。签名与未签名路径必须隔离，签名密钥仅注入签名步骤。
5. **发布说明与正式公开（`update-release-notes`）**：依赖全部 `build` 任务成功。提取中英双语 Changelog 中对应版本的章节，生成按平台与架构分类的下载表格（表格中的文件名必须直接链接到 Release 产物的实际下载 URL），校验通过后取消草稿状态并按 `prerelease` 标志正式发布。

## 版本与安全约束

- 每次自动发布的提交必须拥有唯一且不可变的发布标识：CI 预发布通过追加运行编号或提交哈希区分，避免每次推送都手动修改版本文件；发布下一个正式版前必须递增清单版本号。
- 工作区清单、锁文件、前端 `package.json` 与原生应用清单中的版本号必须保持同步，且中英双语 Changelog 中均必须存在对应的 `## [x.y.z]` 章节；预发布版本读取基础版本号对应的 Changelog 章节，并在产物文件名中保留预发布版本后缀。
- 产物文件名不匹配发布说明分类规则，或发布说明中的产物条目未链接到实际 Release 下载 URL 时，必须在发布阶段直接报错终止。
- 禁止在产物、日志、发布说明或工作流 output 中暴露凭据、签名证书、私钥或 Token。
- 第三方 Action 必须锁定维护中的主版本号并配合锁文件安装依赖；环境变量中显式固定构建所用的 Node 版本（如 Node 24）。
- `continue-on-error` 仅允许用于明确标为可选的签名或诊断步骤，禁止用于质量门禁或打包步骤。
- 模糊失败后禁止自动重放非幂等操作；重复推送或重跑工作流时，`prepare` 阶段禁止覆盖无关标签，且预发布版本必须显式标记 `prerelease=true` 以免覆盖仓库的最新正式版（Latest Release）。

## 提交前验证与汇报要求

提交工作流前必须在本地运行与 CI 一致的格式、静态检查、单元测试、前端构建、发布说明链接测试及空白字符检查（例如 `cargo fmt --all -- --check`、`cargo clippy --workspace --all-targets --locked -- -D warnings`、`cargo test --workspace --locked`、`node --test <release-notes-tests>`、`<frontend-build-command>` 与 `git diff --check`）；严禁仅凭单一操作系统的单元测试通过就宣称跨平台打包已验证。

交付工作流时必须同步列出：支持与显式排除的平台架构表、质量与集成测试命令、产物命名与下载链接规则、所需的仓库 Secrets 及无签名回退行为、版本号与双语 Changelog 约束、以及本地与 CI 验证命令。

## Checklist

- [ ] 是否已检查 Windows / Linux 的 `x86_64` 与 `aarch64` 以及 macOS 的 `aarch64` 与 `x86_64`，并为可构建目标全部配置了包含架构名的缓存键？
- [ ] `quality` 与 `integration` 是否设置 `fail-fast: false`，且 `prepare` 与 `build` 严格依赖二者成功？
- [ ] `integration` 容器日志收集与清理步骤是否均配置了 `if: always()`？
- [ ] 工作区清单、锁文件、前端与原生应用清单版本号是否同步，且中英双语 Changelog 均包含对应 `## [x.y.z]` 章节？
- [ ] GitHub Release 在全部架构打包、校验和上传与双语下载表更新完成前是否保持 `draft` 状态？
- [ ] `pull_request` 是否已完全阻断发布，且预发布版本保留文件名预发布后缀并明确设置 `prerelease=true`？
- [ ] Release Notes 中的产物名是否为指向实际 Release 下载地址的可点击链接？
- [ ] 第三方 Action 是否已锁定主版本、显式指定 Node 版本，且 `continue-on-error` 未用于质量门禁或打包步骤？
- [ ] 签名密钥是否仅在签名步骤注入，且未出现在任何日志、产物或工作流输出中？
- [ ] 提交前是否已在本地通过格式检查、严格 lint、单元测试、前端构建、发布说明测试及 `git diff --check`？
